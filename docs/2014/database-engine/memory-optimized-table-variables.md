---
title: Le variabili di tabella ottimizzate | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774416"
---
# <a name="memory-optimized-table-variables"></a>Variabili di tabella con ottimizzazione per la memoria
  Oltre alle tabelle ottimizzate per la memoria per l'accesso efficiente ai dati e alle stored procedure compilate in modo nativo per l'elaborazione efficiente delle query e l'esecuzione della logica di business, [!INCLUDE[hek_2](../includes/hek-2-md.md)] introduce un terzo tipo di oggetto: il tipo di tabella ottimizzata per la memoria. Una variabile di tabella creata utilizzando un tipo di tabella ottimizzata per la memoria è una variabile di tabella ottimizzata per la memoria.  
  
 Le variabili di tabella con ottimizzazione per la memoria offrono i vantaggi descritti di seguito rispetto alle variabili di tabella basate su disco:  
  
-   Le variabili sono archiviate solo in memoria. L'accesso ai dati è più efficiente poiché il tipo di tabella ottimizzata per la memoria utilizza lo stesso algoritmo e le stesse strutture dei dati ottimizzate per la memoria utilizzati per le tabelle ottimizzate per la memoria, in particolare quando le variabili sono utilizzate in stored procedure compilate in modo nativo.  
  
-   Con le variabili di tabella ottimizzata per la memoria, non viene utilizzato tempdb. Le variabili di tabella non vengono archiviate in tempdb e non utilizzano alcuna risorsa in tempdb.  
  
 Gli scenari di utilizzo tipici per le variabili di tabella ottimizzata per la memoria sono:  
  
-   Archiviazione dei risultati intermedi e creazione di singoli set di risultati basati su più query in stored procedure compilate in modo nativo.  
  
-   Passaggio di parametri con valori di tabella alle stored procedure compilate in modo nativo e alle stored procedure interpretate.  
  
-   Sostituzione delle variabili di tabella basata su disco e, in alcuni casi, delle tabelle #temp locali in una stored procedure. Si tratta di un aspetto particolarmente utile se sono presenti contese di tempdb nel sistema.  
  
-   Le variabili di tabella possono essere utilizzate per simulare i cursori in stored procedure compilate in modo nativo, con cui è possibile risolvere le limitazioni della superficie di attacco in stored procedure compilate in modo nativo.  
  
 Come per le tabelle ottimizzate per la memoria, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] genera una DLL per ogni tipo di tabella ottimizzata per la memoria. (La compilazione viene richiamata quando viene creato il tipo di tabella con ottimizzazione per la memoria e non quando viene utilizzato per creare le variabili di tabella con ottimizzazione per la memoria). La DLL include le funzioni per l'accesso a indici e il recupero dei dati dalle variabili di tabella. Quando una variabile di tabella ottimizzata per la memoria viene dichiarata in base al tipo di tabella, nella sessione utente viene creata un'istanza delle strutture di indice e della tabella corrispondenti al tipo di tabella. La variabile di tabella può quindi essere utilizzata in modo analogo alle variabili di tabella basata su disco. È possibile inserire, aggiornare ed eliminare righe nella variabile di tabella, nonché utilizzare le variabili nelle query di [!INCLUDE[tsql](../includes/tsql-md.md)] . È inoltre possibile passare le variabili alle stored procedure compilate in modo nativo e interpretate, come parametri con valori di tabella.  
  
 L'esempio seguente viene illustrato un tipo di tabella con ottimizzazione per la memoria dall'esempio basato su AdventureWorks OLTP In memoria ([esempio di OLTP In memoria di SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491)).  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 Nell'esempio viene illustrato che la sintassi dei tipi di tabella ottimizzata per la memoria è simile ai tipi di tabella basati su disco, con le seguenti eccezioni:  
  
-   `MEMORY_OPTIMIZED=ON` indica se il tipo di tabella è ottimizzato per la memoria.  
  
-   Il tipo deve contenere almeno un indice. Analogamente alle tabelle ottimizzate per la memoria, è possibile utilizzare indici hash e non cluster.  
  
     Per un indice hash, il numero di bucket deve essere da una a due volte il numero previsto di chiavi di indice univoche. Per ulteriori informazioni, vedere [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
-   Il tipo di dati e le restrizioni relative ai vincoli nelle tabelle ottimizzate per la memoria si applicano anche ai tipi di tabella ottimizzata per la memoria. Ad esempio, in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sono supportati i vincoli predefiniti, ma non i vincoli CHECK.  
  
 Come le tabelle ottimizzate per la memoria, le variabili di tabella ottimizzata per la memoria  
  
-   Non supportano piani paralleli.  
  
-   Non devono superare la memoria disponibile e non devono utilizzare le risorse del disco.  
  
 Le variabili di tabella basata su disco si trovano in tempdb. Le variabili di tabella con ottimizzazione per la memoria si trovano nel database utente, ma non utilizzano spazio di archiviazione e non vengono recuperate.  
  
 Non è possibile creare una variabile di tabella ottimizzata per la memoria utilizzando la sintassi inline. A differenza delle variabili di tabella basate su disco, è necessario creare prima un tipo.  
  
## <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 Il seguente script di esempio illustra la dichiarazione di una variabile di tabella come tipo di tabella ottimizzata per la memoria `Sales.SalesOrderDetailType_inmem`, l'inserimento di tre righe nella variabile e il passaggio della variabile come parametro con valori di tabella in `Sales.usp_InsertSalesOrder_inmem`.  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 I tipi di tabella con ottimizzazione per la memoria possono essere utilizzati come tipo per i parametri con valori di tabella di stored procedure e i client possono fare riferimento a essi esattamente allo stesso modo di parametri con valori di tabella e tipi di tabella basata su disco. Pertanto, la chiamata di stored procedure con parametri con valori di tabella ottimizzata per la memoria e stored procedure compilate in modo nativo ha un funzionamento analogo alla chiamata di stored procedure interpretate con parametri con valori di tabella basata su disco.  
  
## <a name="temp-table-replacement"></a>Sostituzione della tabella #temp  
 Nell'esempio seguente vengono illustrati tipi di tabella e variabili di tabella ottimizzata per la memoria come sostituti di tabelle #temp locali in una stored procedure.  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>Creazione di un singolo set di risultati  
 Nell'esempio seguente viene illustrato come archiviare i risultati intermedi e creare singoli set di risultati basati su più query in stored procedure compilate in modo nativo. L'esempio calcola l'unione `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`.  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>Consumo di memoria per le variabili di tabella  
 Il consumo di memoria per le variabili di tabella è simile alle tabelle ottimizzate per la memoria, ad eccezione degli indici non cluster. Se si inseriscono molte righe nelle variabili di tabella ottimizzata per la memoria con indici non cluster e se le chiavi di indice sono di grandi dimensioni, queste variabili di tabella utilizzano una quantità di memoria sproporzionata. Gli indici non cluster nelle variabili di tabella di grandi dimensioni richiedono proporzionalmente una quantità di memoria superiore rispetto a quella richiesta da un indice non cluster per lo stesso numero di righe inserite in una tabella (maggiore quantità di memoria nelle pagine di indice).  
  
 La memoria per le variabili di tabella proviene dal pool di risorse di Resource Governor del database.  
  
 A differenza delle tabelle ottimizzate per la memoria, la memoria utilizzata (incluse le righe eliminate) dalle variabili di tabella viene liberata quando la variabile di tabella abbandona l'ambito.  
  
 La memoria viene rappresentata come parte di un singolo consumer di memoria di PGPOOL del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di Transact-SQL per OLTP in memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
