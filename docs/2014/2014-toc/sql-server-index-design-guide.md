---
title: Guida per la progettazione di indici di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: b856ee9a-49e7-4fab-a88d-48a633fce269
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ee47da3e97240ec4573303700e9793ee482821c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62513042"
---
# <a name="sql-server-index-design-guide"></a>Guida per la progettazione di indici di SQL Server

  Gli indici progettati in modo non corretto e la mancanza di indici costituiscono le cause principali dei colli di bottiglia delle applicazioni di database. La progettazione di indici efficienti è fondamentale per ottenere buone prestazioni del database e dell'applicazione. In questa guida per la progettazione di indici di SQL Server sono contenute informazioni e procedure consigliate che consentono di progettare indici validi per soddisfare le esigenze dell'applicazione.  
  
**Si applica a**: [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] tramite [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] se non specificato diversamente.  
  
 In questa guida si presuppone che il lettore conosca i tipi di indice disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per una descrizione generale dei tipi di indice, vedere [Tipi di indice](../relational-databases/indexes/indexes.md).  
  
##  <a name="Top"></a> In questa Guida  

 [Nozioni fondamentali sulla progettazione di indici](#Basics)  
  
 [Linee guida generali per la progettazione dell'indice](#General_Design)  
  
 [Linee guida per la progettazione di indici cluster](#Clustered)  
  
 [Linee guida per la progettazione di indici non cluster](#Nonclustered)  
  
 [Linee guida per la progettazione di indici univoci](#Unique)  
  
 [Linee guida per la progettazione di indici filtrati](#Filtered)  
  
 [Informazioni aggiuntive](#Additional_Reading)  
  
##  <a name="Basics"></a> Nozioni fondamentali sulla progettazione di indici  

 Un indice è una struttura su disco associata a una tabella o a una vista che consente di recuperare in modo rapido le righe della tabella o della vista. L'indice contiene chiavi costituite da una o più colonne della tabella o della vista. Queste chiavi vengono archiviate in una struttura (albero B) che consente a SQL Server di individuare con rapidità ed efficienza la riga o le righe associate ai valori di chiave.  
  
 La selezione degli indici adatti a un database e al relativo carico di lavoro è un'operazione complessa che comporta la ricerca di un equilibrio tra velocità delle query e costi di aggiornamento. Gli indici limitati, ovvero con poche colonne nella chiave di indice, richiedono meno spazio su disco e overhead di gestione. Gli indici estesi, d'altra parte, coprono più query. Potrebbe essere necessario sperimentare diverse soluzioni prima di trovare l'indice più efficiente. È possibile aggiungere, modificare ed eliminare indici senza modificare lo schema del database o la struttura dell'applicazione. È pertanto opportuno sperimentare il funzionamento di vari tipi di indice.  
  
 Query Optimizer in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente di scegliere in modo affidabile l'indice più efficace nella maggior parte dei casi. La strategia globale di progettazione dell'indice deve offrire a Query Optimizer un'ampia gamma di indici tra cui scegliere e fare affidamento su questo strumento per la scelta. In questo modo, è possibile ridurre i tempi di analisi e garantire buone prestazioni in numerose situazioni. Per visualizzare gli indici usati da Query Optimizer per una query specifica, in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]scegliere **Includi piano di esecuzione effettivo** dal menu **Query**.  
  
 L'utilizzo di indici non consente necessariamente di ottenere prestazioni ottimali e prestazioni ottimali non sempre sono da mettere in relazione all'utilizzo di indici. Se l'utilizzo di un indice garantisse sempre le prestazioni migliori, il processo di Query Optimizer risulterebbe semplice. In realtà, una scelta non corretta di un indice può portare a prestazioni per niente ottimali. L'attività di Query Optimizer consiste pertanto nel selezionare un indice, o una combinazione di indici, solo quando questo comporta un miglioramento delle prestazioni e nell'evitare il recupero indicizzato quando ciò potrebbe avere conseguenze negative sulle prestazioni.  
  
### <a name="index-design-tasks"></a>Attività di progettazione di indici  

 Le attività seguenti costituiscono la strategia consigliata per la progettazione di indici:  
  
1.  Comprendere le caratteristiche del database. Stabilire, ad esempio, se si tratta di un database OLTP (Online Transaction Processing) in cui avvengono frequenti modifiche dei dati o di un database DSS (Decision Support System) o di data warehouse (OLAP) contenente principalmente dati di sola lettura e tramite cui è necessario elaborare rapidamente set di dati di grandi dimensioni. In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]l'indice *columnstore con ottimizzazione per la memoria di xVelocity* è particolarmente appropriato per set di dati di data warehousing tipici. Gli indici columnstore possono trasformare l'ambiente di data warehousing per gli utenti consentendo prestazioni più veloci per le query di data warehousing comuni quali quelle di filtro, aggregazione, raggruppamento e join a stella. Per altre informazioni, vedere [descrizione degli indici Columnstore](../relational-databases/indexes/columnstore-indexes-described.md).  
  
2.  Comprendere le caratteristiche delle query utilizzate più di frequente. Se, ad esempio, si stabilisce che una query utilizzata di frequente unisce in join due o più tabelle, è possibile determinare il tipo più adatto di indici da utilizzare.  
  
3.  Comprendere le caratteristiche delle colonne utilizzate nelle query. Un indice è ad esempio ideale per colonne con tipo di dati integer e univoche o non Null. Per colonne con subset di dati ben definiti, è possibile utilizzare un indice filtrato in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive. Per altre informazioni, vedere [Linee guida per la progettazione di indici filtrati](#Filtered) in questa guida.  
  
4.  Determinare quali opzioni dell'indice potrebbero migliorare le prestazioni in fase di creazione o manutenzione dell'indice. Per la creazione, ad esempio, di un indice cluster in una tabella esistente di grandi dimensioni può essere utile utilizzare l'opzione ONLINE. Tale opzione consente l'esecuzione di attività simultanee sui dati sottostanti durante la creazione o la ricompilazione dell'indice. Per altre informazioni vedere [Impostare le opzioni di indice](../relational-databases/indexes/set-index-options.md).  
  
5.  Determinare il percorso di archiviazione ottimale per l'indice. Un indice non cluster può essere archiviato nello stesso filegroup della tabella sottostante oppure in un filegroup diverso. Il percorso di archiviazione degli indici può consentire di migliorare le prestazioni di esecuzione delle query grazie a un aumento delle prestazioni di I/O su disco. L'archiviazione, ad esempio, di un indice non cluster in un filegroup in un disco diverso rispetto al filegroup della tabella può consentire di migliorare le prestazioni in quanto è possibile leggere più dischi contemporaneamente.  
  
     In alternativa, per gli indici cluster e non cluster è possibile utilizzare uno schema di partizione in più filegroup. Il partizionamento semplifica la gestione di tabelle o indici di grandi dimensioni in quanto consente di gestire o accedere a subset di dati in modo rapido ed efficace mantenendo l'integrità della raccolta. Per altre informazioni, vedere [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md). Quando si considera il partizionamento, determinare se è necessario che l'indice sia allineato, ovvero partizionato nello stesso modo della tabella, o partizionato in modo indipendente.  
  
##  <a name="General_Design"></a> Linee guida generali per la progettazione di indici  

 Gli amministratori di database esperti in genere sono in grado di progettare un set di indici adeguato, ma questa attività è molto complessa, richiede tempo ed è soggetta ad errori anche nel caso di database e carichi di lavoro di media complessità. Conoscere le caratteristiche del database, delle query e delle colonne di dati può aiutare a progettare indici ottimali.  
  
### <a name="database-considerations"></a>Considerazioni sui database  

 Quando si progetta un indice è consigliabile attenersi alle linee guida seguenti sui database:  
  
-   Un numero elevato di indici in una tabella ha ripercussioni sulle prestazioni delle istruzioni INSERT, UPDATE, DELETE e MERGE perché, quando vengono modificati i dati nella tabella, tutti gli indici devono essere modificati di conseguenza. Ad esempio, se una colonna viene utilizzata in molti indici e si esegue un'istruzione UPDATE tramite cui i dati della colonna vengono modificati, ogni indice contenente la colonna in questione deve essere aggiornato, nonché la colonna nella tabella di base sottostante (heap o indice cluster).  
  
    -   Evitare di creare un numero eccessivo di indici in tabelle che vengono aggiornate spesso e mantenere indici di piccole dimensioni, vale a dire con il minor numero possibile di colonne.  
  
    -   Utilizzare molti indici per migliorare le prestazioni delle query nelle tabelle che vengono aggiornate raramente ma che contengono grandi volumi di dati. Un numero elevato di indici può contribuire a migliorare le prestazioni delle query che non modificano i dati, ad esempio delle istruzioni SELECT, perché Query Optimizer può scegliere fra un numero maggiore di indici per determinare il metodo di accesso più rapido.  
  
-   L'indicizzazione di tabelle di piccole dimensioni può non risultare ottimale, perché Query Optimizer impiega più tempo per scorrere l'indice cercando i dati che per eseguire una semplice scansione della tabella. Pertanto, può accadere che gli indici delle tabelle di piccole dimensioni non vengano mai utilizzati, ma devono comunque essere gestiti in caso di modifica dei dati della tabella.  
  
-   Gli indici nelle viste possono garantire miglioramenti significativi delle prestazioni quando la vista contiene aggregazioni, join di tabella o una combinazione di aggregazioni e join. Non è necessario che venga fatto riferimento esplicito alla vista nella query affinché Query Optimizer la utilizzi.  
  
-   Utilizzare Ottimizzazione guidata motore di database per analizzare il database e raccogliere informazioni per gli indici. Per altre informazioni, vedere [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md).  
  
### <a name="query-considerations"></a>Considerazioni sulle query  

 Quando si progetta un indice è consigliabile attenersi alle linee guida seguenti sulle query:  
  
-   Creare indici non cluster nelle colonne che vengono utilizzate spesso in predicati e condizioni di join nelle query. Tuttavia, è consigliabile non aggiungere colonne non necessarie. L'aggiunta di un numero eccessivo di colonne di indice può avere effetti negativi sullo spazio su disco e sulle prestazioni per la gestione degli indici.  
  
-   Gli indici di copertura possono migliorare le prestazioni delle query, perché tutti i dati necessari per soddisfare i requisiti della query esistono all'interno dell'indice stesso. In altre parole, per recuperare i dati richiesti sono necessarie solo le pagine di indice, e non le pagine di dati della tabella o dell'indice cluster. Viene dunque ridotto l'I/O complessivo del disco. Una query di colonne **a** e **b** in una tabella con un indice composto creato nelle colonne **a**, **b**e **c** può recuperare i dati specificati dall'indice solo.  
  
-   Scrivere query che inseriscono o modificano il numero più alto possibile di righe con una sola istruzione, anziché utilizzare più query per aggiornare le stesse righe. L'utilizzo di una sola istruzione consente di avvalersi della gestione ottimizzata degli indici.  
  
-   Valutare il tipo di query e la modalità di utilizzo delle colonne nella query. Una colonna utilizzata in un tipo di query di corrispondenze esatte, ad esempio, potrebbe essere valida per un indice non cluster o cluster.  
  
### <a name="column-considerations"></a>Considerazioni sulle colonne  

 Quando si progetta un indice è consigliabile attenersi alle linee guidata seguenti:  
  
-   Mantenere corta la chiave dell'indice negli indici cluster. Inoltre, è consigliabile creare gli indici cluster su colonne univoche o non Null.  
  
-   Non è possibile specificare come colonne chiave indice le colonne di tipo `ntext`, `text`, `image`, `varchar(max)`, `nvarchar(max)` e `varbinary(max)`. Tuttavia, i tipi di dati `varchar(max)`, `nvarchar(max)`, `varbinary(max)` e `xml` possono partecipare a un indice non cluster come colonne non chiave dell'indice. Per altre informazioni, vedere la sezione " [Indice con colonne incluse](#Included_Columns)" in questa guida.  
  
-   Un tipo di dati `xml` può essere solo una colonna chiave solo in un indice XML. Per altre informazioni, vedere [Indici XML &#40;SQL Server&#41;](../relational-databases/xml/xml-indexes-sql-server.md). In SQL Server 2012 SP1 viene introdotto un nuovo tipo di indice XML noto come indice XML selettivo. Grazie al nuovo indice potranno essere migliorate le prestazioni di esecuzione delle query sui dati archiviati come XML in SQL Server, pertanto sarà possibile un'indicizzazione molto più rapida di carichi di lavoro di dati XML di grandi dimensioni, nonché un miglioramento della scalabilità riducendo i costi di archiviazione dell'indice stesso. Per altre informazioni vedere [Indici XML selettivi &#40;SXI&#41;](../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
-   Esaminare l'univocità delle colonne. Un indice univoco al posto di un indice non univoco nella stessa combinazione di colonne fornisce informazioni aggiuntive per Query Optimizer, che rendono l'indice più utile. Per altre informazioni, vedere [Linee guida per la progettazione di indici univoci](#Unique) in questa guida.  
  
-   Esaminare la distribuzione dei dati nelle colonne indicizzate. Spesso l'esecuzione prolungata di una query deriva dall'indicizzazione di una colonna con pochi valori univoci o dall'esecuzione di un join su tale colonna. Questo problema fondamentale relativo ai dati e alle query in genere non può essere risolto senza identificare questa situazione specifica. Ad esempio, in un elenco telefonico ordinato alfabeticamente in base al cognome non sarà possibile velocizzare la ricerca se i nomi di tutti gli abitanti della città sono Bianchi o Rossi. Per altre informazioni sulla distribuzione dei dati, vedere [Statistiche](../relational-databases/statistics/statistics.md).  
  
-   È consigliabile utilizzare indici filtrati su colonne dispongono di subset ben definiti, ad esempio colonne di tipo sparse, colonne con la maggior parte di valori Null, colonne con categorie di valori e colonne con intervalli di valori distinti. Un indice filtrato progettato correttamente consente di migliorare le prestazioni di esecuzione delle query e di ridurre i costi di archiviazione e di manutenzione dell'indice.  
  
-   Esaminare l'ordine delle colonne se l'indice conterrà più colonne. La colonna che viene utilizzata nella clausola WHERE in una condizione di ricerca uguale a (=), maggiore di (>), minore di (<) o BETWEEN oppure che partecipa a un join deve essere al primo posto. Le altre colonne devono essere ordinate in base alla presenza di valori distinct, vale a dire da quella con più valori distinct a quella con meno valori distinct.  
  
     Se, ad esempio, l'indice è definito come `LastName`, `FirstName` l'indice risulterà utile se il criterio di ricerca è `WHERE LastName = 'Smith'` o `WHERE LastName = Smith AND FirstName LIKE 'J%'`. Query Optimizer, tuttavia, non utilizzerebbe l'indice per una query che effettuasse la ricerca solo in base a `FirstName (WHERE FirstName = 'Jane')`.  
  
-   Valutare l'opportunità di indicizzare colonne calcolate. Per altre informazioni, vedere [Indici per le colonne calcolate](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="index-characteristics"></a>Caratteristiche degli indici  

 Dopo avere determinato che un indice è adeguato per una query, è possibile scegliere il tipo di indice più adatto a seconda della situazione. Le caratteristiche degli indici sono:  
  
-   Cluster e non cluster  
  
-   Univoci e non univoci  
  
-   A colonna singola e a più colonne  
  
-   In ordine crescente o decrescente per le colonne dell'indice  
  
-   Di tabella completa o filtrato per gli indici non cluster  
  
 È inoltre possibile personalizzare le caratteristiche iniziali dell'archiviazione dell'indice per ottimizzarne le prestazioni o la gestione impostando un'opzione quale FILLFACTOR. È inoltre possibile determinare la posizione di archiviazione dell'indice utilizzando filegroup o schemi di partizione per ottimizzare le prestazioni.  
  
###  <a name="Index_placement"></a> Posizione degli indici nei filegroup o negli schemi di partizioni  

 Durante lo sviluppo della strategia di progettazione degli indici, è opportuno considerare la posizione degli indici nei filegroup associati al database. Un'attenta selezione dello schema di filegroup o di partizione può contribuire a migliorare le prestazioni delle query.  
  
 Per impostazione predefinita, gli indici vengono archiviati nello stesso filegroup della tabella di base in cui viene creato l'indice. Un indice cluster non partizionato e la tabella di base sono sempre inclusi nello stesso filegroup. È tuttavia possibile eseguire una delle operazioni seguenti:  
  
-   Creare indici non cluster in un filegroup diverso dal filegroup della tabella di base o un indice cluster.  
  
-   Partizionare indici cluster e non cluster tra più filegroup.  
  
-   Spostare una tabella da un filegroup a un altro eliminando l'indice cluster e specificando un nuovo schema di filegroup o di partizione nella clausola MOVE TO dell'istruzione DROP INDEX oppure utilizzando l'istruzione CREATE INDEX con la clausola DROP_EXISTING.  
  
 La creazione dell'indice non cluster in un altro filegroup consente di migliorare le prestazioni se i filegroup utilizzano unità fisiche diverse con controller distinti. In tal caso, i dati e le informazioni degli indici possono essere letti in parallelo contemporaneamente da più testine. Ad esempio, se `Table_A` nel filegroup `f1` e `Index_A` nel filegroup `f2` vengono entrambi utilizzati dalla stessa query, è possibile che si riscontrino miglioramenti delle prestazioni, in quanto i filegroup vengono utilizzati integralmente senza contese. Se invece tramite la query viene eseguita l'analisi di `Table_A` ma non è presente un riferimento a `Index_A` , verrà utilizzato solo il filegroup `f1` . e non si otterrà un miglioramento delle prestazioni.  
  
 Non potendo prevedere il tipo di accesso e tantomeno il momento in cui questo si verifica, risulta più appropriato scegliere di suddividere le tabelle e gli indici tra tutti i filegroup. Poiché tutti i dati e gli indici sono suddivisi equamente in tutti i dischi, l'accesso riguarderà tutti i dischi, indipendentemente dalla modalità di accesso. Questo approccio è inoltre più semplice per gli amministratori del sistema.  
  
#### <a name="partitions-across-multiple-filegroups"></a>Partizioni tra più filegroup  

 È anche possibile scegliere di partizionare indici cluster e non cluster tra più filegroup. Gli indici vengono partizionati in orizzontale, ovvero per riga, in base a una funzione di partizione. Tale funzione definisce la modalità di mapping di ciascuna riga a un set di partizioni sulla base dei valori di colonne specifiche, dette colonne di partizionamento. Uno schema di partizione consente di specificare il mapping delle partizioni a un set di filegroup.  
  
 Il partizionamento di un indice può offrire i vantaggi seguenti:  
  
-   Fornire sistemi scalabili per una maggior gestibilità degli indici di grandi dimensioni. I sistemi OLTP, ad esempio, possono implementare applicazioni che riconoscono le partizioni e gestiscono correttamente gli indici di grandi dimensioni.  
  
-   Rendere più rapida ed efficace l'esecuzione delle query. Quando le query accedono a diverse partizioni di un indice, Query Optimizer è in grado di elaborare le singole partizioni contemporaneamente e di escludere quelle non interessate dalla query.  
  
 Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="Sort_Order"></a> Linee guida per la progettazione dell'ordinamento dell'indice  

 Quando si definiscono gli indici, è necessario valutare se la colonna chiave dell'indice deve essere archiviata in ordine crescente o decrescente. L'ordine crescente rappresenta l'impostazione predefinita e consente di garantire la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La sintassi delle istruzioni CREATE INDEX, CREATE TABLE e ALTER TABLE supporta le parole chiave ASC (ascending, crescente) e DESC (descending, decrescente) per singole colonne di indici e vincoli.  
  
 È utile specificare l'ordine di archiviazione dei valori chiave in un indice nel caso in cui le query che fanno riferimento alla tabella includono clausole ORDER BY che specificano direzioni diverse per la colonna o le colonne chiave nell'indice. In questi casi, l'indice non richiede un operatore SORT nel piano della query e pertanto la query risulta più efficiente. Gli acquirenti nel reparto acquisti di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] , ad esempio, devono valutare la qualità dei prodotti acquistati dai fornitori. Gli acquirenti sono più interessati a trovare i prodotti inviati dai fornitori con una percentuale di resi maggiore. Come illustrato nella query seguente, per recuperare i dati che soddisfano questo criterio è necessario che la colonna `RejectedQty` della tabella `Purchasing.PurchaseOrderDetail` sia disposta in ordine decrescente, ovvero dal valore più grande al più piccolo, e che la colonna `ProductID` sia disposta in ordine crescente, ovvero dal valore più piccolo al più grande.  
  
```sql
SELECT RejectedQty, ((RejectedQty/OrderQty)*100) AS RejectionRate,  
    ProductID, DueDate  
FROM Purchasing.PurchaseOrderDetail  
ORDER BY RejectedQty DESC, ProductID ASC;  
```  
  
 Il piano di esecuzione seguente per questa query mostra che in Query Optimizer viene utilizzato un operatore SORT per restituire il set di risultati nell'ordine specificato dalla clausola ORDER BY.  
  
 ![Piano di esecuzione indica un ordinamento viene utilizzato l'operatore. ](media/indexsort1.gif "Piano di esecuzione indica un ordinamento viene utilizzato l'operatore.")  
  
 Se un indice viene creato con colonne chiave che corrispondono a quelle della clausola ORDER BY nella query, è possibile eliminare l'operatore SORT nel piano della query, migliorando l'efficienza della query.  
  
```sql
CREATE NONCLUSTERED INDEX IX_PurchaseOrderDetail_RejectedQty  
ON Purchasing.PurchaseOrderDetail  
    (RejectedQty DESC, ProductID ASC, DueDate, OrderQty);  
```  
  
 Dopo che la query è stata eseguita di nuovo, il piano di esecuzione seguente mostra che l'operatore SORT è stato eliminato ed è stato utilizzato il nuovo indice non cluster creato.  
  
 ![Piano di esecuzione indica un ordinamento non viene usato](media/insertsort2.gif "piano di esecuzione indica un ordinamento non viene usato")  
  
 Il [!INCLUDE[ssDE](../includes/ssde-md.md)] consente di spostarsi con la stessa efficienza in entrambe le direzioni. Un indice definito come `(RejectedQty DESC, ProductID ASC)` può comunque essere utilizzato per una query in cui l'ordinamento delle colonne nella clausola ORDER BY viene invertito. L'indice può ad esempio essere utilizzato da una query con la clausola ORDER BY `ORDER BY RejectedQty ASC, ProductID DESC` .  
  
 È possibile specificare l'ordinamento solo per le colonne chiave. La vista del catalogo [sys.index_columns](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql) e la funzione INDEXKEY_PROPERTY indicano se una colonna di un indice è archiviata in ordine crescente o decrescente.  
  
 ![Icona freccia usata con il collegamento superiore](media/uparrow16x16.gif "icona freccia usata con il collegamento superiore") [In questa Guida](#Top)  
  
##  <a name="Clustered"></a> Linee guida per la progettazione di indici cluster  

 Gli indici cluster ordinano e archiviano le righe di dati della tabella in base ai valori di chiave. Per ogni tabella è disponibile un solo indice cluster poiché le righe di dati possono essere ordinate con un solo tipo di ordinamento. Con poche eccezioni, è opportuno definire un indice cluster sulla colonna o sulle colonne di tutte le tabelle che presentano le caratteristiche seguenti:  
  
-   Possono essere utilizzate per query frequenti.  
  
-   Garantiscono un elevato livello di univocità.  
  
    > [!NOTE]  
    >  Quando si crea un vincolo PRIMARY KEY, viene automaticamente creato un indice univoco sulla colonna o sulle colonne. Per impostazione predefinita, tale indice è cluster. È tuttavia possibile specificare un indice non cluster durante la creazione del vincolo.  
  
-   Possono essere utilizzate in query di intervallo.  
  
 Se l'indice cluster non viene creato con la proprietà UNIQUE, tramite il [!INCLUDE[ssDE](../includes/ssde-md.md)] viene aggiunta automaticamente una colonna uniqueifier a 4 byte alla tabella. Se necessario, tramite il [!INCLUDE[ssDE](../includes/ssde-md.md)] viene aggiunto automaticamente un valore uniqueifier a una riga per rendere univoca ciascuna chiave. Questa colonna e i relativi valori sono per uso interno e non sono visualizzati o accessibili dagli utenti.  
  
### <a name="clustered-index-architecture"></a>Architettura dell'indice cluster  

 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]gli indici sono organizzati in alberi B. Ogni pagina dell'albero B di un indice viene definita nodo. Il nodo di livello superiore dell'albero B viene definito nodo radice. I nodi inferiori dell'indice vengono definiti nodi foglia. I livelli dell'indice compresi tra il nodo radice e i nodi foglia sono noti come livelli intermedi. In un indice cluster il livello foglia include le pagine di dati della tabella sottostante. I nodi di livello radice e intermedio contengono pagine di indice che includono le righe dell'indice. Ogni riga di indice contiene un valore di chiave e un puntatore a una pagina di livello intermedio nell'albero B o a una riga di dati nel livello foglia dell'indice. Le pagine di ogni livello dell'indice sono collegate in un elenco collegato doppiamente.  
  
 Gli indici cluster includono una riga in [sys.partitions](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql), con **index_id** = 1 per ogni partizione usata dall'indice. Per impostazione predefinita, un indice cluster include una singola partizione. Quando in un indice cluster sono incluse più partizioni, ogni partizione ha un albero B contenente i dati per la partizione specifica. Se, ad esempio, un indice cluster include quattro partizioni, vi sono quattro alberi B, una in ogni partizione.  
  
 In base al tipo di dati nell'indice non cluster, ogni struttura dell'indice non cluster avrà una o più unità di allocazione in cui archiviare e gestire i dati per una partizione specifica. Ogni indice cluster conterrà almeno un'unità di allocazione IN_ROW_DATA per partizione e anche un'unità di allocazione LOB_DATA per partizione se contiene colonne LOB. Conterrà inoltre un'unità di allocazione ROW_OVERFLOW_DATA per partizione, se include colonne a lunghezza variabile che superano il limite della lunghezza di riga di 8.060.  
  
 Le pagine nella catena di dati e le righe incluse nelle pagine vengono ordinate in base al valore della chiave dell'indice cluster. Tutti gli inserimenti vengono eseguiti in corrispondenza del punto in cui il valore di chiave della riga inserita rientra nella sequenza di ordinamento tra righe esistenti.  
  
 Nella figura seguente viene illustrata la struttura di un indice cluster in una singola partizione.  
  
 ![I livelli di un indice cluster](media/bokind2.gif "livelli di un indice cluster")  
  
### <a name="query-considerations"></a>Considerazioni sulle query  

 Prima di creare indici cluster, è consigliabile conoscere la modalità di accesso ai dati. Utilizzare ad esempio un indice cluster per query che eseguono le operazioni seguenti:  
  
-   Restituiscono un intervallo di valori utilizzando operatori quali BETWEEN, >, >=, < e <=.  
  
     Quando la riga con il primo valore viene trovata utilizzando l'indice cluster, le righe con i valori indicizzati successivi sono sempre fisicamente adiacenti. Se, ad esempio, tramite una query vengono recuperati i record compresi tra un intervallo di numeri di ordini vendita, la presenza di un indice cluster nella colonna `SalesOrderNumber` consente di individuare rapidamente la riga contenente il numero iniziale dell'ordine di vendita e quindi di recuperare tutte le righe successive nella tabella fino al raggiungimento dell'ultimo numero dell'ordine vendita.  
  
-   Restituiscono set di risultati di grandi dimensioni.  
  
-   Utilizzano clausole JOIN, come nel caso delle colonne chiave esterne.  
  
-   Utilizzano clausole ORDER BY o GROUP BY.  
  
     L'utilizzo di un indice basato sulle colonne specificate nella clausola ORDER BY o GROUP BY consente di evitare operazioni di ordinamento dei dati in [!INCLUDE[ssDE](../includes/ssde-md.md)] perché le righe sono già ordinate e pertanto di ottimizzare le prestazioni delle query.  
  
### <a name="column-considerations"></a>Considerazioni sulle colonne  

 È in genere opportuno definire la chiave di indice cluster con il minor numero di colonne possibile. Utilizzare colonne che presentano o più degli attributi seguenti:  
  
-   Sono univoche o contengono molti valori distinti.  
  
     Gli ID dipendente consentono ad esempio di identificare in modo univoco i dipendenti. Un indice cluster o un vincolo PRIMARY KEY nella colonna `EmployeeID` contribuisce a migliorare le prestazioni di query tramite cui viene eseguita la ricerca di informazioni sui dipendenti in base al numero ID del dipendente. In alternativa, è possibile creare un indice cluster in `LastName`, `FirstName`, `MiddleName` perché i record relativi ai dipendenti sono in genere raggruppati e sottoposti a query in questo modo. Inoltre, la combinazione di queste colonne garantisce un elevato livello di differenziazione.  
  
-   Sono caratterizzate dall'accesso in modalità sequenziale.  
  
     Tramite un ID prodotto, ad esempio, vengono identificati in modo univoco i prodotti inclusi nella tabella `Production.Product` del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . La definizione di un indice cluster in `WHERE ProductID BETWEEN 980 and 999`produce effetti positivi sulle query in cui è stata specificata una ricerca sequenziale, come nel caso di `ProductID`, in quanto le righe vengono archiviate in base all'ordinamento definito per tale colonna chiave.  
  
-   Definite come IDENTITY.  
  
-   Vengono utilizzate di frequente per ordinare i dati recuperati da una tabella.  
  
     Può essere utile eseguire il clustering della tabella, ovvero ordinarla fisicamente, in base a tale colonna per evitare il costo di un'operazione di ordinamento ogni volta che si esegue la query sulla colonna.  
  
 Gli indici cluster non sono consigliati per gli attributi seguenti:  
  
-   Colonne che vengono modificate di frequente  
  
     Le modifiche frequenti determinano lo spostamento dell'intera riga in quanto [!INCLUDE[ssDE](../includes/ssde-md.md)] deve mantenere i valori dei dati nell'ordine fisico. Si tratta di una considerazione importante nel caso di sistemi che elaborano volumi elevati di transazioni in cui i dati sono in genere volatili.  
  
-   Chiavi estese  
  
     Le chiavi estese sono costituite da diverse colonne normali o di grandi dimensioni. I valori di chiave dell'indice cluster vengono utilizzati come chiavi di ricerca da tutti gli indici non cluster. Gli indici non cluster definiti nella stessa tabella saranno significativamente più grandi perché le voci di indice non cluster includono la chiave di clustering, nonché le colonne chiave definite per l'indice non cluster.  
  
 ![Icona freccia usata con il collegamento superiore](media/uparrow16x16.gif "icona freccia usata con il collegamento superiore") [In questa Guida](#Top)  
  
##  <a name="Nonclustered"></a> Linee guida per la progettazione di un indice non cluster  

 Un indice non cluster contiene i valori della chiave di indice e gli indicatori di posizione delle righe che puntano al percorso di archiviazione dei dati della tabella. In una vista tabella o indicizzata è possibile creare più indici non cluster. In genere, gli indici non cluster consentono di migliorare le prestazioni di query utilizzate di frequente non coperte da un indice cluster.  
  
 Analogamente a quando si utilizza l'indice di un libro, Query Optimizer cerca un valore di dati eseguendo una ricerca nell'indice non cluster per trovare la posizione del valore di dati nella tabella e quindi recupera i dati direttamente da quella posizione. Per questo motivo, gli indici non cluster sono la scelta ottimale per le query di corrispondenza esatta, in quanto l'indice contiene le voci che descrivono la posizione esatta nella tabella dei valori di dati cercati dalle query. Per eseguire, ad esempio, una query sulla tabella `HumanResources. Employee` per cercare tutti i dipendenti che fanno riferimento a un responsabile specifico, tramite Query Optimizer si potrebbe utilizzare l'indice non cluster `IX_Employee_ManagerID`, la cui colonna chiave è `ManagerID` . Query Optimizer consente di trovare in modo rapido tutte le voci di indice che corrispondono all'oggetto `ManagerID`specificato. Ogni voce di indice punta alla pagina e alla riga esatte nella tabella o all'indice cluster in cui è possibile trovare i dati corrispondenti. Dopo avere trovato tutte le voci nell'indice, Query Optimizer può passare direttamente alla pagina e alla riga esatte per recuperare i dati.  
  
### <a name="nonclustered-index-architecture"></a>Architettura dell'indice non cluster  

 Gli indici non cluster hanno lo stesso albero B degli indici cluster, con due differenze significative:  
  
-   Le righe di dati della tabella sottostante vengono archiviate con ordinamento basato sulle relative chiavi non cluster.  
  
-   Il livello foglia di un indice non cluster è composto da pagine di indice invece che da pagine di dati.  
  
 Gli indicatori di posizione delle righe nelle righe di indice non cluster sono rappresentati da un puntatore a una riga o da una chiave di indice cluster per una riga, come illustrato di seguito:  
  
-   Se la tabella è un heap, ovvero non include un indice cluster, l'indicatore di posizione è un puntatore riferito alla riga e compilato in base all'ID del file, al numero della pagina e al numero della riga nella pagina. L'intero puntatore è noto come ID di riga.  
  
-   Se una tabella include un indice cluster oppure l'indice è riferito a una vista indicizzata, l'indicatore di posizione delle righe corrisponde alla chiave di indice cluster per la riga.  
  
 Negli indici non cluster è inclusa una riga in [sys.partitions](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql) con **index_id** >1 per ogni partizione usata dall'indice. Per impostazione predefinita, un indice non cluster include una singola partizione. Quando in un indice non cluster sono incluse più partizioni, ogni partizione ha un albero B contenente le righe di indice per la partizione specifica. Se, ad esempio, un indice non cluster include quattro partizioni, vi sono quattro alberi B, una in ogni partizione.  
  
 In base ai tipi di dati nell'indice non cluster, ogni struttura dell'indice non cluster avrà una o più unità di allocazione in cui archiviare e gestire i dati per una partizione specifica. Ogni indice non cluster ha almeno un'unità di allocazione IN_ROW_DATA per partizione in cui sono archiviate le pagine relative all'albero B dell'indice. L'indice non cluster includerà inoltre un'unità di allocazione LOB_DATA per partizione se contiene colonne LOB. L'indice include inoltre un'unità di allocazione ROW_OVERFLOW_DATA per partizione se contiene colonne a lunghezza variabile che superano le dimensioni massime di 8.060 byte.  
  
 Nella figura seguente viene illustrata la struttura di un indice non cluster in una singola partizione.  
  
 ![Livelli di un indice nonclustered](media/bokind1.gif "livelli di un indice non cluster")  
  
### <a name="database-considerations"></a>Considerazioni sui database  

 Quando si progettano indici non cluster, considerare le caratteristiche del database.  
  
-   In caso di database o tabelle che richiedono pochi aggiornamenti ma contengono grandi volumi di dati, l'utilizzo di molti indici non cluster può consentire di migliorare le prestazioni di esecuzione delle query. È consigliabile creare indici filtrati per subset ben definiti di dati per ottimizzare le prestazioni relative alle query e ridurre i costi di archiviazione e di manutenzione dell'indice rispetto agli indici non cluster di tabella completa.  
  
     In caso di applicazioni DSS (Decision Support System) e database che contengono principalmente dati di sola lettura è consigliabile l'utilizzo di molti indici non cluster. In questo modo, saranno disponibili per Query Optimizer più indici tra cui scegliere per determinare il metodo di accesso più rapido e la bassa frequenza di aggiornamento del database significa che la manutenzione dell'indice non influirà negativamente sulle prestazioni.  
  
-   In caso di applicazioni di elaborazione delle transazioni online (OLP) e database contenenti tabelle aggiornate di frequente, è consigliabile evitare di utilizzare un numero eccessivo di indici. È inoltre necessario che gli indici siano limitati, ovvero con il minor numero possibile di colonne.  
  
     Un numero elevato di indici in una tabella ha ripercussioni sulle prestazioni delle istruzioni INSERT, UPDATE, DELETE e MERGE perché, quando vengono modificati i dati nella tabella, tutti gli indici devono essere modificati di conseguenza.  
  
### <a name="query-considerations"></a>Considerazioni sulle query  

 Prima di creare indici non cluster, è consigliabile analizzare la modalità di accesso ai dati. Utilizzare un indice non cluster per le query con gli attributi seguenti:  
  
-   Query che utilizzano clausole JOIN o GROUP BY.  
  
     Creare più indici non cluster in colonne interessate da operazioni di join e raggruppamento e un indice cluster in ogni colonna chiave esterna.  
  
-   Query che non restituiscono set di risultati estesi.  
  
     Creare indici filtrati per coprire query che restituiscono un subset ben definito di righe da una tabella di elevate dimensioni.  
  
-   Query che contengono colonne interessate di frequente da condizioni di ricerca di una query, ad esempio la clausola WHERE, che restituiscono corrispondenze esatte.  
  
### <a name="column-considerations"></a>Considerazioni sulle colonne  

 Considerare le colonne con uno o più degli attributi seguenti:  
  
-   Colonne che coprono la query.  
  
     È possibile ottenere un miglioramento delle prestazioni quando l'indice contiene tutte le colonne nella query. Query Optimizer può individuare tutti i valori della colonna all'interno dell'indice. Poiché non viene effettuato l'accesso ai dati della tabella o dell'indice cluster, il numero di operazioni di I/O su disco risulta inferiore. Utilizzare un indice con colonne per aggiungere colonne di copertura anziché creare una chiave di indice esteso.  
  
     Se la tabella include un indice cluster, la colonna o le colonne definite in tale indice vengono automaticamente accodate alla fine di ogni indice non cluster nella tabella. In questo modo, è possibile produrre una query coperta senza specificare le colonne dell'indice cluster nella definizione dell'indice non cluster. Se, ad esempio, in una tabella sono inclusi un indice cluster nella colonna `C`, un indice non cluster nelle colonne `B` e `A` , le colonne `B`, `A`e `C`della tabella in questione rappresenteranno i relativi valori chiave.  
  
-   Colonne che includono un numero elevato di valori distinct, ad esempio una combinazione di cognome e nome, se per le altre colonne viene utilizzato un indice cluster.  
  
     Se sono presenti soltanto pochi valori distinct, ad esempio 1 e 0, la maggior parte delle query non utilizzerà l'indice in quanto una scansione della tabella risulta in genere più efficiente. Per questo tipo di dati, creare un indice filtrato su un valore distinto che presente solo in un numero ridotto di righe. Se la maggior parte dei valori è impostata su 0, Query Optimizer potrebbe utilizzare un indice filtrato per le righe di dati che contengono il valore 1.  
  
####  <a name="Included_Columns"></a> Utilizzare colonne incluse per estendere gli indici non cluster  

 È possibile estendere le funzionalità degli indici non cluster aggiungendo colonne non chiave a livello foglia dell'indice non cluster. Con l'inclusione di colonne non chiave è possibile creare indici non cluster in grado di coprire più query. Ciò è possibile perché le colonne non chiave presentano i vantaggi seguenti:  
  
-   Possono essere tipi di dati che non sono consentiti come colonne chiave indice.  
  
-   Non vengono prese in esame dal [!INCLUDE[ssDE](../includes/ssde-md.md)] durante il calcolo del numero di colonne chiave indice o della dimensione delle chiavi di indice.  
  
 Un indice con colonne non chiave incluse può aumentare significativamente le prestazioni delle query quando tutte le colonne della query sono incluse nell'indice come colonne chiave o non chiave. I vantaggi nelle prestazioni si ottengono poiché in Query Optimizer è possibile individuare tutti i valori delle colonne all'interno dell'indice. In questo modo, la quantità di operazioni di I/O su disco è inferiore dato che non viene eseguito alcun accesso ai dati delle tabelle o degli indici cluster.  
  
> [!NOTE]  
>  Quando un indice contiene tutte le colonne a cui fa riferimento la query, viene generalmente indicato come indice di copertura.  
  
 Mentre le colonne chiave sono archiviate a tutti i livelli dell'indice, le colonne non chiave sono archiviate solo al livello foglia.  
  
##### <a name="using-included-columns-to-avoid-size-limits"></a>Utilizzo di colonne incluse per aggirare i limiti alle dimensioni  

 È possibile includere colonne non chiave in un indice non cluster per evitare il superamento delle limitazioni di dimensione correnti degli indici (numero massimo di colonne chiave pari a 16 e dimensione massima delle chiavi di indice pari a 900 byte). Il [!INCLUDE[ssDE](../includes/ssde-md.md)] non prende in esame le colonne non chiave durante il calcolo del numero di colonne chiave indice o della dimensione delle chiavi di indice.  
  
 Si supponga, ad esempio, che si desideri indicizzare le colonne seguenti nella tabella `Document` :  
  
 `Title nvarchar(50)`  
  
 `Revision nchar(5)`  
  
 `FileName nvarchar(400)`  
  
 Dal momento che i tipi i dati `nchar` e `nvarchar` richiedono 2 byte per ogni carattere, un indice contenente queste tre colonne supererebbe di 10 byte la limitazione di dimensione di 900 byte (455 \* 2). Utilizzando la clausola `INCLUDE` dell'istruzione `CREATE INDEX` , è possibile definire la chiave dell'indice come (`Title, Revision`) e `FileName` come colonna non chiave. In questo modo, la dimensione della chiave dell'indice sarebbe pari a 110 byte (55 \* 2) e l'indice conterrebbe ancora tutte le colonne necessarie. Nell'istruzione seguente viene creato un simile indice.  
  
```sql
CREATE INDEX IX_Document_Title   
ON Production.Document (Title, Revision)   
INCLUDE (FileName);   
```  
  
##### <a name="index-with-included-columns-guidelines"></a>Linee guida sull'utilizzo degli indici con colonne incluse  

 Quando si progettano indici non cluster con colonne incluse è opportuno considerare le indicazioni generali seguenti:  
  
-   Le colonne non chiave vengono definite nella clausola INCLUDE dell'istruzione CREATE INDEX.  
  
-   Le colonne non chiave possono essere definite solo su indici non cluster su tabelle o viste indicizzate.  
  
-   È possibile utilizzare qualsiasi tipo di dati, ad eccezione di `text`, `ntext` e `image`.  
  
-   Come colonne incluse è possibile utilizzare colonne calcolate che sono deterministiche, sia precise che imprecise. Per altre informazioni, vedere [Indici per le colonne calcolate](../relational-databases/indexes/indexes-on-computed-columns.md).  
  
-   In maniera simile alle colonne chiave, le colonne calcolate derivate dai tipi di dati `image`, `ntext` e `text` possono essere colonne non chiave (incluse) purché il tipo di dati della colonna calcolata sia consentito come colonna non chiave dell'indice.  
  
-   Non è possibile specificare i nomi delle colonne sia nell'elenco INCLUDE che nell'elenco delle colonne chiave.  
  
-   Non è possibile ripetere i nomi delle colonne nell'elenco INCLUDE.  
  
##### <a name="column-size-guidelines"></a>Linee guida sulle dimensioni delle colonne  
  
-   È necessario definire almeno una colonna chiave. Il numero massimo di colonne non chiave è 1023. Questo limite è rappresentato dal numero massimo di colonne nelle tabelle meno 1.  
  
-   Le colonne chiave non indice, escluse le colonne non chiave dell'indice, devono soddisfare le limitazioni di dimensione correnti degli indici (numero massimo di colonne chiave pari a 16 e dimensione totale delle chiavi di indice pari a 900 byte).  
  
-   La dimensione totale delle colonne non chiave è limitata solo dalle dimensioni delle colonne specificate nella clausola INCLUDE (ad esempio, le colonne `varchar(max)` sono limitate a 2 GB).  
  
##### <a name="column-modification-guidelines"></a>Linee guida sulla modifica delle colonne  

 Quando si modifica una colonna di tabella che è stata definita come colonna inclusa, vengono applicate le limitazioni seguenti:  
  
-   Non è possibile eliminare dalla tabella le colonne non chiave se non si è prima eliminato l'indice.  
  
-   Non è possibile modificare le colonne non chiave se non per effettuare le operazioni seguenti:  
  
    -   Modifica del supporto di valori NULL della colonna da NOT NULL a NULL.  
  
    -   Aumento della lunghezza di colonne `varchar`, `nvarchar` o `varbinary`.  
  
        > [!NOTE]  
        >  Tali restrizioni sulla modifica delle colonne sono valide anche per le colonne chiave indice.  
  
##### <a name="design-recommendations"></a>Consigli sulla progettazione  

 Progettare nuovamente gli indici non cluster con chiavi di indice dalle dimensioni elevate in modo da utilizzare come colonne chiave solo le colonne utilizzate per le ricerche. Modificare in colonne non chiave incluse tutte le altre colonne che coprono la query. In questo modo si avranno tutte le colonne necessarie per coprire la query, contenendo al tempo stesso le dimensioni della chiave dell'indice e mantenendone l'efficienza.  
  
 Si supponga, ad esempio, che si desideri progettare un indice per coprire la query seguente.  
  
```sql
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
```  
  
 Per coprire la query è necessario definire tutte le colonne nell'indice. Sebbene sia possibile definire tutte le colonne come colonne chiave, la dimensione delle chiavi sarebbe di 334 byte. Dal momento che la sola colonna effettivamente utilizzata come criterio di ricerca è la colonna `PostalCode` , la quale ha una lunghezza pari a 30 byte, è possibile migliorare la progettazione degli indici definendo `PostalCode` come colonna chiave e includendo tutte le altre colonne come colonne non chiave.  
  
 Nell'istruzione seguente viene creato un indice con colonne incluse per coprire la query.  
  
```sql
CREATE INDEX IX_Address_PostalCode  
ON Person.Address (PostalCode)  
INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
```  
  
##### <a name="performance-considerations"></a>Considerazioni sulle prestazioni  

 Evitare di aggiungere colonne non necessarie. L'aggiunta di troppe colonne indice, chiave o non chiave, può avere le implicazioni sulle prestazioni seguenti:  
  
-   In una pagina rientreranno meno righe di indice. Ciò potrebbe causare più operazioni di I/O e ridurre l'efficienza della cache.  
  
-   Sarà necessario più spazio su disco per archiviare l'indice. In particolare, l'aggiunta di tipi di dati `varchar(max)`, `nvarchar(max)`, `varbinary(max)` o `xml` come colonne non chiave dell'indice potrebbe aumentare significativamente lo spazio su disco richiesto. Ciò accade perché i valori delle colonne vengono copiati nel livello foglia dell'indice, risiedendo in tal modo sia nell'indice che nella tabella di base.  
  
-   La manutenzione degli indici può aumentare il tempo necessario per eseguire modifiche, inserimenti, aggiornamenti o eliminazioni nella tabella sottostante o nella vista indicizzata.  
  
 Sarà necessario determinare se i guadagni in termini di prestazioni delle query offrano maggiore vantaggio rispetto all'influenza sulle prestazioni durante la modifica dei dati e ai maggiori requisiti di spazio su disco.  
  
 ![Icona freccia usata con il collegamento superiore](media/uparrow16x16.gif "icona freccia usata con il collegamento superiore") [In questa Guida](#Top)  
  
##  <a name="Unique"></a> Linee guida per la progettazione di indici univoci  

 Un indice univoco consente di garantire che nella chiave dell'indice non siano contenuti valori duplicati e che pertanto ogni riga della tabella sia univoca. È consigliabile specificare un indice univoco solo se l'unicità è una caratteristica dei dati stessi. Per verificare, ad esempio, che i valori della colonna `NationalIDNumber` nella tabella `HumanResources.Employee` siano univoci quando la chiave primaria è `EmployeeID`, creare un vincolo UNIQUE nella colonna `NationalIDNumber` . Se l'utente tenta di inserire nella colonna lo stesso valore per più dipendenti, verrà visualizzato un messaggio di errore e il valore duplicato non verrà inserito.  
  
 Per gli indici univoci a più colonne, l'indice garantisce che ogni combinazione di valori nella chiave dell'indice sia univoca. Ad esempio, se si crea un indice univoco basato su una combinazione delle colonne `LastName`, `FirstName`e `MiddleName` , non è possibile che nella tabella siano incluse due righe in cui è presente la stessa combinazione di valori per queste colonne.  
  
 Sia gli indici cluster che non cluster possono essere univoci. Se i dati nella colonna sono univoci, nella stessa tabella è possibile creare sia un indice cluster univoco che più indici non cluster univoci.  
  
 Gli indici univoci offrono i vantaggi seguenti:  
  
-   Garantiscono l'integrità dei dati delle colonne definite.  
  
-   Forniscono informazioni aggiuntive utili per Query Optimizer.  
  
 Se si crea un vincolo PRIMARY KEY o UNIQUE, viene creato automaticamente un indice univoco basato sulle colonne specificate. Non esistono differenze significative tra la creazione determinata da un vincolo UNIQUE e la creazione di un indice univoco indipendente da un vincolo. La convalida dei dati viene eseguita nello stesso modo e Query Optimizer non differenzia un indice univoco creato da un vincolo da un indice creato in modo manuale. Se l'obiettivo è l'integrità dei dati, è tuttavia consigliabile creare un vincolo UNIQUE o PRIMARY KEY sulla colonna, in modo tale che l'obiettivo dell'indice risulti chiaro.  
  
### <a name="considerations"></a>Considerazioni  
  
-   Se nei dati sono presenti valori di chiave duplicati, non è possibile creare un indice univoco, un vincolo UNIQUE o un vincolo PRIMARY KEY.  
  
-   Se i dati sono univoci e si desidera imporre l'unicità, la creazione di un indice univoco anziché di un indice non univoco per la stessa combinazione di colonne fornirà a Query Optimizer una maggiore quantità di informazioni che consentiranno di creare piani di esecuzione più efficienti. In questo caso è consigliabile creare un indice univoco, preferibilmente tramite un vincolo UNIQUE.  
  
-   In un indice non cluster univoco possono essere contenute colonne non chiave. Per altre informazioni, vedere [Indice con colonne incluse](#Included_Columns).  
  
 ![Icona freccia usata con il collegamento superiore](media/uparrow16x16.gif "icona freccia usata con il collegamento superiore") [In questa Guida](#Top)  
  
##  <a name="Filtered"></a> Linee guida per la progettazione di indici filtrati  

 Un indice filtrato è un indice non cluster ottimizzato, particolarmente indicato per coprire query che selezionano dati da un subset ben definito. Un indice di questo tipo utilizza un predicato del filtro per indicizzare una parte di righe nella tabella. Se confrontato con indici di tabella completa, un indice filtrato progettato correttamente consente di migliorare le prestazioni di esecuzione delle query e di ridurre i costi di manutenzione e di archiviazione dell'indice stesso.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|  
  
 Rispetto agli indici di tabella completa, gli indici filtrati consentono di ottenere i vantaggi seguenti:  
  
-   **Prestazioni di esecuzione delle query e qualità del piano migliorate**  
  
     Un indice filtrato progettato correttamente migliora le prestazioni di esecuzione delle query e la qualità del piano di esecuzione poiché è caratterizzato da dimensioni minori rispetto a un indice non cluster di tabella completa e dispone di statistiche filtrate. Queste ultime sono più accurate delle statistiche di tabella completa poiché coprono solo le righe nell'indice filtrato.  
  
-   **Costi di manutenzione dell'indice ridotti**  
  
     La manutenzione di un indice viene eseguita solo quando le istruzioni DML (Data Manipulation Language) influiscono sui dati relativi all'indice. Un indice filtrato consente di ridurre i costi di manutenzione rispetto a un indice non cluster di tabella completa poiché è caratterizzato da dimensioni minori e viene gestito solo se i dati relativi sono interessati. È possibile disporre di un numero elevato di indici filtrati, soprattutto quando questi ultimi contengono dati interessati raramente. In modo analogo, se un indice filtrato contiene dati interessati di frequente, la dimensione minore dell'indice consente di ridurre il costo di aggiornamento delle statistiche.  
  
-   **Costi di archiviazione dell'indice ridotti**  
  
     La creazione di un indice filtrato può ridurre lo spazio di archiviazione su disco per gli indici non cluster nel caso in cui non sia necessario un indice di tabella completa. È possibile sostituire un indice non cluster di tabella completa con più indici filtrati senza aumentare in modo significativo i requisiti di archiviazione.  
  
 Gli indici filtrati risultano particolarmente utili quando le colonne contengono subset ben definiti di dati cui le query fanno riferimento nelle istruzioni SELECT. Di seguito vengono indicati alcuni esempi:  
  
-   Colonne di tipo sparse che contengono solo un numero limitato di valori non NULL.  
  
-   Colonne eterogenee che contengono categorie di dati.  
  
-   Colonne che contengono intervalli di valori diversi, ad esempio quantità di denaro, ore e date.  
  
-   Partizioni di tabelle definite da logica di confronto semplice per i valori di colonna.  
  
 I costi di manutenzione ridotti ottenuti dall'utilizzo di indici filtrati sono più apprezzabili quando il numero di righe dell'indice non è elevato rispetto a quello di un indice di tabella completa. Se l'indice filtrato include la maggior parte delle righe della tabella, è possibile che i costi di manutenzione siano maggiori rispetto a quelli relativi a un indice di tabella completa. In questo caso è opportuno utilizzare un indice di tabella completa anziché un indice filtrato.  
  
 Gli indici filtrati sono definiti in una tabella e supportano solo operatori di confronto semplici. Se è necessaria un'espressione di filtro in cui viene fatto riferimento a più tabelle o in cui è presente della logica complessa, è necessario creare una vista.  
  
### <a name="design-considerations"></a>Considerazioni sulla progettazione  

 Per progettare indici filtrati efficaci, è importante comprendere quali sono le query utilizzate dall'applicazione e il modo in cui sono correlate ai subset dei dati. Alcuni esempi di dati che dispongono di subset ben definiti sono costituiti da colonne con la maggior parte di valori NULL, colonne con categorie eterogenee di valori e colonne con intervalli di valori distinti. Nelle considerazioni sulla progettazione seguenti viene indicata una varietà di scenari in cui un indice filtrato può fornire vantaggi rispetto agli indici di tabella completa.  
  
#### <a name="filtered-indexes-for-subsets-of-data"></a>Indici filtrati per subset di dati  

 Quando una colonna dispone solo di un numero ridotto di valori rilevanti per le query, è possibile creare un indice filtrato sul subset di valori. Ad esempio, quando la maggior parte dei valori di una colonna è costituita da valori NULL e la query esegue la selezione solo dai valori non NULL, è possibile creare un indice filtrato per le righe di dati non NULL. L'indice risultante sarà minore e sarà possibile gestirlo con costi ridotti rispetto a un indice non cluster di tabella completa definito sulle stesse colonne chiave.  
  
 Nel database `AdventureWorks2012` , ad esempio, è disponibile una tabella `Production.BillOfMaterials` con 2679 righe. La colonna `EndDate` dispone solo di 199 righe che contengono un valore non NULL, mentre le altre 2480 righe contengono valori NULL. L'indice filtrato seguente coprirà query che restituiscono le colonne definite nell'indice e che selezionano solo righe con un valore non NULL per `EndDate`.  
  
```sql
CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL ;  
GO  
```  
  
 L'indice filtrato `FIBillOfMaterialsWithEndDate` è valido per la query seguente. È possibile visualizzare il piano di esecuzione della query per determinare se in Query Optimizer è stato utilizzato l'indice filtrato.  
  
```sql
SELECT ProductAssemblyID, ComponentID, StartDate   
FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL   
    AND ComponentID = 5   
    AND StartDate > '20080101' ;  
```  
  
 Per altre informazioni sulla creazione di indici filtrati e sulla definizione dell'espressione del predicato dell'indice filtrato, vedere [Creare indici filtrati](../relational-databases/indexes/create-filtered-indexes.md).  
  
#### <a name="filtered-indexes-for-heterogeneous-data"></a>Indici filtrati per dati eterogenei  

 Se in una tabella sono presenti righe di dati eterogenei, è possibile creare un indice filtrato per una o più categorie di dati.  
  
 Ogni prodotto elencato nella tabella `Production.Product` , ad esempio, è assegnato a un `ProductSubcategoryID`, associato a sua volta alle categorie di prodotti Bikes, Components, Clothing o Accessories. Queste categorie sono eterogenee poiché i valori di colonna relativi nella tabella `Production.Product` non sono strettamente correlati. Ad esempio, le colonne `Color`, `ReorderPoint`, `ListPrice`, `Weight`, `Class`e `Style` dispongono di caratteristiche univoche per ogni categoria di prodotti. Se vengono eseguite query frequenti sugli accessori con sottocategorie tra 27 e 36 inclusi, è possibile migliorarne le prestazioni creando un indice filtrato nella sottocategoria degli accessori come mostrato nell'esempio riportato di seguito.  
  
```sql
CREATE NONCLUSTERED INDEX FIProductAccessories  
    ON Production.Product (ProductSubcategoryID, ListPrice)   
        Include (Name)  
WHERE ProductSubcategoryID >= 27 AND ProductSubcategoryID <= 36;
```  
  
 L'indice filtrato `FIProductAccessories` si applica alla query seguente, in quanto i risultati  
  
 della query sono contenuti nell'indice e il piano della query non include una ricerca nella tabella di base. Ad esempio, l'espressione del predicato di query `ProductSubcategoryID = 33` è un subset del predicato dell'indice filtrato `ProductSubcategoryID >= 27` e `ProductSubcategoryID <= 36`, le colonne `ProductSubcategoryID` e `ListPrice` nel predicato di query sono entrambe colonne chiave nell'indice e il nome è archiviato al livello foglia dell'indice come colonna inclusa.  
  
```sql
SELECT Name, ProductSubcategoryID, ListPrice  
FROM Production.Product  
WHERE ProductSubcategoryID = 33 AND ListPrice > 25.00 ;  
```  
  
#### <a name="key-columns"></a>Colonne chiave  

 È consigliabile inserire un numero ridotto di colonne chiave o incluse in una definizione di indice filtrato e incorporare solo le colonne necessarie affinché Query Optimizer scelga l'indice filtrato per il piano di esecuzione della query. Sebbene Query Optimizer possa scegliere un indice filtrato per la query indipendentemente dal fatto che la copra o meno, tuttavia è più probabile che venga scelto un indice filtrato che copre la query.  
  
 In alcuni casi, un indice filtrato copre la query senza includere le colonne nell'espressione che lo definisce come colonne chiave o incluse nella definizione dell'indice stesso. Le linee guida seguenti indicano quando una colonna nell'espressione che definisce l'indice filtrato deve essere una colonna chiave o inclusa nella definizione dell'indice filtrato stesso. Gli esempi si riferiscono all'indice filtrato `FIBillOfMaterialsWithEndDate` creato in precedenza.  
  
 Non è necessario che una colonna nell'espressione che definisce l'indice filtrato sia una colonna chiave o inclusa nella definizione dell'indice stesso se l'espressione che definisce l'indice filtrato è equivalente al predicato della query e la query non restituisce la colonna in tale espressione con i risultati della query. L'indice `FIBillOfMaterialsWithEndDate` , ad esempio, copre la query seguente perché il predicato della query è equivalente all'espressione di filtro ed `EndDate` non viene restituito con i risultati della query. `FIBillOfMaterialsWithEndDate` non ha bisogno di `EndDate` come colonna chiave o inclusa nella definizione dell'indice filtrato.  
  
```sql
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;   
```  
  
 Una colonna nell'espressione che definisce l'indice filtrato deve essere una colonna chiave o inclusa nella definizione dell'indice se il predicato della query la utilizza in un confronto non equivalente all'espressione che definisce l'indice filtrato. L'indice `FIBillOfMaterialsWithEndDate` , ad esempio, è valido per la query seguente perché seleziona un subset di righe dall'indice filtrato. Tale indice tuttavia non copre la query poiché `EndDate` viene utilizzato nel confronto `EndDate > '20040101'`, che non è equivalente all'espressione che definisce l'indice filtrato. Poiché Query Processor non è in grado di eseguire questa query senza cercare i valori di `EndDate`, Di conseguenza, `EndDate` deve essere una colonna chiave o inclusa nella definizione dell'indice filtrato.  
  
```sql
SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
WHERE EndDate > '20040101';   
```  
  
 Una colonna nell'espressione che definisce l'indice filtrato deve essere una colonna chiave o inclusa nella definizione dell'indice se è presente nel set di risultati della query. L'indice `FIBillOfMaterialsWithEndDate` , ad esempio, non copre la query seguente perché restituisce la colonna `EndDate` nei risultati della query. Di conseguenza, `EndDate` deve essere una colonna chiave o inclusa nella definizione dell'indice filtrato.  
  
```sql
SELECT ComponentID, StartDate, EndDate FROM Production.BillOfMaterials  
WHERE EndDate IS NOT NULL;  
```  
  
 Non è necessario che la chiave di indice cluster della tabella sia una colonna chiave o inclusa nella definizione dell'indice filtrato poiché viene inclusa automaticamente in tutti gli indici non cluster, inclusi quelli filtrati.  
  
#### <a name="data-conversion-operators-in-the-filter-predicate"></a>Operatori di conversione dei dati nel predicato del filtro  

 Se l'operatore di confronto specificato nell'espressione che definisce l'indice filtrato determina una conversione dei dati implicita o esplicita, si verificherà un errore se la conversione viene eseguita sul lato sinistro di un operatore di confronto. Una soluzione consiste nello scrivere l'espressione che definisce l'indice filtrato con l'operatore di conversione dei dati (CAST o CONVERT) sul lato destro dell'operatore di confronto.  
  
 Nell'esempio seguente viene creata una tabella con tipi di dati diversi.  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.TestTable (a int, b varbinary(4));  
```  
  
 Nella definizione dell'indice filtrato seguente la colonna `b` viene convertita implicitamente a un tipo di dati integer per eseguire il confronto con la costante 1. Verrà generato un messaggio di errore 10611 poiché la conversione viene eseguita sul lato sinistro dell'operatore nel predicato filtrato.  
  
```sql
CREATE NONCLUSTERED INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = 1;  
```  
  
 La soluzione consiste nel convertire la costante sul lato destro in modo che sia dello stesso tipo della colonna `b`, come illustrato nell'esempio seguente:  
  
```sql
CREATE INDEX TestTabIndex ON dbo.TestTable(a,b)  
WHERE b = CONVERT(Varbinary(4), 1);  
```  
  
 Lo spostamento della conversione dei dati dal lato sinistro a quello destro di un operatore di confronto potrebbe modificare il significato della conversione. Nell'esempio precedente, quando l'operatore CONVERT è stato aggiunto al lato destro, il confronto è stato modificato da un confronto di un tipo integer in un confronto di tipo `varbinary`.  
  
 ![Icona freccia usata con il collegamento superiore](media/uparrow16x16.gif "icona freccia usata con il collegamento superiore") [In questa Guida](#Top)  
  
##  <a name="Additional_Reading"></a> Ulteriori informazioni  

 [Miglioramento delle prestazioni con le viste indicizzate di SQL Server 2008](https://msdn.microsoft.com/library/dd171921(v=sql.100).aspx)  
  
 [Partitioned Tables and Indexes](../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
