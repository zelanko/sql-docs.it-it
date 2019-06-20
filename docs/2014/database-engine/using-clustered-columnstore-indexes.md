---
title: Utilizzo di indici Columnstore cluster | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e65c3e277eb9a3e5e3703525b9c1ac06b423c96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773739"
---
# <a name="using-clustered-columnstore-indexes"></a>Utilizzo di indici columnstore cluster
  Attività per l'utilizzo di indici columnstore cluster in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Per una panoramica di indici columnstore, vedere [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Per informazioni sugli indici columnstore cluster, vedere [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Sommario  
  
-   [Creare un indice Columnstore cluster](#create)  
  
-   [Eliminare un indice Columnstore cluster](#drop)  
  
-   [Caricare i dati in un indice Columnstore cluster](#load)  
  
-   [Modificare i dati in un indice Columnstore cluster](#change)  
  
-   [Ricompilare un indice Columnstore cluster](#rebuild)  
  
-   [Riorganizzare un indice Columnstore cluster](#reorganize)  
  
##  <a name="create"></a> Creare un indice Columnstore cluster  
 Per creare un indice columnstore cluster, creare innanzitutto una tabella rowstore come heap o indice cluster e quindi usare il [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) istruzione per convertire la tabella in un cluster indice ColumnStore. Se si desidera che l'indice columnstore cluster abbia lo stesso nome dell'indice cluster, utilizzare l'opzione DROP_EXISTING.  
  
 In questo esempio viene creata una tabella come heap, che viene poi convertita in un indice columnstore cluster denominato cci_Simple. In questo modo viene modificata l'archiviazione dell'intera tabella da rowstore a columnstore.  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 Per altri esempi, vedere la sezione esempi in [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql).  
  
##  <a name="drop"></a> Eliminare un indice Columnstore cluster  
 Usare la [DROP INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql) istruzione per eliminare un indice columnstore cluster. Questa operazione consente di eliminare l'indice e convertire la tabella columnstore nell'heap di un rowstore.  
  
##  <a name="load"></a> Caricare i dati in un indice Columnstore cluster  
 È possibile aggiungere dati a un indice columnstore cluster esistente utilizzando uno dei metodi di caricamento standard.  Ad esempio, il caricamento bulk bcp degli strumenti, servizi di integrazione e INSERT... SELECT possono caricare i dati in un indice columnstore cluster.  
  
 Gli indici columnstore cluster utilizzano il deltastore per impedire la frammentazione dei segmenti di colonna nel columnstore.  
  
### <a name="loading-into-a-partitioned-table"></a>Caricamento in una tabella partizionata  
 Per i dati partizionati, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] assegna prima ogni riga a una partizione, quindi esegue operazioni columnstore sui dati nella partizione. Ogni partizione ha i propri rowgroup e almeno un deltastore.  
  
### <a name="deltastore-loading-scenarios"></a>Scenari di caricamento deltastore  
 Le righe vengono accumulate nel deltastore finché non viene raggiunto il numero di righe massimo consentito per un rowgroup. Quando il deltastore contiene il numero massimo di righe per rowgroup, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contrassegna il rowgroup come "CLOSED". Un processo in background, denominato "tuple-mover", individua il rowgroup CLOSED e passa al columnstore, in cui il rowgroup viene compresso in segmenti di colonna e i segmenti di colonna vengono archiviati nel columnstore.  
  
 Per ogni indice columnstore cluster possono essere presenti più deltastore.  
  
-   Se un deltastore è bloccato in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , si tenterà di ottenere un blocco su un deltastore diverso. Se non esistono deltastore disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , verrà creato un nuovo deltastore.  
  
-   Per una tabella partizionata, possono essere presenti uno o più deltastore per ogni partizione.  
  
 Solo per gli indici columnstore cluster, gli scenari seguenti indicano quando le righe caricate vengono direttamente indirizzate al columnstore o passano per il deltastore.  
  
 Nell'esempio, ogni rowgroup può avere 102.400-1.048.576 righe per rowgroup.  
  
|Righe per il caricamento bulk|Righe aggiunte al columnstore|Righe aggiunte al deltastore|  
|-----------------------|-----------------------------------|----------------------------------|  
|102.000|0|102.000|  
|145.000|145.000<br /><br /> Dimensioni rowgroup: 145.000|0|  
|1\.048.577|1,048,576<br /><br /> Dimensioni rowgroup: 1.048.576.|1|  
|2\.252.152|2\.252.152<br /><br /> Dimensioni rowgroup: 1.048.576, 1.048.576, 155.000.|0|  
  
 Nell'esempio seguente vengono illustrati i risultati del caricamento di 1.048.577 righe in una partizione. I risultati mostrano che esiste un rowgroup COMPRESSED nel columnstore (come segmenti di colonna compressi) e 1 riga nel deltastore.  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![Rowgroup e archivio differenziale per un carico batch](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup e archivio differenziale per un carico batch")  
  

  
##  <a name="change"></a> Modificare i dati in un indice Columnstore cluster  
 Gli indici columnstore cluster supportano le operazione DML di inserimento, aggiornamento ed eliminazione.  
  
 Uso [Inserisci &#40;Transact-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql) per inserire una riga. La riga viene aggiunta al deltastore.  
  
 Usare [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) per eliminare una riga.  
  
-   Se la riga è nel columnstore, viene contrassegnata in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] come eliminata logicamente, ma non viene reclamata l'archiviazione fisica della riga fino alla successiva ricompilazione dell'indice.  
  
-   Se la riga è nel deltastore, viene logicamente e fisicamente eliminata in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Usare [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) per aggiornare una ruga.  
  
-   Se la riga è nel columnstore, viene contrassegnata in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] come eliminata logicamente e la riga aggiornata viene inserita nel deltastore.  
  
-   Se la riga è nel deltastore, viene aggiornata nel deltastore in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="rebuild"></a> Ricompilare un indice Columnstore cluster  
 Uso [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) oppure [ALTER INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) per eseguire una ricompilazione completa di un indice columnstore cluster esistente. È anche possibile usare ALTER INDEX ... REBUILD per ricompilare una partizione specifica.  
  
### <a name="rebuild-process"></a>Processo di ricompilazione  
 Per ricompilare un indice columnstore cluster, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Acquisisce un blocco esclusivo sulla tabella o partizione durante la ricompilazione.  I dati sono "offline" e non disponibili durante la ricompilazione.  
  
-   Deframmenta il columnstore eliminando fisicamente le righe eliminate in modo logico dalla tabella; i byte eliminati vengono recuperati sui supporti fisici.  
  
-   Esegue l'unione dei dati del rowstore nel deltastore con i dati del columnstore prima che venga ricompilato l'indice. Al termine della ricompilazione, tutti i dati vengono archiviati nel formato columnstore e il deltastore è vuoto.  
  
-   Ricomprime tutti i dati nel columnstore. Durante la ricompilazione esistono due copie dell'indice columnstore. Al termine della ricompilazione, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] elimina l'indice columnstore originale.  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>Suggerimenti per la ricompilazione di un indice columnstore cluster  
 La ricompilazione di un indice columnstore cluster è utile per rimuovere la frammentazione e spostare tutte le righe nel columnstore. Tenere presenti le seguenti indicazioni:  
  
-   Ricompilare una partizione anziché l'intera tabella.  
  
    1.  La ricompilazione di un'intera tabella richiede molto tempo se l'indice è esteso ed è necessario sufficiente spazio su disco per archiviare una copia aggiuntiva dell'indice durante la ricompilazione. In genere è necessario solo ricompilare la partizione utilizzata più di recente.  
  
    2.  Per le tabelle partizionate, non è necessario ricompilare l'intero indice columnstore perché la frammentazione probabilmente avviene solo nelle partizioni modificate di recente. Le tabelle dei fatti e le tabelle delle dimensioni grandi vengono in genere partizionate per eseguire operazioni di backup e di gestione dei blocchi della tabella.  
  
-   Ricompilare una partizione dopo onerose operazioni DML  
  
     La ricompilazione di una partizione deframmenta la partizione e riduce lo spazio su disco. La ricompilazione elimina dal columnstore tutte le righe contrassegnate per l'eliminazione e sposta tutte le righe dal deltastore nel columnstore.  
  
-   Ricompilare una partizione dopo il caricamento dei dati.  
  
     In questo modo viene garantita l'archiviazione di tutti i dati nel columnstore. Se si verificano più caricamenti contemporaneamente, ogni partizione potrebbe avere più deltastore. La ricompilazione sposterà tutte le righe del deltastore nel columnstore.  
  
##  <a name="reorganize"></a> Riorganizzare un indice Columnstore cluster  
 La riorganizzazione di un indice columnstore cluster sposta tutti i rowgroup CLOSED nel columnstore. Per eseguire una riorganizzazione, utilizzare [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)con l'opzione REORGANIZE.  
  
 La riorganizzazione non è necessaria per spostare i rowgroup CLOSED nel columnstore. Tramite il processo tuple-mover verranno infine trovati e spostati tutti i rowgroup CLOSED. Tuple-mover è un processo a thread singolo e potrebbe non consentire uno spostamento sufficientemente rapido dei rowgroup per il carico di lavoro.  
  
### <a name="recommendations-for-reorganizing"></a>Suggerimenti per la riorganizzazione  
 Quando riorganizzare un indice columnstore cluster:  
  
-   Riorganizzare un indice columnstore cluster dopo uno o più caricamenti di dati per migliorare rapidamente le prestazioni delle query. La riorganizzazione inizialmente richiede risorse di CPU aggiuntive per comprimere i dati, il che potrebbe globalmente ridurre le prestazioni del sistema. Tuttavia, non appena i dati sono compressi, le prestazioni delle query possono migliorare.  
  
  
