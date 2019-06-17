---
title: Determinazione del numero di Bucket corretto per gli indici Hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b79c0908f8639df869d01a8ff862afc5be77cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754243"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>Determinazione del numero di bucket corretto per gli indici hash
  È necessario specificare un valore per il parametro `BUCKET_COUNT` durante la creazione della tabella ottimizzata per la memoria. In questo argomento vengono fornite indicazioni per determinare il valore appropriato per il parametro `BUCKET_COUNT`. Se non è possibile determinare il numero di bucket corretto, utilizzare in alternativa un indice non cluster.  Un valore `BUCKET_COUNT` errato, in particolare se troppo basso, può influire in modo significativo sulle prestazioni del carico di lavoro e sul tempo di recupero del database. È consigliabile sovrastimare il numero di bucket.  
  
 Le chiavi duplicate dell'indice possono ridurre le prestazioni con un indice hash perché viene eseguito l'hash delle chiavi nello stesso bucket, causando un aumento della catena del bucket.  
  
 Per ulteriori informazioni sugli indici hash non cluster, vedere [Hash Indexes](hash-indexes.md) e [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Una tabella hash viene allocata per ogni indice hash in una tabella ottimizzata per la memoria. Le dimensioni della tabella hash allocata per un indice viene specificato per il `BUCKET_COUNT` parametro nel [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) o [CREATE TYPE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql). Il numero di bucket verrà arrotondato internamente per eccesso alla potenza più vicina di due. Se, ad esempio, si specifica un numero di bucket pari a 300.000 si avrà un numero di bucket effettivo pari a 524.288.  
  
 Per i collegamenti a un articolo e a un video sul numero di bucket, vedere [Come determinare 'esatto numero di bucket per gli indici hash (OLTP in memoria)](https://www.mssqltips.com/sqlservertip/3104/determine-bucketcount-for-hash-indexes-for-sql-server-memory-optimized-tables/).  
  
## <a name="recommendations"></a>Indicazioni  
 Nella maggior parte dei casi, il numero di bucket dovrebbe essere impostato su un valore compreso tra una e due volte il numero di valori distinct nella chiave di indice. Se la chiave di indice contiene molti valori duplicati (in media sono presenti più di 10 righe per ogni valore di chiave di indice), utilizzare in alternativa un indice non cluster.  
  
 Non è sempre possibile stimare quanti valori ha o potrebbe avere una particolare chiave di indice. Le prestazioni dovrebbero essere accettabili se il valore `BUCKET_COUNT` non supera di 5 volte il numero effettivo dei valori di chiave.  
  
 Per determinare il numero delle chiavi di indice univoche nei dati esistenti, utilizzare query simili agli esempi seguenti:  
  
### <a name="primary-key-and-unique-indexes"></a>Chiave primaria e indici univoci  
 Poiché l'indice di chiave primaria è univoco, il numero di valori distinct nella chiave corrisponde al numero di righe nella tabella. Per un esempio di chiave primaria in (SalesOrderID, SalesOrderDetailID) nella tabella Sales.SalesOrderDetail del database AdventureWorks, eseguire la query seguente per calcolare il numero di valori di chiave primaria distinct, che corrisponde al numero di righe nella tabella:  
  
```sql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 La query indica un numero di righe pari a 121.317. Utilizzare un numero di bucket pari a 240.000 se il conteggio delle righe non cambia in modo significativo. Utilizzare un numero di bucket pari a 480.000 se si prevede che il numero di ordini di vendita nella tabella venga quadruplicato.  
  
### <a name="non-unique-indexes"></a>Indici non univoci  
 Per altri indici, ad esempio un indice a più colonne in (SpecialOfferID, ProductID), eseguire la query seguente per determinare il numero di valori di chiave di indice univoci:  
  
```sql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 Questa query restituisce un conteggio di chiavi di indice per (SpecialOfferID, ProductID) di 484, per indicare che deve essere utilizzato un indice non cluster anziché un indice hash non cluster.  
  
### <a name="determining-the-number-of-duplicates"></a>Determinazione del numero di duplicati  
 Per determinare il numero medio di valori duplicati per un valore di chiave di indice, dividere il numero totale delle righe per il numero di chiavi di indice univoche.  
  
 Per l'indice dell'esempio in (SpecialOfferID, ProductID), si ha il calcolo 121317/484 = 251. Ciò significa che la media dei valori di chiave di indice è pari 251 ed è pertanto consigliabile un indice non cluster.  
  
## <a name="troubleshooting-the-bucket-count"></a>Risoluzione dei problemi relativi al numero di bucket  
 Per risolvere i problemi di conteggio dei bucket nelle tabelle ottimizzate per la memoria, usare [DM db_xtp_hash_index_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql) per ottenere statistiche sui bucket vuoti e la lunghezza delle catene di righe. È possibile utilizzare la query seguente per ottenere statistiche su tutti gli indici hash nel database corrente. L'esecuzione della query può richiedere alcuni minuti se sono presenti tabelle di grandi dimensioni nel database.  
  
```sql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 I due indicatori principali dell'indice hash sono i seguenti:  
  
 *empty_bucket_percent*  
 *empty_bucket_percent* indica il numero di bucket vuoti nell'indice hash.  
  
 Se *empty_bucket_percent* è minore del 10%, il numero di bucket è probabilmente troppo basso. In teoria, il valore *empty_bucket_percent* dovrebbe essere pari al 33% o superiore. Se il numero di bucket corrisponde al numero di valori di chiave di indice, circa 1/3 dei bucket è vuoto, a causa della distribuzione hash.  
  
 *avg_chain_length*  
 *avg_chain_length* indica la lunghezza media delle catene di righe nel bucket di hash.  
  
 Se *avg_chain_length* è maggiore di 10 e *empty_bucket_percent* è maggiore del 10%, probabilmente sono presenti molti valori di chiave di indice duplicati ed è più adatto un indice non cluster. La lunghezza media ideale della catena è pari a 1.  
  
 Sulla lunghezza della catena influiscono due fattori:  
  
1.  Duplicati. Tutte le righe duplicate fanno parte della stessa catena nell'indice hash.  
  
2.  Viene eseguito il mapping di più valori allo stesso bucket. Più basso è il numero di bucket, maggiore sarà il numero di bucket con più valori a cui verrà eseguito il mapping.  
  
 Ad esempio, si considerino la tabella e lo script per inserire righe di esempio nella tabella riportati di seguito:  
  
```sql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 Lo script inserisce 262.144 righe nella tabella. Vengono inseriti valori univoci nell'indice di chiave primaria e in IX_OrderSequence. Vengono inseriti molti valori duplicati nell'indice IX_Status: lo script genera solo 8 valori distinct.  
  
 L'output della query per la risoluzione dei problemi di BUCKET_COUNT è il seguente:  
  
|nome indice|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 Si considerino i tre indici hash in questa tabella:  
  
-   IX_Status: 50 percento dei bucket è vuoto, condizione positiva. Tuttavia, la lunghezza media della catena è molto elevata (65.536). Ciò indica un numero alto di valori duplicati. Pertanto, l'utilizzo di un indice hash non cluster non è appropriato in questo caso. È più opportuno utilizzare in alternativa un indice non cluster.  
  
-   IX_OrderSequence: 0 percento dei bucket è vuoto, un valore troppo basso. Inoltre, la lunghezza media della catena è pari a 8. I valori di questo indice sono univoci e ciò implica che, in media, viene eseguito il mapping di 8 valori per ogni bucket. Il numero di bucket deve essere aumentato. Poiché la chiave di indice ha 262.144 valori univoci, il numero di bucket deve essere pari ad almeno 262.144. Se si prevede una crescita futura, il numero deve essere maggiore.  
  
-   Indice di chiave primaria (PK): 36% dei bucket è vuoto, condizione positiva. Inoltre, la lunghezza media della catena è pari a 1, un'altra condizione positiva. Non è necessario apportare alcuna modifica.  
  
 Per ulteriori informazioni sulla risoluzione dei problemi relativi agli indici hash ottimizzati per la memoria, vedere [Troubleshooting Common Performance Problems with Memory-Optimized Hash Indexes](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md).  
  
## <a name="detailed-considerations-for-further-optimization"></a>Considerazioni dettagliate per un'ulteriore ottimizzazione  
 In questa sezione vengono presentate altre considerazioni per l'ottimizzazione del numero di bucket.  
  
 Per ottenere prestazioni ottimali per gli indici hash, è opportuno bilanciare la quantità di memoria allocata alla tabella hash e il numero di valori distinct nella chiave di indice. Esiste inoltre un compromesso tra le prestazioni delle ricerche di punti e le scansioni di tabella:  
  
-   Più alto è il valore del numero di bucket, maggiore sarà il numero di bucket vuoti nell'indice. Ciò influisce sull'utilizzo della memoria (8 byte per bucket) e sulle prestazioni delle analisi di tabella, in quanto ogni bucket viene analizzato come parte di un'analisi di tabella.  
  
-   Più basso è il numero di bucket, più saranno i valori assegnati a un singolo bucket. Ciò riduce le prestazioni per le ricerche di punti e gli inserimenti, perché in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può essere necessario attraversare diversi valori in un singolo bucket per trovare il valore specificato nel predicato.  
  
 Se il numero di bucket è notevolmente inferiore al numero di chiavi di indice univoche, verrà eseguito il mapping di molti valori a ogni bucket. Ciò comporta una riduzione delle prestazioni della maggior parte delle operazioni DML, in particolare delle ricerche di punti (ricerca di singole chiavi di indice) e delle operazioni di inserimento. Ad esempio, si può avere un peggioramento delle prestazioni delle query SELECT e delle operazioni UPDATE e DELETE con predicati di uguaglianza corrispondenti alle colonne chiave di indice nella clausola WHERE. Un numero di bucket basso influisce anche sul tempo di recupero del database, in quanto gli indici vengono ricreati all'avvio del database.  
  
### <a name="duplicate-index-key-values"></a>Valori di chiave di indice duplicati  
 I valori duplicati possono aumentare l'impatto sulle prestazioni delle collisioni hash. Ciò non costituisce generalmente un problema se ogni chiave di indice dispone di un numero basso di duplicati. Può tuttavia costituire un problema se la discrepanza tra il numero di chiavi di indice univoche e il numero di righe delle tabelle aumenta molto.  
  
 Tutte le righe con la stessa chiave di indice saranno nella stessa catena duplicata. Se più chiavi di indice si trovano nello stesso bucket a causa di una collisione hash, gli scanner dell'indice devono sempre analizzare l'intera catena di duplicati per trovare il primo valore prima di poter individuare la prima riga corrispondente al secondo valore. Le chiavi duplicate rendono inoltre più difficile l'individuazione della riga da parte di Garbage Collection. Ad esempio, se sono presenti 1.000 duplicati per una chiave e una delle righe viene eliminata, il Garbage Collector deve analizzare la catena di 1.000 duplicati per scollegare la riga dall'indice. Ciò vale anche se la query che ha individuato l'eliminazione ha utilizzato un indice più efficiente (un indice di chiave primaria) per individuare la riga, perché il Garbage Collector deve rimuovere il collegamento da ogni indice.  
  
 Per gli indici hash è possibile ridurre la quantità di operazioni rese necessarie dai valori di chiave di indice duplicati in due modi:  
  
-   Utilizzare in alternativa un indice non cluster. È possibile ridurre i duplicati aggiungendo colonne alla chiave di indice senza che sia necessario apportare alcuna modifica all'applicazione.  
  
-   Specificare un numero di bucket molto elevato per l'indice. Ad esempio, da 20 a 100 volte il numero di chiavi di indice univoche. In questo modo si riducono le collisioni hash.  
  
### <a name="small-tables"></a>Tabelle di piccole dimensioni  
 Per le tabelle più piccole, l'utilizzo della memoria non costituisce in genere un problema, perché le dimensioni dell'indice saranno ridotte rispetto alle dimensioni complessive del database.  
  
 È necessario operare una scelta in base al tipo di prestazioni desiderate:  
  
-   Se le operazioni critiche per le prestazioni nell'indice sono principalmente le ricerche di punti e/o le operazioni di inserimento, un numero di bucket elevato è più adatto per ridurre la probabilità di collisioni hash. La scelta ottimale sarà un valore pari a tre o più volte il numero di righe.  
  
-   Se le scansioni complete dell'indice sono le operazioni critiche per le prestazioni più frequenti, utilizzare un numero di bucket simile al numero effettivo dei valori di chiave di indice.  
  
### <a name="big-tables"></a>Tabelle di grandi dimensioni  
 Per le tabelle di grandi dimensioni, l'utilizzo della memoria può costituire un problema. Ad esempio, con una tabella di 250 milioni di righe che include 4 indici hash, ciascuno con un numero di bucket di un miliardo, l'overhead per le tabelle hash è di 4 indici * 1 miliardo bucket \* 8 byte = 32 GB di utilizzo della memoria. Quando si sceglie un numero di bucket di 250 milioni per ciascun indice, l'overhead totale per le tabelle hash sarà di 8 GB. Si noti che questo è oltre agli 8 byte dell'utilizzo della memoria a ogni indice aggiunge a ogni singola riga, pari a 8 GB in questo scenario (4 indici \* 8 byte \* 250 milioni di righe).  
  
 Le scansioni complete delle tabelle non fanno in genere parte del percorso critico per le prestazioni per i carichi di lavoro OLTP. Pertanto, occorre scegliere tra l'utilizzo della memoria e le prestazioni della operazioni di ricerca di punti e di inserimento:  
  
-   Se l'utilizzo della memoria rappresenta un problema, scegliere un numero di bucket simile al numero dei valori di chiave di indice. Il numero di bucket non deve essere notevolmente inferiore al numero di valori di chiave di indice, in quanto ciò influisce sulla maggior parte delle operazioni DML nonché sul tempo necessario per il recupero del database dopo il riavvio del server.  
  
-   Per ottimizzare le prestazioni per le ricerche di punti, è consigliabile un numero di bucket superiore di due o persino tre volte al numero di valori di indice univoci. Un numero di bucket più alto comporterebbe un aumento dell'utilizzo della memoria e del tempo richiesto per un'analisi completa dell'indice.  
  
## <a name="see-also"></a>Vedere anche  
 [Indici in tabelle con ottimizzazione per la memoria](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
