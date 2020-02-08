---
title: Riorganizzare e ricompilare gli indici | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd844947b93e17684643fe95b5c51335af81b473
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74249748"
---
# <a name="reorganize-and-rebuild-indexes"></a>Riorganizzare e ricompilare gli indici

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Questo articolo descrive come riorganizzare o ricompilare un indice frammentato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Tramite il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] la modifica degli indici viene eseguita automaticamente dopo ogni operazione di modifica, inserimento o eliminazione dei dati sottostanti. Nel tempo, queste modifiche possono provocare la frammentazione dell'indice nel database. La frammentazione si verifica quando negli indici sono presenti pagine in cui l'ordinamento logico, basato sul valore chiave, non corrisponde all'ordinamento fisico all'interno del file di dati. Gli indici con un alto grado di frammentazione possono essere causa del calo delle prestazioni delle query e rallentare l'applicazione, in particolare le operazioni di scansione.

È possibile porre rimedio alla frammentazione eseguendo la riorganizzazione o la ricompilazione dell'indice. Per gli indici partizionati compilati in base a uno schema di partizione, è possibile usare uno dei metodi seguenti su un intero indice o su una singola partizione:

- La **riorganizzazione di un indice** richiede una quantità minima di risorse di sistema ed è un'operazione online. Ciò significa che i blocchi di tabella a lungo termine non vengono mantenuti attivi e le query o gli aggiornamenti inerenti la tabella sottostante possono continuare durante la transazione `ALTER INDEX REORGANIZE`.
  - Per gli indici **rowstore**, questa operazione deframmenta il livello foglia di indici cluster e non cluster di tabelle e viste tramite il riordinamento fisico delle pagine al livello foglia in base all'ordine logico (da sinistra verso destra) dei nodi foglia. La riorganizzazione consente inoltre di compattare le pagine di indice in base al valore del fattore di riempimento esistente. Per visualizzare l'impostazione del fattore di riempimento, usare [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).
  - Quando si usano gli indici **columnstore**, è possibile che dopo il caricamento dei dati l'archivio differenziale includa più rowgroup di piccole dimensioni. La riorganizzazione dell'indice columnstore consiste nel forzare l'inserimento di tutti i rowgroup nel columnstore e quindi combinarli generando un numero minore di rowgroup con più righe. L'operazione di riorganizzazione rimuoverà anche le righe che sono state eliminate dal columnstore. La riorganizzazione inizialmente richiede risorse di CPU aggiuntive per comprimere i dati, il che potrebbe globalmente ridurre le prestazioni del sistema. Tuttavia, non appena i dati sono compressi, le prestazioni delle query possono migliorare.

- La **ricompilazione di un indice** consiste nell'eliminare e creare nuovamente l'indice. A seconda del tipo di indice e della versione di [!INCLUDE[ssDE](../../includes/ssde-md.md)], questa operazione può essere eseguita online o offline.
  - Per gli indici **rowstore**, la ricompilazione ha l'effetto di rimuovere la frammentazione, rendere disponibile spazio su disco grazie alla compattazione delle pagine in base all'impostazione del fattore di riempimento esistente o specificata e riordinare le righe dell'indice in pagine contigue. Quando viene specificata la parola chiave `ALL`, tutti gli indici della tabella vengono eliminati e ricompilati in una singola transazione. Non è necessario eliminare in anticipo i vincoli di chiave esterna. Quando vengono ricompilati indici con un numero di extent pari o superiore a 128, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] posticipa le effettive deallocazioni delle pagine e i blocchi associati fino al termine del commit della transazione.
  - Per gli indici **columnstore**, la ricompilazione ha l'effetto di rimuovere la frammentazione, spostare tutte le righe nel columnstore e rendere disponibile spazio su disco eliminando fisicamente le righe che sono state eliminate logicamente dalla tabella. A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], la ricompilazione dell'indice columnstore in genere non è necessaria perché `REORGANIZE` esegue gran parte della ricompilazione in background come operazione online.

Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è talvolta possibile ricompilare un indice non cluster rowstore per risolvere le incoerenze causate da errori hardware.
A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], è ancora possibile correggere tali incoerenze tra l'indice e l'indice cluster tramite la ricompilazione di un indice non cluster offline. Non è possibile, tuttavia, correggere le incoerenze di indici non cluster tramite la ricompilazione dell'indice online, in quanto il meccanismo di ricompilazione online utilizza l'indice non cluster esistente come base per la ricompilazione e di conseguenza l'incoerenza persiste. La ricompilazione dell'indice offline può talvolta forzare l'analisi dell'indice cluster (o dell'heap) rimuovendo pertanto l'incoerenza. Per garantire una ricompilazione dall'indice cluster, eliminare e ricreare l'indice non cluster. Come nelle versioni precedenti, il metodo consigliato per il recupero in seguito all'individuazione di incoerenze consiste nel ripristino da backup dei dati interessati. È tuttavia possibile correggere le incoerenze dell'indice tramite la ricompilazione offline dell'indice non cluster. Per altre informazioni, vedere [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).

## <a name="Fragmentation"></a> Rilevamento della frammentazione

Il primo passaggio per decidere il metodo di deframmentazione da usare consiste nell'eseguire un'analisi dell'indice per determinare il grado di frammentazione.

### <a name="detecting-fragmentation-on-rowstore-indexes"></a>Rilevamento della frammentazione negli indici rowstore

La funzione di sistema [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)consente di rilevare la frammentazione in un indice specifico, in tutti gli indici di una tabella o vista indicizzata, in tutti gli indici di un database o in tutti gli indici di tutti i database. Per gli indici partizionati, **sys.dm_db_index_physical_stats** fornisce anche informazioni sulla frammentazione per ogni partizione.

Il set di risultati restituito dalla funzione **sys.dm_db_index_physical_stats** include le colonne seguenti:

|Colonna|Descrizione|
|------------|-----------------|
|**avg_fragmentation_in_percent**|Percentuale di frammentazione logica (pagine non ordinate nell'indice).|
|**fragment_count**|Numero di frammenti (pagine foglia fisicamente consecutive) nell'indice.|
|**avg_fragment_size_in_pages**|Numero medio di pagine in un frammento di un indice.|

Una volta noto il grado di frammentazione, usare la tabella seguente per determinare il metodo migliore per la correzione della frammentazione.

|Valore di**avg_fragmentation_in_percent**|Istruzione correttiva|
|-----------------------------------------------|--------------------------|
|> 5% e < = 30%|ALTER INDEX REORGANIZE|
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> È possibile eseguire la ricompilazione di un indice online oppure offline. La riorganizzazione di un indice viene sempre eseguita online. Per ottenere una disponibilità simile a quella offerta dall'opzione di riorganizzazione è necessario ricompilare gli indici in modalità online. Per altre informazioni, vedere [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).

> [!TIP]
> Questi valori costituiscono un'indicazione approssimativa per determinare il punto in cui passare da `ALTER INDEX REORGANIZE` a `ALTER INDEX REBUILD`. I valori effettivi, in realtà, variano da caso a caso. È importante riuscire a determinare la soglia migliore per l'ambiente in uso. Se ad esempio un determinato indice viene usato principalmente per le operazioni di analisi, la rimozione della frammentazione può migliorare le prestazioni di tali operazioni. Il vantaggio in termini di prestazioni è meno evidente per gli indici usati principalmente per le operazioni di ricerca. Analogamente, la rimozione della frammentazione in un heap (una tabella senza indici cluster) è particolarmente utile per le operazioni di analisi degli indici non cluster, ma ha un effetto ridotto nelle operazioni di ricerca.

Non è in genere consigliabile usare questi comandi per livelli di frammentazione ridotti (inferiori al 5%), poiché i vantaggi offerti dalla rimozione di una frammentazione così limitata sono praticamente annullati dal costo della riorganizzazione o della ricompilazione dell'indice. Per altre informazioni su `ALTER INDEX REORGANIZE` e `ALTER INDEX REBUILD`, vedere [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).

> [!NOTE]
> La ricompilazione o la riorganizzazione degli indici rowstore di dimensioni ridotte spesso non riduce la frammentazione. Le pagine di indici di dimensioni ridotte vengono talvolta archiviate in extent misti. Poiché gli extent misti possono essere condivisi al massimo da otto oggetti, la frammentazione in un indice di dimensioni ridotte potrebbe non ridursi dopo la riorganizzazione o la ricompilazione dell'indice.

### <a name="detecting-fragmentation-on-columnstore-indexes"></a>Rilevamento della frammentazione negli indici columnstore

Usando la DMV [sys.dm_db_column_store_row_group_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) è possibile determinare la percentuale di righe eliminate, ovvero una misura corretta per la frammentazione in un rowgroup. Usare queste informazioni per calcolare la frammentazione in un indice specifico, in tutti gli indici di una tabella, in tutti gli indici di un database o in tutti gli indici di tutti i database.

Il set di risultati restituito dalla DMV **sys.dm_db_column_store_row_group_physical_stats** include le colonne seguenti:

|Colonna|Descrizione|
|------------|-----------------|
|**total_rows**|Numero di righe archiviate fisicamente nel gruppo di righe. Per i gruppi di righe compressi, sono incluse le righe contrassegnate come eliminate.|
|**deleted_rows**|Numero di righe archiviate fisicamente in un gruppo di righe compresso contrassegnate per l'eliminazione. 0 per i gruppi di righe presenti nell'archivio differenziale.|

Questa operazione può essere usata per calcolare la frammentazione usando la formula `100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0)`. Una volta noto il grado di frammentazione, usare la tabella seguente per determinare il metodo migliore per la correzione della frammentazione.

|Valore di **computed fragmentation in percent**|Si applica alla versione|Istruzione correttiva|
|-----------------------------------------------|--------------------------|--------------------------|
|> = 20%|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|ALTER INDEX REBUILD|
|> = 20%|A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|ALTER INDEX REORGANIZE|

## <a name="index-defragmentation-considerations"></a>Considerazioni sulla deframmentazione dell'indice

In determinate condizioni, la ricompilazione di un indice cluster ricrea automaticamente tutti gli indici non cluster che fanno riferimento alla chiave di clustering, se è necessario modificare gli identificatori fisici o logici contenuti nei record degli indici non cluster.

Scenari che forzano la ricompilazione automatica di tutti gli indici rowstore non cluster in una tabella:

- Creazione di un indice cluster in una tabella
- Rimozione di un indice cluster, che causa l'archiviazione della tabella come heap
- Modifica della chiave di clustering per includere o escludere colonne

Scenari che non richiedono la ricompilazione automatica di tutti gli indici rowstore non cluster in una tabella:

- Ricompilazione di un indice cluster univoco
- Ricompilazione di un indice cluster non univoco
- Modifica dello schema dell'indice, ad esempio tramite l'applicazione di uno schema di partizionamento a un indice cluster o lo spostamento dell'indice cluster in un filegroup diverso

> [!IMPORTANT]
> Non è possibile riorganizzare o ricompilare indici contenuti in un filegroup offline o di sola lettura. Quando viene specificata la parola chiave ALL e uno o più indici si trovano in un filegroup offline o di sola lettura, l'istruzione ha esito negativo.
>
> Quando viene eseguita la ricompilazione di un indice, il supporto fisico deve disporre di spazio sufficiente per archiviare due copie dell'indice. Al termine della ricompilazione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina l'indice originale.

Quando viene specificato `ALL` con l'istruzione `ALTER INDEX`, vengono riorganizzati gli indici relazionali, sia cluster sia non cluster, e gli indici XML della tabella.

### <a name="considerations-specific-to-rebuilding-a-columnstore-index"></a>Considerazioni specifiche per la ricompilazione di un indice columnstore

Durante la ricompilazione di un indice columnstore, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] legge tutti i dati dell'indice columnstore originale, incluso l'archivio differenziale. Combina i dati in nuovi rowgroup e comprime i rowgroup nel columnstore. Il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] deframmenta il columnstore eliminando fisicamente le righe eliminate in modo logico dalla tabella. I byte eliminati vengono recuperati sul disco.

Ricompilare una partizione in alternativa all'intera tabella:

- La ricompilazione di un'intera tabella richiede molto tempo se l'indice è esteso ed è necessario sufficiente spazio su disco per archiviare una copia aggiuntiva dell'indice durante la ricompilazione. In genere è necessario solo ricompilare la partizione utilizzata più di recente.
- Per le tabelle partizionate, non è necessario ricompilare l'intero indice columnstore perché la frammentazione probabilmente avviene solo nelle partizioni modificate di recente. Le tabelle dei fatti e le tabelle delle dimensioni grandi vengono in genere partizionate per eseguire operazioni di backup e di gestione dei blocchi della tabella.

Ricompilare una partizione dopo onerose operazioni DML:

- La ricompilazione di una partizione deframmenta la partizione e riduce lo spazio su disco. La ricompilazione elimina dal columnstore tutte le righe contrassegnate per l'eliminazione e sposta tutti i rowgroup dall'archivio differenziale nel columnstore. Si noti che nell'archivio differenziale possono esistere più rowgroup e che ognuno include meno di un milione di righe.

Ricompilare una partizione dopo il caricamento dei dati:

- In questo modo viene garantita l'archiviazione di tutti i dati nel columnstore. Quando i processi simultanei caricano ognuno meno di 100.000 righe contemporaneamente nella stessa partizione, nella partizione possono essere creati più archivi differenziali. La ricompilazione sposterà tutte le righe dell'archivio differenziale nel columnstore.

### <a name="considerations-specific-to-reorganizing-a-columnstore-index"></a>Considerazioni specifiche per la riorganizzazione di un indice columnstore

Durante la riorganizzazione di un indice columnstore, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] comprime tutti i rowgroup differenziali CLOSED nel columnstore come rowgroup compresso. A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e nel [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], il comando `REORGANIZE` esegue online le ottimizzazioni di deframmentazione aggiuntive seguenti:

- Rimuove fisicamente le righe da un rowgroup quando più del 10% delle righe è stato eliminato in modo logico. I byte eliminati vengono recuperati sui supporti fisici. Ad esempio, se in un rowgroup compresso di 1 milione di righe 100.000 righe sono state eliminate, SQL Server rimuoverà le righe eliminate e ricomprimerà il rowgroup con 900.000 righe. Esegue il salvataggio nell'archiviazione rimuovendo le righe eliminate.

- Combina uno o più rowgroup compressi per aumentare le righe in ogni rowgroup, fino a un massimo di 1.024.576 righe. Ad esempio, se si importano globalmente 5 batch di 102.400 righe si otterranno 5 rowgroup compressi. Se si esegue l'operazione REORGANIZE, questi rowgroup verranno uniti in un rowgroup compresso di 512.000 righe. Si presuppone che non vi siano limiti di memoria o di dimensioni del dizionario.
- Per i rowgroup in cui almeno il 10% delle righe è stato eliminato in modo logico, il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tenterà di combinare questo rowgroup con uno o più rowgroup. Ad esempio, il rowgroup 1 viene compresso con 500.000 righe e il rowgroup 21 viene compresso con il numero massimo di 1.048.576 righe. Nel rowgroup 21 il 60% delle righe è stato eliminato in modo da lasciare 409.830 righe. Il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] consente di combinare questi due rowgroup per comprimere un nuovo rowgroup con 909.830 righe.

Dopo l'esecuzione di carichi di dati, è possibile che nell'archivio differenziale rimangano più rowgroup di piccole dimensioni. È possibile usare `ALTER INDEX REORGANIZE` per forzare l'inserimento di tutti i rowgroup in columnstore e poi combinare i rowgroup in un numero inferiore di rowgroup con più righe. L'operazione di riorganizzazione rimuoverà anche le righe che sono state eliminate dal columnstore.

## <a name="Restrictions"></a> Limitazioni e restrizioni

Gli indici rowstore con più di 128 extent vengono ricompilati in due fasi separate, logica e fisica. Nella fase logica, le unità di allocazione esistenti usate dall'indice vengono contrassegnate per la deallocazione, le righe di dati vengono copiate e ordinate, quindi spostate nelle nuove unità di allocazione create per archiviare l'indice ricompilato. Nella fase fisica, le unità di allocazione precedentemente contrassegnate per la deallocazione vengono fisicamente eliminate nelle transazioni brevi eseguite in background e non richiedono molti blocchi. Per altre informazioni sugli extent, vedere la [Guida all'architettura di pagine ed extent](../../relational-databases/pages-and-extents-architecture-guide.md).

L'istruzione `ALTER INDEX REORGANIZE` richiede che nel file di dati che include l'indice sia disponibile spazio, perché l'operazione può allocare solo pagine di lavoro temporanee nello stesso file, non in un altro file nel filegroup. Anche se nel filegroup possono essere disponibili pagine libere, è tuttavia possibile che l'utente incontri l'errore 1105: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

> [!WARNING]
> La creazione e la ricompilazione di indici non allineati per una tabella con oltre 1.000 partizioni sono possibili, ma non supportate. Questo tipo di operazioni può causare riduzioni delle prestazioni e un eccessivo consumo della memoria. Quando il numero di partizioni supera 1000, Microsoft consiglia di usare solo indici allineati.

Non è possibile riorganizzare o ricompilare indici contenuti in un filegroup **offline** o **di sola lettura**. Quando viene specificata la parola chiave `ALL` e uno o più indici si trovano in un filegroup offline o di sola lettura, l'istruzione ha esito negativo.

Quando un indice viene **creato** o **ricompilato** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le statistiche vengono create o aggiornate analizzando tutte le righe nella tabella. Tuttavia a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] le statistiche non vengono create o aggiornate analizzando tutte le righe nella tabella quando viene creato o ricompilato un indice partizionato. Query Optimizer usa invece l'algoritmo di campionamento predefinito per generare queste statistiche. Per ottenere statistiche sugli indici partizionati analizzando tutte le righe nella tabella, usare `CREATE STATISTICS` o `UPDATE STATISTICS` con la clausola `FULLSCAN`.

Quando un indice viene **riorganizzato** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le statistiche non vengono aggiornate.

Quando l'opzione `ALLOW_PAGE_LOCKS` è impostata su OFF, non è possibile eseguire operazioni di riorganizzazione degli indici.

Fino a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], la ricompilazione di un indice columnstore cluster è un'operazione offline. Il [!INCLUDE[ssde_md](../../includes/ssde_md.md)] deve acquisire un blocco esclusivo sulla tabella o sulla partizione durante la ricompilazione. I dati sono offline e non sono disponibili durante la ricompilazione, anche quando si usa `NOLOCK`, l'isolamento dello snapshot Read Committed (RCSI) o l'isolamento dello snapshot.
A partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], un indice columnstore cluster può essere ricompilato tramite l'opzione `ONLINE=ON`.

Per una tabella di Azure SQL Data Warehouse con un indice columnstore cluster ordinato, `ALTER INDEX REBUILD` riordina i dati usando TempDB. Monitorare TempDB durante le operazioni di ricompilazione. Se è necessario più spazio per TempDB, è possibile aumentare le dimensioni del data warehouse. Tornare alle dimensioni precedenti al termine della ricompilazione dell'indice.

Per una tabella di Azure SQL Data Warehouse con un indice columnstore cluster ordinato, `ALTER INDEX REORGANIZE` non riordina i dati. Per riordinare i dati, usare `ALTER INDEX REBUILD`.

## <a name="Security"></a> Sicurezza

### <a name="Permissions"></a> Autorizzazioni

È richiesta l'autorizzazione `ALTER` per la tabella o la vista. L'utente deve essere un membro di almeno uno dei ruoli seguenti:

- Ruolo del database **db_ddladmin**<sup>1</sup>
- Ruolo del database **db_owner**
- Ruolo del server **sysadmin**

<sup>1</sup>Il ruolo del database **db_ddladmin** è quello con i [minori privilegi](/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models).

## <a name="SSMSProcedureFrag"></a> Controllare la frammentazione dell'indice tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

> [!NOTE]
> [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] non può essere usato per calcolare la frammentazione degli indici columnstore in SQL Server e non può essere usato per calcolare la frammentazione di nessun indice nel database SQL di Azure. Usare l'esempio [!INCLUDE[tsql](../../includes/tsql-md.md)][seguente](#TsqlProcedureFrag).

1. In Esplora oggetti espandere il database contenente la tabella in cui si desidera controllare la frammentazione di un indice.
2. Espandere la cartella **Tabelle** .
3. Espandere la tabella in cui si desidera controllare la frammentazione di un indice.
4. Espandere la cartella **Indici** .
5. Fare clic con il pulsante destro del mouse sull'indice di cui si vuole controllare la frammentazione e scegliere **Proprietà**.
6. In **Selezione pagina**selezionare **Frammentazione**.

Le informazioni seguenti sono disponibili nella pagina **Frammentazione** :

|valore|Descrizione|
|---|---|
|**Livello di riempimento pagina**|Indica il livello medio di riempimento delle pagine di indice, espresso come percentuale. Il valore 100% indica che le pagine di indice sono completamente piene. Il valore 50% indica che ogni pagina di indice è piena all'incirca per metà.|
|**Frammentazione totale**|Percentuale di frammentazione logica. Indica il numero di pagine di un indice che non sono archiviate in ordine.|
|**Dimensioni medie delle righe**|Dimensioni medie di una riga al livello foglia.|
|**Livello nidificazione**|Numero di livelli dell'indice, compreso il livello foglia.|
|**Record inoltrati**|Numero di record in un heap che hanno inoltrato puntatori a un altro percorso dei dati. Questo stato si verifica durante un aggiornamento, nel caso in cui non vi sia spazio sufficiente per archiviare la riga nel percorso originale.|
|**Righe fantasma**|Numero di righe contrassegnate come eliminate ma non ancora rimosse. Queste righe verranno rimosse da un thread di pulitura nel momento in cui il server non è occupato. Questo valore non comprende le righe mantenute a causa di una transazione di isolamento dello snapshot in attesa.|
|**Tipo di indice**|Tipo di indice. I valori possibili sono **Indice cluster**, **Indice non cluster**e **XML primario**. È inoltre possibile archiviare le tabelle come heap (senza indici), ma in questo caso non sarà possibile aprire la pagina Proprietà indice.|
|**Righe al livello foglia**|Numero di righe al livello foglia.|
|**Dimensioni massime righe**|Dimensioni massime delle righe al livello foglia.|
|**Dimensioni minime righe**|Dimensioni minime delle righe al livello foglia.|
|**Pagine**|Numero totale di pagine di dati.|
|**ID partizione**|ID partizione dell'albero B contenente l'indice.|
|**Righe fantasma versione**|Numero di record fantasma mantenuti a causa di una transazione di isolamento dello snapshot in attesa.|

## <a name="TsqlProcedureFrag"></a> Controllare la frammentazione dell'indice tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]

### <a name="to-check-the-fragmentation-of-a-rowstore-index"></a>Per controllare la frammentazione di un indice rowstore

L'esempio seguente consente di trovare la percentuale di frammentazione media di tutti gli indici nella tabella `HumanResources.Employee` del database `AdventureWorks2016`.

```sql
SELECT a.object_id, object_name(a.object_id) AS TableName,
    a.index_id, name AS IndedxName, avg_fragmentation_in_percent
FROM sys.dm_db_index_physical_stats
    (DB_ID (N'AdventureWorks2016_EXT')
        , OBJECT_ID(N'HumanResources.Employee')
        , NULL
        , NULL
        , NULL) AS a
INNER JOIN sys.indexes AS b
    ON a.object_id = b.object_id
    AND a.index_id = b.index_id;
GO
```

L'istruzione precedente restituisce un set di risultati simile al seguente.

```
object_id   TableName    index_id    IndexName                                             avg_fragmentation_in_percent
----------- ------------ ----------- ----------------------------------------------------- ------------------------------
1557580587  Employee     1           PK_Employee_BusinessEntityID                          0
1557580587  Employee     2           IX_Employee_OrganizationalNode                        0
1557580587  Employee     3           IX_Employee_OrganizationalLevel_OrganizationalNode    0
1557580587  Employee     5           AK_Employee_LoginID                                   66.6666666666667
1557580587  Employee     6           AK_Employee_NationalIDNumber                          50
1557580587  Employee     7           AK_Employee_rowguid                                   0

(6 row(s) affected)
```

Per altre informazioni, vedere [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).

### <a name="to-check-the-fragmentation-of-a-columnstore-index"></a>Per controllare la frammentazione di un indice columnstore

L'esempio seguente consente di trovare la percentuale di frammentazione media di tutti gli indici nella tabella `dbo.FactResellerSalesXL_CCI` del database `AdventureWorksDW2016`.

```sql
SELECT i.object_id,
    object_name(i.object_id) AS TableName,
    i.index_id,
    i.name AS IndexName,
    100*(ISNULL(SUM(CSRowGroups.deleted_rows),0))/NULLIF(SUM(CSRowGroups.total_rows),0) AS 'Fragmentation'
FROM sys.indexes AS i  
INNER JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups
    ON i.object_id = CSRowGroups.object_id
    AND i.index_id = CSRowGroups.index_id
WHERE object_name(i.object_id) = 'FactResellerSalesXL_CCI'
GROUP BY i.object_id, i.index_id, i.name
ORDER BY object_name(i.object_id), i.name;
```

L'istruzione precedente restituisce un set di risultati simile al seguente.

```
object_id   TableName                   index_id    IndexName                       Fragmentation
----------- --------------------------- ----------- ------------------------------- ---------------
114099447   FactResellerSalesXL_CCI     1           IndFactResellerSalesXL_CCI      0

(1 row(s) affected)
```

## <a name="SSMSProcedureReorg"></a> Rimuovere la frammentazione tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

### <a name="to-reorganize-or-rebuild-an-index"></a>Per riorganizzare o ricompilare un indice

1. In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare un indice.
2. Espandere la cartella **Tabelle** .
3. Espandere la tabella in cui si desidera riorganizzare un indice.
4. Espandere la cartella **Indici** .
5. Fare clic con il pulsante destro del mouse sull'indice che si vuole riorganizzare e scegliere **Riorganizza**.
6. Nella finestra di dialogo **Riorganizza indici** verificare che nella griglia **Indici da riorganizzare** sia presente l'indice corretto, quindi scegliere **OK**.
7. Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.
8. Scegliere **OK.**

> [!NOTE]
> La riorganizzazione di un indice columnstore con [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] combina insieme i rowgroup `COMPRESSED`, ma non forza la compressione di tutti i rowgroup nel columnstore. Il rowgroup CLOSED verranno compressi, mentre i rowgroup OPEN non verranno compressi nel columnstore. Per comprimere tutti i rowgroup, usare l'esempio [!INCLUDE[tsql](../../includes/tsql-md.md)][seguente](#TsqlProcedureReorg).

### <a name="to-reorganize-all-indexes-in-a-table"></a>Per riorganizzare tutti gli indici in una tabella

1. In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare gli indici.
2. Espandere la cartella **Tabelle** .
3. Espandere la tabella in cui si desidera riorganizzare gli indici.
4. Fare clic con il pulsante destro del mouse sulla cartella **Indici** e scegliere **Riorganizza tutto**.
5. Nella finestra di dialogo **Riorganizza indici** verificare che nella griglia **Indici da riorganizzare**siano presenti gli indici corretti. Per rimuovere un indice dalla griglia **Indici da riorganizzare** , selezionare l'indice desiderato e premere CANC.
6. Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.
7. Scegliere **OK.**

### <a name="to-rebuild-an-index"></a>Per ricompilare un indice

1. In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare un indice.
2. Espandere la cartella **Tabelle** .
3. Espandere la tabella in cui si desidera riorganizzare un indice.
4. Espandere la cartella **Indici** .
5. Fare clic con il pulsante destro del mouse sull'indice che si vuole riorganizzare e scegliere **Ricompila**.
6. Nella finestra di dialogo **Ricompila indici** verificare che nella griglia **Indici da ricompilare** sia presente l'indice corretto, quindi scegliere **OK**.
7. Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.
8. Scegliere **OK.**

## <a name="TsqlProcedureReorg"></a> Rimuovere la frammentazione tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]

> [!NOTE]
> Per altri esempi sull'uso di [!INCLUDE[tsql](../../includes/tsql-md.md)] per la ricompilazione o la riorganizzazione degli indici, vedere [Esempi di ALTER INDEX: Indici columnstore](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes) ed [Esempi di ALTER INDEX: Indici rowstore](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes).

### <a name="to-reorganize-a-fragmented-index"></a>Per riorganizzare un indice frammentato

L'esempio seguente riorganizza l'indice `IX_Employee_OrganizationalLevel_OrganizationalNode` nella tabella `HumanResources.Employee` del database `AdventureWorks2016`.

```sql
ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode
    ON HumanResources.Employee
    REORGANIZE;
```

L'esempio seguente riorganizza l'indice columnstore `IndFactResellerSalesXL_CCI` nella tabella `dbo.FactResellerSalesXL_CCI` del database `AdventureWorksDW2016`.

```sql
-- This command will force all CLOSED and OPEN rowgroups into the columnstore.
ALTER INDEX IndFactResellerSalesXL_CCI
    ON FactResellerSalesXL_CCI
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

### <a name="to-reorganize-all-indexes-in-a-table"></a>Per riorganizzare tutti gli indici in una tabella

L'esempio seguente riorganizza tutti gli indici della tabella `HumanResources.Employee` del database `AdventureWorks2016`.

```sql
ALTER INDEX ALL ON HumanResources.Employee
   REORGANIZE;
```

### <a name="to-rebuild-a-fragmented-index"></a>Per ricompilare un indice frammentato

Nell'esempio seguente viene ricompilato un singolo indice della tabella `Employee` nel database `AdventureWorks2016`.

[!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]

### <a name="to-rebuild-all-indexes-in-a-table"></a>Per ricompilare tutti gli indici in una tabella

L'esempio seguente ricompila tutti gli indici associati alla tabella nel database `AdventureWorks2016` tramite la parola chiave `ALL`. Vengono inoltre specificate tre opzioni.

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]

Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).

### <a name="automatic-index-and-statistics-management"></a>Gestione automatica dell'indice e delle statistiche

Sfruttare le soluzioni, ad esempio la [deframmentazione dell'indice adattativo](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag), per gestire automaticamente la deframmentazione dell'indice e gli aggiornamenti delle statistiche per uno o più database. Questa procedura sceglie automaticamente se ricompilare o riorganizzare un indice in base al relativo livello di frammentazione, tra gli altri parametri, e aggiornare le statistiche con una soglia lineare.

## <a name="see-also"></a>Vedere anche

- [Architettura e guida per la progettazione degli indici di SQL Server](../../relational-databases/sql-server-index-design-guide.md)
- [Eseguire operazioni online sugli indici](../../relational-databases/indexes/perform-index-operations-online.md)
- [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
- [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) (Deframmentazione dell'indice adattativo)
- [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)
- [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
- [Prestazioni delle query per gli indici columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)
- [Introduzione a columnstore per l'analisi operativa in tempo reale](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)
- [Indici columnstore per il data warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)
- [Indici columnstore e criteri di unione per rowgroup](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)
