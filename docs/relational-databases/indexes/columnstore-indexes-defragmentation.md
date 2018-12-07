---
title: Indici columnstore - Deframmentazione | Microsoft Docs
ms.custom: ''
ms.date: 01/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d3efda1a-7bdb-47f5-80bf-f075329edee5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c33b07af2ad43f15913580ce55c173d04a876366
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511536"
---
# <a name="columnstore-indexes---defragmentation"></a>Indici columnstore - Deframmentazione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Attività per la deframmentazione degli indici columnstore.  
  
## <a name="use-alter-index-reorganize-to-defragment-a-columnstore-index-online"></a>Usare ALTER INDEX REORGANIZE per deframmentare un indice columnstore online  
 **Si applica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
Dopo l'esecuzione di carichi di qualsiasi tipo, è possibile che rimangano più rowgroup piccoli nel deltastore. È possibile usare `ALTER INDEX REORGANIZE` per forzare l'inserimento di tutti i rowgroup in columnstore e poi combinare i rowgroup in un numero inferiore di rowgroup con più righe.  L'operazione di riorganizzazione rimuoverà anche le righe che sono state eliminate dal columnstore.  
  
Per altre informazioni, vedere i post di blog seguenti nel blog del team del motore di database SQL.  
-   [Riduzione al minimo della frammentazione dell'indice negli indici columnstore](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
-   [Indici columnstore e criteri di unione per rowgroup](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
### <a name="recommendations-for-reorganizing"></a>Suggerimenti per la riorganizzazione  
Riorganizzare un indice columnstore dopo uno o più caricamenti di dati per migliorare rapidamente le prestazioni delle query. La riorganizzazione inizialmente richiede risorse di CPU aggiuntive per comprimere i dati, il che potrebbe globalmente ridurre le prestazioni del sistema. Tuttavia, non appena i dati sono compressi, le prestazioni delle query possono migliorare.  
  
Usare l'esempio in [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) per calcolare la frammentazione. Questo permette di determinare se vale la pena eseguire un'operazione REORGANIZE.  
  
### <a name="example-how-reorganizing-works"></a>Esempio: funzionamento della riorganizzazione  
 Questo esempio mostra come usare ALTER INDEX REORGANIZE per forzare l'inserimento di tutti i rowgroup di deltastore in columnstore, per poi combinare i rowgroup.  
  
1.  Eseguire questo codice Transact-SQL per creare una tabella di staging contenente 300.000 righe. Questa tabella verrà usata per il caricamento bulk di righe in un indice columnstore.  
  
    ```sql  
    USE master;  
    GO  
  
    IF EXISTS (SELECT name FROM sys.databases  
        WHERE name = N'[columnstore]')  
        DROP DATABASE [columnstore];  
    GO  
  
    CREATE DATABASE [columnstore];  
    GO  
  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'staging'  
        AND object_id = OBJECT_ID (N'staging'))  
    DROP TABLE dbo.staging;  
    GO  
  
    CREATE TABLE [staging] (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int  
    );  
    GO  
  
    -- Load data  
    DECLARE @loop int;  
    DECLARE @AccountDescription varchar(50);  
    DECLARE @AccountKey int;  
    DECLARE @AccountType varchar(50);  
    DECLARE @AccountCode int;  
  
    SELECT @loop = 0;  
    BEGIN TRAN  
        WHILE (@loop < 300000)   
          BEGIN  
            SELECT @AccountKey = CAST (RAND()*10000000 AS int);  
            SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountCode =  CAST (RAND()*10000000 AS int);  
  
            INSERT INTO staging VALUES (  
               @AccountKey,   
               @AccountDescription,   
               @AccountType,   
               @AccountCode  
            );  
  
            SELECT @loop = @loop + 1;  
          END  
    COMMIT  
    ```  
  
2.  Creare una tabella archiviata come indice columnstore.  
  
    ```sql  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'cci_target'  
        AND object_id = OBJECT_ID (N'cci_target'))  
    DROP TABLE dbo.cci_target;  
    GO  
  
    -- Create a table with a clustered columnstore index  
    -- and the same columns as the rowstore staging table.  
    CREATE TABLE cci_target (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int,  
         INDEX idx_cci_target CLUSTERED COLUMNSTORE  
    )  
    GO  
    ```  
  
3.  Inserimento bulk della righe della tabella di staging nella tabella columnstore. `INSERT INTO ... SELECT` esegue un inserimento bulk. `TABLOCK` consente l'esecuzione di `INSERT` con parallelismo.  
  
    ```sql  
    -- Insert rows in parallel  
    INSERT INTO cci_target WITH (TABLOCK)  
    SELECT TOP (300000) * FROM staging;  
    GO  
    ```  
  
4.  Visualizzare i rowgroup tramite la DMV *sys.dm_db_column_store_row_group_physical_stats*.  
  
    ```sql  
    -- Run this dynamic management view (DMV) to see the OPEN rowgroups.   
    -- The number of rowgroups depends on the degree of parallelism.   
    -- You will see multiple OPEN rowgroups depending on the degree of parallelism.   
    -- This is because insert operation can run in parallel in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     In questo esempio, i risultati mostrano 8 rowgroup OPEN ognuno con 37.500 righe. Il numero di rowgroup OPEN dipende dall'impostazione *max_degree_of_parallelism*.  
  
     ![Rowgroup OPEN](../../relational-databases/indexes/media/cci-openrowgroups.png "Rowgroup OPEN")  
  
5.  Usare `ALTER INDEX REORGANIZE` con l'opzione `COMPRESS_ALL_ROW_GROUPS` per forzare la compressione di tutti i rowgroup nel columnstore.  
  
    ```sql  
    -- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
    ALTER INDEX idx_cci_target ON cci_target   
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     I risultati mostrano 8 rowgroup COMPRESSED e 8 rowgroup TOMBSTONE. Ogni rowgroup viene compresso nel columnstore indipendentemente dalle dimensioni. I rowgroup TOMBSTONE verranno rimossi dal sistema.  
  
     ![Rowgroup TOMBSTONE e COMPRESSED](../../relational-databases/indexes/media/cci-tombstone-compressed-rowgroups.png "Rowgroup TOMBSTONE e COMPRESSED")  
  
6.  Per le prestazioni delle query, è molto meglio combinare i rowgroup piccoli. `ALTER INDEX REORGANIZE` combinerà `COMPRESSED` rowgroup. Ora che i rowgroup delta sono compressi nel columnstore, eseguire di nuovo ALTER INDEX REORGANIZE per combinare i rowgroup COMPRESSED piccoli. In questo caso l'opzione `COMPRESS_ALL_ROW_GROUPS` non è necessaria.  
  
    ```sql  
    -- Run this again and you will see that smaller rowgroups   
    -- combined into one compressed rowgroup with 300,000 rows  
    ALTER INDEX idx_cci_target ON cci_target REORGANIZE;  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     I risultati mostrano che gli 8 rowgroup COMPRESSED sono ora combinati in un solo rowgroup COMPRESSED.  
  
     ![Rowgroup combinati](../../relational-databases/indexes/media/cci-compressed-rowgroups.png "Rowgroup combinati")  
  
## <a name="rebuild"></a> Usare ALTER INDEX REORGANIZE per deframmentare un indice columnstore offline  
 Per [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive, la ricompilazione dell'indice columnstore in genere non è necessaria perché `REORGANIZE` esegue gli aspetti principali di una ricompilazione in background come operazione online.  
  
 La ricompilazione di un indice columnstore consente di rimuovere la frammentazione e spostare tutte le righe nel columnstore. È possibile usare [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) o [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) per eseguire la ricompilazione completa di un indice columnstore cluster esistente. È anche possibile usare ALTER INDEX ... REBUILD per ricompilare una partizione specifica.  
  
### <a name="rebuild-process"></a>Processo di ricompilazione  
 Per ricompilare un indice columnstore, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Acquisisce un blocco esclusivo sulla tabella o partizione durante la ricompilazione. I dati sono "offline" e non disponibili durante la ricompilazione, anche quando si usa `NOLOCK`, RCSI o SI.  
  
2.  Ricomprime tutti i dati nel columnstore. Durante la ricompilazione esistono due copie dell'indice columnstore. Al termine della ricompilazione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina l'indice columnstore originale.  
  
### <a name="recommendations-for-rebuilding-a-columnstore-index"></a>Suggerimenti per la ricompilazione di un indice columnstore  
 La ricompilazione di un indice columnstore è utile per rimuovere la frammentazione e spostare tutte le righe nel columnstore. Tenere presenti le seguenti indicazioni:  
  
1.  Ricompilare una partizione anziché l'intera tabella.  
    -   La ricompilazione di un'intera tabella richiede molto tempo se l'indice è esteso ed è necessario sufficiente spazio su disco per archiviare una copia aggiuntiva dell'indice durante la ricompilazione. In genere è necessario solo ricompilare la partizione utilizzata più di recente.  
    -   Per le tabelle partizionate, non è necessario ricompilare l'intero indice columnstore perché la frammentazione probabilmente avviene solo nelle partizioni modificate di recente. Le tabelle dei fatti e le tabelle delle dimensioni grandi vengono in genere partizionate per eseguire operazioni di backup e di gestione dei blocchi della tabella.  

2.  Ricompilare una partizione dopo onerose operazioni DML  
    -   La ricompilazione di una partizione deframmenta la partizione e riduce lo spazio su disco. La ricompilazione elimina dal columnstore tutte le righe contrassegnate per l'eliminazione e sposta tutti i rowgroup dal deltastore nel columnstore. Si noti che possono esistere più rowgroup nel deltastore e che ognuno include meno di un milione di righe.  
  
3.  Ricompilare una partizione dopo il caricamento dei dati.  
    -   In questo modo viene garantita l'archiviazione di tutti i dati nel columnstore. Quando i processi simultanei caricano ognuno meno di 100.000 righe nella stessa partizione contemporaneamente, si possono creare più deltastore nella partizione. La ricompilazione sposterà tutte le righe del deltastore nel columnstore.  

## <a name="automatic-index-and-statistics-management"></a>Gestione automatica dell'indice e delle statistiche

Sfruttare le soluzioni, ad esempio la [deframmentazione dell'indice adattativo](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag), per gestire automaticamente la deframmentazione dell'indice e gli aggiornamenti delle statistiche per uno o più database. Questa procedura sceglie automaticamente se ricompilare o riorganizzare un indice in base al relativo livello di frammentazione, tra gli altri parametri, e aggiornare le statistiche con una soglia lineare.

## <a name="see-also"></a>Vedere anche        
[Indici columnstore - Novità](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)    
[Prestazioni delle query per gli indici columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
[Introduzione a columnstore per l'analisi operativa in tempo reale](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
[Indici columnstore per il data warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
[Architettura degli indici columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)    
[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) (Deframmentazione dell'indice adattativo)    
  
  
