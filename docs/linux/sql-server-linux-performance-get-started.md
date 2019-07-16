---
title: Introduzione alle funzionalità delle prestazioni di SQL Server in Linux
description: Questo articolo fornisce un'introduzione delle funzionalità delle prestazioni di SQL Server per Linux gli utenti che hanno familiarità con SQL Server. Molti di questi esempi funzionano in tutte le piattaforme, ma il contesto di questo articolo è un sistema Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: fe60b00654d93c6362a8671318a4b7b88ae90a5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896160"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Procedura dettagliata per le funzionalità delle prestazioni di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se sei un utente di Linux che è una novità di SQL Server, le attività seguenti illustrano alcune delle funzionalità delle prestazioni. Questi non sono specifiche di Linux o univoco, ma è utile per dare un'idea delle aree per analizzare ulteriormente il problema. In ogni esempio viene fornito un collegamento alla documentazione di profondità per quell'area.

> [!NOTE]
> Gli esempi seguenti usano il database di esempio AdventureWorks. Per istruzioni su come ottenere e installare il database di esempio, vedere [ripristinare un database di SQL Server da Windows a Linux](sql-server-linux-migrate-restore-database.md).

## <a name="create-a-columnstore-index"></a>Creare un indice Columnstore
Un indice columnstore è una tecnologia per l'archiviazione e query su grandi archivi di dati in un formato di dati in colonna, detto columnstore.  

1. Aggiungere un indice Columnstore sulla tabella SalesOrderDetail eseguendo i comandi Transact-SQL seguenti:

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Eseguire la query seguente che usa l'indice Columnstore per analizzare la tabella seguente:

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Verificare che l'indice Columnstore è stato usato da ricerca di object_id per l'indice Columnstore e per confermare che venga visualizzato in statistiche di utilizzo per la tabella SalesOrderDetail:

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>Usare OLTP In memoria
SQL Server fornisce le funzionalità di OLTP In memoria che possono migliorare notevolmente le prestazioni dei sistemi di applicazione.  In questa sezione della Guida alla valutazione illustrerà i passaggi per creare una tabella con ottimizzazione per la memoria archiviata in memoria e una stored procedure compilata in modo nativo che può accedere alla tabella senza la necessità di essere compilate o interpretate.

### <a name="configure-database-for-in-memory-oltp"></a>Configurare i Database per OLTP In memoria
1. È consigliabile impostare il database a un livello di compatibilità di almeno 130 per usare OLTP In memoria.  Usare la query seguente per verificare il livello di compatibilità corrente di AdventureWorks:  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   Se necessario, aggiornare il livello 130:

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. Quando una transazione include una tabella basata su disco e una tabella con ottimizzazione per la memoria, è essenziale che la parte con ottimizzazione per la memoria della transazione operano a livello di isolamento transazione denominato SNAPSHOT.  Per applicare in modo affidabile questo livello per le tabelle ottimizzate per la memoria in una transazione tra contenitori, eseguire le operazioni seguenti:

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. Prima di poter creare una tabella con ottimizzazione per la memoria è necessario innanzitutto creare un FILEGROUP con ottimizzazione per la memoria e un contenitore per i file di dati:

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>Creare una tabella con ottimizzazione per la memoria
L'archivio primario per le tabelle ottimizzate per la memoria è la memoria principale e pertanto a differenza delle tabelle basate su disco, i dati non devono essere letta dal disco nei buffer di memoria.  Per creare una tabella con ottimizzazione per la memoria, usare il MEMORY_OPTIMIZED = ON clausola.

1. Eseguire la query seguente per creare la tabella ottimizzata per la memoria dbo. ShoppingCart.  Per impostazione predefinita, i dati verranno resi persistenti su disco per motivi di durabilità (si noti che durabilità è anche possibile impostare in modo permanente solo lo schema). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. Inserire alcuni record nella tabella:

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>Stored Procedure compilate in modo nativo
SQL Server supporta le stored procedure compilate in modo nativo che accedono alle tabelle ottimizzate per la memoria. Le istruzioni T-SQL vengono compilate in codice macchina e archiviate come DLL native, consentendo l'accesso ai dati più veloce e l'esecuzione di query più efficiente rispetto alle tradizionali soluzioni T-SQL.   Le stored procedure che sono contrassegnate con NATIVE_COMPILATION vengono compilate in modo nativo. 

1. Eseguire lo script seguente per creare una stored procedure compilata in modo nativo che inserisce un numero elevato di record nella tabella ShoppingCart:


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. Inserire 1.000.000 di righe:

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. Verificare che le righe sono state inserite:

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>Altre informazioni su OLTP In memoria
Per ulteriori informazioni su OLTP In memoria, vedere gli argomenti seguenti:

- [Avvio rapido 1: tecnologie OLTP in memoria per migliorare le prestazioni di Transact-SQL](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [Migrazione a OLTP in memoria](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [Tabella temporanea più rapida e variabile di tabella tramite l'ottimizzazione per la memoria](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [Monitorare e risolvere i problemi relativi all'utilizzo della memoria](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [OLTP in memoria (ottimizzazione per la memoria)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>Usare Query Store
Query Store raccoglie informazioni dettagliate sulle prestazioni relative query, piani di esecuzione e le statistiche di runtime.

Query Store non è attiva per impostazione predefinita e può essere abilitata con ALTER DATABASE:

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

Eseguire la query seguente per restituire informazioni sulle query e piani in archivio query: 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>Viste a gestione dinamica delle query
Viste a gestione dinamica restituiscono informazioni sullo stato di server che possono essere utilizzate per monitorare l'integrità di un'istanza del server, diagnosticare i problemi e ottimizzare le prestazioni.

Per eseguire query sulla vista a gestione dinamica delle statistiche dm_os_wait:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
