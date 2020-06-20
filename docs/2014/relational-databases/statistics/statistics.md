---
title: Statistiche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0f0950e48245bed53581d2f91b120ab9555aa562
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064579"
---
# <a name="statistics"></a>Statistiche
  In Query Optimizer vengono utilizzate le statistiche per creare piani di query che consentono di migliorare le prestazioni di esecuzione delle query. Per la maggior parte delle query, Query Optimizer genera già le statistiche necessarie per un piano di query di alta qualità. In alcuni casi, è necessario creare statistiche aggiuntive o modificare la progettazione delle query per ottenere risultati migliori. In questo argomento vengono illustrati i concetti relativi alle statistiche e vengono fornite linee guida per un utilizzo efficace delle statistiche di ottimizzazione delle query.  
  
##  <a name="components-and-concepts"></a><a name="DefinitionQOStatistics"></a> Componenti e concetti  
 Statistiche  
 Le statistiche di ottimizzazione delle query sono oggetti contenenti informazioni statistiche sulla distribuzione dei valori in una o più colonne di una tabella o di una vista indicizzata. In Query Optimizer queste statistiche vengono usate per la stima della *cardinalità*o del numero di righe nel risultato della query. Queste *stime di cardinalità* consentono a Query Optimizer di creare un piano di query di alta qualità. Query Optimizer può ad esempio utilizzare le stime della cardinalità per scegliere l'operatore Index Seek anziché l'operatore Index Scan che utilizza un numero più elevato di risorse, migliorando di conseguenza le prestazioni di esecuzione delle query.  
  
 Ogni oggetto statistiche viene creato in un elenco di una o più colonne di tabella e include un istogramma in cui è visualizzata la distribuzione dei valori nella prima colonna. Negli oggetti statistiche su più colonne sono inoltre archiviate informazioni statistiche sulla correlazione dei valori tra le colonne. Queste statistiche sulla correlazione o *densità*derivano dal numero di righe distinte di valori di colonna. Per altre informazioni sugli oggetti statistiche, vedere [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql).  
  
 Statistiche filtrate  
 Le statistiche filtrate possono migliorare le prestazioni di esecuzione delle query che effettuano la selezione da subset ben definiti di dati. Le statistiche filtrate utilizzano un predicato del filtro per selezionare il subset di dati incluso nelle statistiche. Statistiche filtrate progettate correttamente possono migliorare il piano di esecuzione delle query rispetto alle statistiche di tabella completa. Per altre informazioni sul predicato del filtro, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql). Per altre informazioni su quando creare statistiche filtrate, vedere la sezione [Quando creare le statistiche](#UpdateStatistics) in questo argomento. Per un case study, vedere l'intervento di blog sull' [uso di statistiche filtrate con le tabelle partizionate](https://go.microsoft.com/fwlink/?LinkId=178505)sul sito Web SQLCAT.  
  
 Opzioni relative alle statistiche  
 Sono disponibili tre opzioni che se impostate influiscono sui tempi e sulle modalità di creazione e aggiornamento delle statistiche. Queste opzioni vengono impostate solo a livello di database.  
  
 Opzione AUTO_CREATE_STATISTICS  
 Quando l'opzione per la creazione automatica delle statistiche, AUTO_CREATE_STATISTICS, è impostata su ON (attivata), Query Optimizer crea le statistiche necessarie per colonne singole nel predicato di query, al fine di migliorare le stime della cardinalità per il piano di query. Queste statistiche di colonna singola vengono create in colonne che ancora non dispongono di un istogramma in un oggetto statistiche esistente. L'opzione AUTO_CREATE_STATISTICS non determina se le statistiche vengono create per gli indici. Questa opzione non genera inoltre statistiche filtrate, ma si applica esclusivamente alle statistiche di colonna singola per la tabella completa.  
  
 Quando Query Optimizer crea statistiche per colonne singole in seguito all'utilizzo dell'opzione AUTO_CREATE_STATISTICS, il nome delle statistiche inizia con `_WA`. Per determinare se tramite Query Optimizer vengono create statistiche per una colonna del predicato di query, è possibile utilizzare la query riportata di seguito.  
  
```  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
 Opzione AUTO_UPDATE_STATISTICS  
 Quando l'opzione per l'aggiornamento automatico delle statistiche, AUTO_UPDATE_STATISTICS, è impostata su ON, Query Optimizer determina se le statistiche potrebbero non essere aggiornate, quindi ne esegue l'aggiornamento qualora vengano utilizzate tramite una query. Le statistiche diventano obsolete in seguito a operazioni di inserimento, aggiornamento, eliminazione o unione che modificano la distribuzione dei dati nella tabella o nella vista indicizzata. Query Optimizer determina che le statistiche potrebbero non essere aggiornate contando il numero di modifiche apportate ai dati dopo l'ultimo aggiornamento delle statistiche e confrontando il numero di modifiche con una soglia basata sul numero di righe nella tabella o nella vista indicizzata.  
  
 Query Optimizer controlla la presenza di statistiche non aggiornate prima di compilare una query e prima di eseguire un piano di query memorizzato nella cache. Prima di compilare una query, Query Optimizer usano le colonne, le tabelle e le viste indicizzate nel predicato di query per identificare le eventuali statistiche non aggiornate. Prima di eseguire un piano di query memorizzato nella cache, il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] verifica che tale piano faccia riferimento alle statistiche aggiornate.  
  
 L'opzione AUTO_UPDATE_STATISTICS si applica a oggetti statistiche creati per indici, colonne singole nei predicati di query e statistiche create con l'istruzione [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) . Questa opzione si applica anche alle statistiche filtrate.  
  
 AUTO_UPDATE_STATISTICS_ASYNC  
 L'opzione relativa all'aggiornamento asincrono delle statistiche, AUTO_UPDATE_STATISTICS_ASYNC, determina se Query Optimizer utilizza gli aggiornamenti sincroni o asincroni delle statistiche. L'opzione relativa all'aggiornamento asincrono delle statistiche è disattivata (OFF) per impostazione predefinita. Query Optimizer aggiorna pertanto le statistiche in modo sincrono. L'opzione AUTO_UPDATE_STATISTICS_ASYNC si applica a oggetti statistiche creati per indici, colonne singole nei predicati di query e statistiche create con l'istruzione [Create Statistics](/sql/t-sql/statements/create-statistics-transact-sql) .  
  
 Gli aggiornamenti delle statistiche possono essere sincroni (impostazione predefinita) o asincroni. Con gli aggiornamenti sincroni delle statistiche, le query vengono sempre compilate ed eseguite con statistiche aggiornate. Se le statistiche sono obsolete, Query Optimizer rimane in attesa di statistiche aggiornate prima di compilare ed eseguire la query. Con gli aggiornamenti asincroni delle statistiche, le query vengono compilate con le statistiche esistenti anche non sono aggiornate. È possibile che Query Optimizer scelga un piano di query non ottimale se le statistiche non sono aggiornate al momento della compilazione della query. L'utilizzo di statistiche aggiornate offrirà vantaggi nelle query compilate dopo il completamento degli aggiornamenti asincroni.  
  
 Utilizzare le statistiche sincrone quando si eseguono operazioni che modificano la distribuzione dei dati, quali il troncamento di una tabella o l'esecuzione di un inserimento bulk di una percentuale elevata di righe. Se non si aggiornano le statistiche dopo avere completato l'operazione, l'utilizzo di statistiche sincrone garantisce che le statistiche vengano aggiornate prima di eseguire query sui dati modificati.  
  
 Utilizzare le statistiche asincrone per ottenere tempi di risposta alle query più stimabili per gli scenari seguenti:  
  
-   L'applicazione esegue di frequente la stessa query, query analoghe o piani di query memorizzati nella cache analoghi. È possibile che gli aggiornamenti asincroni delle statistiche consentano di ottenere tempi di risposta alle query più stimabili rispetto agli aggiornamenti sincroni delle statistiche perché Query Optimizer può eseguire le query in entrata senza attendere le statistiche aggiornate. Ciò evita che alcune query vengano eseguite in ritardo rispetto ad altre.  
  
-   Sono stati riscontrati timeout nelle richieste client causati da una o più query in attesa delle statistiche aggiornate. In alcuni casi, l'attesa delle statistiche sincrone può causare errori nelle applicazioni con timeout aggressivi.  
  
 INCREMENTAL STATS  
 Quando impostata su ON, le statistiche create sono di tipo per partizione. Quando impostata su OFF, l'albero delle statistiche viene eliminato e le statistiche vengono rielaborate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Il valore predefinito è OFF. Questa impostazione esegue l'override della proprietà INCREMENTAL a livello di database.  
  
 Quando vengono aggiunte delle nuove partizioni a una tabella di grandi dimensioni, è necessario aggiornare le statistiche per includere le nuove partizioni. Tuttavia, l'analisi dell'intera tabella (opzione FULLSCAN o SAMPLE) potrebbe richiedere diverso tempo. Inoltre, l'analisi dell'intera tabella non è necessaria in quanto occorrono solo le statistiche sulle nuove partizioni. L'opzione Incrementale crea e archivia le statistiche in base alle partizioni, e quando viene eseguito un aggiornamento, permette di aggiornare solo le statistiche di quelle partizioni che richiedono nuove statistiche.  
  
 Se le statistiche per partizione non sono supportate, l'opzione viene ignorata e viene generato un avviso. Le statistiche incrementali non sono supportate per i seguenti tipi di statistiche:  
  
-   Statistiche create con indici che non hanno il partizionamento allineato con la tabella di base.  
  
-   Statistiche create per i database secondari leggibili AlwaysOn.  
  
-   Statistiche create per i database di sola lettura.  
  
-   Statistiche create per gli indici filtrati.  
  
-   Statistiche create per le viste.  
  
-   Statistiche create per le tabelle interne.  
  
-   Statistiche create con indici spaziali o indici XML.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
##  <a name="when-to-create-statistics"></a><a name="CreateStatistics"></a>Quando creare le statistiche  
 Query Optimizer crea già le statistiche nelle modalità seguenti:  
  
1.  Query Optimizer crea statistiche per gli indici in tabelle o viste, al momento della creazione dell'indice stesso. Tali statistiche vengono create nelle colonne chiave dell'indice. Se l'indice è filtrato, Query Optimizer crea statistiche filtrate nello stesso subset di righe specificato per l'indice filtrato. Per altre informazioni sugli indici filtrati, vedere [Creare indici filtrati](../indexes/create-filtered-indexes.md) e [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
2.  Quando AUTO_CREATE_STATISTICS è impostata su ON, Query Optimizer crea statistiche per le singole colonne nei predicati di query.  
  
 Per la maggior parte delle query, questi due metodi di creazione delle statistiche garantiscono la definizione di un piano di query di alta qualità. In alcuni casi, è possibile migliorare i piani di query creando statistiche aggiuntive con l'istruzione [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) . Tali statistiche aggiuntive possono acquisire correlazioni statistiche che non vengono prese in considerazione in Query Optimizer durante la creazione di statistiche per indici o singole colonne. È possibile che nell'applicazione siano disponibili correlazioni statistiche aggiuntive nei dati della tabella che, se calcolate in un oggetto statistiche, possono consentire a Query Optimizer di migliorare i piani di query. Le statistiche filtrate per un subset di righe di dati o le statistiche multicolonna per le colonne dei predicati di query possono ad esempio migliorare il piano di query.  
  
 Quando si creano statistiche con l'istruzione CREATE STATISTICS, si consiglia di mantenere l'opzione AUTO_CREATE_STATISTICS impostata su ON, in modo tale che Query Optimizer continui a creare regolarmente statistiche di colonna singola per le colonne dei predicati di query. Per altre informazioni sui predicati, vedere [Condizione di ricerca&#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
 Utilizzare l'istruzione CREATE STATISTICS per creare statistiche in una delle seguenti condizioni:  
  
-   In Ottimizzazione guidata [!INCLUDE[ssDE](../../../includes/ssde-md.md)] viene indicato di creare statistiche.  
  
-   Il predicato di query contiene più colonne correlate che non si trovano ancora nello stesso indice.  
  
-   La query effettua la selezione da un subset di dati.  
  
-   La query presenta statistiche mancanti.  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>Il predicato di query contiene più colonne correlate  
 Quando il predicato di una query contiene più colonne correlate e dipendenti tra loro, è possibile che la creazione di statistiche per più colonne consenta di migliorare il piano di query. Le statistiche su più colonne contengono le statistiche sulla correlazione tra colonne, denominate *densità*, le quali non sono disponili nelle statistiche di colonna singola. Le densità possono migliorare le stime della cardinalità qualora i risultati della query dipendano da relazioni tra i dati di più colonne.  
  
 Se le colonne si trovano già nello stesso indice, l'oggetto statistiche multicolonna esiste già e non è necessario crearlo manualmente. Se le colonne ancora non si trovano nello stesso indice, è possibile creare le statistiche multicolonna tramite un indice nelle colonne o l'istruzione CREATE STATISTICS. La gestione di un indice richiede più risorse di sistema rispetto a un oggetto statistiche. Se l'applicazione non richiede l'indice multicolonna, è possibile utilizzare una quantità ridotta di risorse di sistema creando l'oggetto statistiche senza creare l'indice.  
  
 Quando si creano le statistiche multicolonna, l'ordine delle colonne nella definizione dell'oggetto statistiche influisce sull'efficacia delle densità nel calcolo delle stime della cardinalità. L'oggetto statistiche archivia le densità per ciascun prefisso delle colonne chiave nella definizione dell'oggetto statistiche. Per altre informazioni sulle densità, vedere [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql).  
  
 Per creare densità utili per le stime della cardinalità, è necessario che le colonne nel predicato di query corrispondano a uno dei prefissi delle colonne nella definizione dell'oggetto statistiche. Di seguito viene ad esempio creato un oggetto statistiche multicolonna per le colonne `LastName`, `MiddleName`e `FirstName`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 In questo esempio, l'oggetto statistiche `LastFirst` dispone delle densità per i seguenti prefissi di colonna: (`LastName`), (`LastName, MiddleName`) e (`LastName, MiddleName, FirstName`). La densità non è disponibile per (`LastName, FirstName`). Se la query utilizza `LastName` e `FirstName` senza utilizzare `MiddleName`, la densità non è disponibile per le stime della cardinalità.  
  
### <a name="query-selects-from-a-subset-of-data"></a>La query effettua la selezione da un subset di dati  
 La creazione di statistiche per indici e colonne singole in Query Optimizer implica la creazione di statistiche per i valori in tutte le righe. Quando le query effettuano la selezione da un subset di righe che dispone di una distribuzione dei dati univoca, le statistiche filtrate possono migliorare i piani di query. È possibile creare le statistiche filtrate utilizzando l'istruzione CREATE STATISTICS con la clausola WHERE per definire l'espressione del predicato del filtro.  
  
 Se ad esempio si utilizza [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], ogni prodotto nella tabella Production.Product appartiene a una delle quattro categorie della tabella Production.ProductCategory, ovvero Bikes, Components, Clothing e Accessories. Ogni categoria dispone di una distribuzione dei dati diversa in relazione al peso. I pesi nella categoria Bikes sono compresi tra 13,77 e 30, quelli della categoria Components sono compresi tra 2,12 e 1.050 con alcuni valori NULL e quelli delle categorie Clothing e Accessories sono tutti NULL.  
  
 Prendendo come esempio la categoria Bikes, le statistiche filtrate per tutti i pesi consentono di fornire a Query Optimizer statistiche più accurate e di migliorare la qualità del piano di query rispetto alle statistiche di tabella completa o alle statistiche inesistenti nella colonna relativa al peso (Weight). La colonna Weight della categoria Bikes rappresenta un candidato valido per le statistiche filtrate. Nel caso di un numero relativamente ridotto di ricerche correlate al peso, tale colonna non è tuttavia necessariamente un candidato valido per un indice filtrato. È possibile che i vantaggi derivanti dai miglioramenti alle prestazioni delle ricerche offerti da un indice filtrato siano inferiori rispetto agli svantaggi derivanti dai costi di manutenzione e archiviazione supplementari dovuti all'aggiunta di un indice filtrato al database.  
  
 L'istruzione seguente crea le statistiche filtrate di `BikeWeights` per tutte le sottocategorie di Bikes. L'espressione del predicato filtrata definisce le biciclette (Bikes) enumerando tutte le sottocategorie di Bikes con l'elemento `Production.ProductSubcategoryID IN (1,2,3)`di confronto. Il predicato non può utilizzare il nome di categoria Bikes perché viene archiviato nella tabella Production.ProductCategory e tutte le colonne nell'espressione di filtro devono trovarsi nella stessa tabella.  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../snippets/tsql/SQL14/tsql/statisticsddl/transact-sql/filteredstats.sql#filteredstats2)]  
  
 Query Optimizer può utilizzare le statistiche filtrate di `BikeWeights` per migliorare il piano di query per la query seguente che seleziona tutti gli elementi della categoria Bikes con peso maggiore di `25`.  
  
```  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>La query identifica le statistiche mancanti  
 Se un errore o un altro evento impedisce la creazione di statistiche da parte di Query Optimizer, il piano di query viene creato senza utilizzare statistiche. Query Optimizer contrassegna le statistiche come mancanti e tenta di rigenerare le statistiche alla successiva esecuzione della query.  
  
 Le statistiche mancanti sono indicate come avvisi (nome della tabella in rosso) quando il piano di esecuzione di una query viene visualizzato graficamente utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Il monitoraggio della classe di eventi **Missing Column Statistics** con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica anche i casi in cui le statistiche risultano mancanti. Per altre informazioni, vedere [Categoria di eventi Errori e avvisi &#40;Motore di database&#41;](../event-classes/errors-and-warnings-event-category-database-engine.md).  
  
 In caso di statistiche mancanti, effettuare quanto segue:  
  
-   Verificare che AUTO_CREATE_STATISTICS e AUTO_UPDATE_STATISTICS siano impostate su ON.  
  
-   Verificare che il database non sia di sola lettura. Se il database è di sola lettura, Query Optimizer non è in grado di salvare le statistiche.  
  
-   Creare le statistiche mancanti mediante l'istruzione CREATE STATISTICS.  
  
 Quando le statistiche su uno snapshot o un database di sola lettura sono mancanti o non aggiornate, il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] crea e gestisce statistiche temporanee in `tempdb`. Quando il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] crea statistiche temporanee, al nome delle statistiche viene aggiunto il suffisso _readonly_database_statistic per distinguere le statistiche temporanee da quelle permanenti. Il suffisso _readonly_database_statistic è riservato alle statistiche generate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È possibile creare script per le statistiche temporanee e riprodurli in un database di lettura e scrittura. Quando viene creato uno script, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] modifica il suffisso del nome delle statistiche da _readonly_database_statistic a _readonly_database_statistic_scripted.  
  
 Solo in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è possibile creare e aggiornare le statistiche temporanee. È tuttavia possibile eliminare le statistiche temporanee e monitorare le relative proprietà utilizzando gli stessi strumenti utilizzati per le statistiche permanenti:  
  
-   Eliminare le statistiche temporanee usando l'istruzione [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) .  
  
-   Monitorare le statistiche usando le viste del catalogo **sys.stats** e **sys.stats_columns** . **sys_stats** include una colonna, **is_temporary** , che indica quali statistiche sono permanenti e quali invece temporanee.  
  
 Poiché le statistiche temporanee sono archiviate in `tempdb`, un riavvio del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comporta l'indisponibilità di tutte le statistiche temporanee.  
  
##  <a name="when-to-update-statistics"></a><a name="UpdateStatistics"></a>Quando aggiornare le statistiche  
 Query Optimizer determina che le statistiche potrebbero non essere aggiornate, quindi ne effettua l'aggiornamento qualora siano necessarie per un piano di query. In alcuni casi, è possibile migliorare il piano di query e le prestazioni di esecuzione delle query aggiornando le statistiche più frequentemente di quanto accada quando AUTO_UPDATE_STATISTICS è impostata su ON. È possibile aggiornare le statistiche mediante l'istruzione UPDATE STATISTICS o la stored procedure sp_updatestats.  
  
 Sebbene consenta di garantire che le query vengano compilate con statistiche aggiornate, l'aggiornamento delle statistiche causa la ricompilazione delle query. Si consiglia di non aggiornare le statistiche troppo frequentemente perché è necessario mantenere un equilibrio a livello di prestazioni tra la necessità di migliorare i piani di query e il tempo necessario per la ricompilazione delle query. Tale equilibrio dipende dall'applicazione in uso.  
  
 Quando si utilizza UPDATE STATISTICS o sp_updatestats per aggiornare le statistiche, mantenere AUTO_UPDATE_STATISTICS impostata su ON, affinché l'aggiornamento continui a essere eseguito regolarmente in Query Optimizer. Per altre informazioni sull'aggiornamento delle statistiche per una colonna, un indice, una tabella o una vista indicizzata, vedere [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql). Per informazioni sull'aggiornamento delle statistiche per tutte le tabelle interne e definite dall'utente nel database, vedere la stored procedure [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql).  
  
 Per determinare la data dell'ultimo aggiornamento delle statistiche, usare la funzione [STATS_DATE](/sql/t-sql/functions/stats-date-transact-sql) .  
  
 Aggiornare le statistiche nei seguenti casi:  
  
-   I tempi di esecuzione delle query sono particolarmente lunghi.  
  
-   Si verificano operazioni di inserimento in colonne chiave crescenti o decrescenti.  
  
-   In seguito a operazioni di manutenzione.  
  
### <a name="query-execution-times-are-slow"></a>I tempi di esecuzione delle query sono particolarmente lunghi  
 Se i tempi di risposta alle query sono troppo lunghi o imprevedibili, assicurarsi che le query dispongano di statistiche aggiornate prima di eseguire ulteriori procedure di risoluzione dei problemi.  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>Si verificano operazioni di inserimento in colonne chiave crescenti o decrescenti  
 È possibile che le statistiche per colonne chiave crescenti o decrescenti, ad esempio colonne IDENTITY o timestamp in tempo reale, richiedano aggiornamenti più frequenti rispetto a quelli previsti in Query Optimizer. Le operazioni di inserimento accodano nuovi valori alle colonne crescenti o decrescenti. È possibile che il numero di righe aggiunte non sia sufficiente per attivare un aggiornamento delle statistiche. Se le statistiche non sono aggiornate e le query effettuano la selezione dalle righe aggiunte più di recente, le statistiche correnti non disporranno delle stime della cardinalità per tali nuovi valori. Ciò può comportare imprecisioni nelle stime della cardinalità e prestazioni di esecuzione delle query ridotte.  
  
 Le stime della cardinalità di una query che effettua la selezione dalle date degli ordini di vendita più recenti non saranno ad esempio precise se le statistiche non sono aggiornate in modo da includere le stime della cardinalità di tali date.  
  
### <a name="after-maintenance-operations"></a>In seguito a operazioni di manutenzione  
 Aggiornare le statistiche dopo avere eseguito procedure di manutenzione che modificano la distribuzione dei dati, quali il troncamento di una tabella o l'esecuzione di un inserimento bulk di un'elevata percentuale di righe. Ciò consente di evitare ritardi futuri nell'elaborazione delle query causati dall'attesa da parte delle query stesse degli aggiornamenti automatici delle statistiche.  
  
 Operazioni quali la ricompilazione, la deframmentazione o la riorganizzazione di un indice non modificano la distribuzione dei dati. Non è pertanto necessario aggiornare le statistiche in seguito all'esecuzione di operazioni ALTER INDEX REBUILD, DBCC REINDEX, DBCC INDEXDEFRAG o ALTER INDEX REORGANIZE. L'aggiornamento delle statistiche viene eseguito in Query Optimizer in seguito alla ricompilazione di un indice in una tabella o una vista mediante ALTER INDEX REBUILD o DBCC DBREINDEX. Tale aggiornamento delle statistiche è tuttavia il risultato della ricostruzione dell'indice. L'aggiornamento delle statistiche non viene eseguito in Query Optimizer dopo operazioni DBCC INDEXDEFRAG o ALTER INDEX REORGANIZE.  
  
##  <a name="queries-that-use-statistics-effectively"></a><a name="DesignStatistics"></a>Query che utilizzano le statistiche in modo efficace  
 Alcune implementazioni delle query, quali le variabili locali e le espressioni complesse nel predicato di query, possono comportare la definizione di piani di query non ottimali. Per evitare che ciò accada, attenersi alle linee guida relative alla progettazione delle query per un utilizzo efficace delle statistiche. Per altre informazioni sui predicati, vedere [Condizione di ricerca&#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql).  
  
 È possibile migliorare i piani di query applicando le linee guida relative alla progettazione delle query che prevedono un utilizzo efficace delle statistiche, al fine di migliorare le *stime della cardinalità* per espressioni, variabili e funzioni usate nei predicati di query. Se il valore di un'espressione, di una variabile o di una funzione non è noto, Query Optimizer non è in grado di determinare il valore da ricercare nell'istogramma e non può pertanto recuperare la stima della cardinalità ottimale dall'istogramma. In tal caso, la stima della cardinalità di Query Optimizer si basa sul numero medio di righe per valore distinct per tutte le righe campionate nell'istogramma. Ciò comporta stime della cardinalità non ottimali e può causare una riduzione delle prestazioni di esecuzione delle query.  
  
 Nelle linee guida seguenti viene indicato come scrivere query per migliorare i piani di query grazie all'ottimizzazione delle stime della cardinalità.  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>Miglioramento delle stime della cardinalità per le espressioni  
 Per migliorare le stime della cardinalità per le espressioni, attenersi alle seguenti linee guida:  
  
-   Se possibile, semplificare le espressioni contenenti costanti. Query Optimizer non valuta tutte le funzioni e le espressioni che contengono costanti prima di determinare le stime della cardinalità. Semplificare ad esempio l'espressione ABS(`-100) to 100`.  
  
-   Se l'espressione utilizza più variabili, creare una colonna calcolata per l'espressione, quindi creare le statistiche o un indice nella colonna calcolata. È ad esempio possibile che la stima della cardinalità del predicato di query `WHERE PRICE + Tax > 100` sia migliore se si crea una colonna calcolata per l'espressione `Price + Tax`.  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>Miglioramento delle stime della cardinalità per variabili e funzioni  
 Per migliorare le stime della cardinalità per variabili e funzioni, attenersi alle seguenti linee guida:  
  
-   Se nel predicato di query viene utilizzata una variabile locale, riscrivere la query in modo da utilizzare un parametro anziché una variabile locale. Il valore di una variabile locale non è noto quando Query Optimizer crea il piano di esecuzione della query. Quando una query utilizza un parametro, Query Optimizer utilizza la stima della cardinalità per il primo valore di parametro effettivo passato alla stored procedure.  
  
-   Utilizzare una tabella standard o una tabella temporanea per archiviare i risultati di funzioni con valori di tabella con più istruzioni. Query Optimizer non crea statistiche per le funzioni con valori di tabella con più istruzioni. In questo modo, Query Optimizer è in grado di creare statistiche per le colonne della tabella e utilizzarle per definire un piano di query più efficace.  
  
-   Utilizzare una tabella standard o una tabella temporanea in sostituzione delle variabili di tabella. Query Optimizer non crea statistiche per le variabili di tabella. In questo modo, Query Optimizer è in grado di creare statistiche per le colonne della tabella e utilizzarle per definire un piano di query più efficace. Diversi elementi determinano l'opportunità di utilizzare una tabella temporanea o una variabile di tabella. Le variabili di tabella utilizzate nelle stored procedure causano un numero di ricompilazioni delle stored procedure inferiore rispetto alle tabelle temporanee. In base all'applicazione in uso, è possibile che l'utilizzo di una tabella temporanea al posto di una variabile di tabella non comporti un miglioramento delle prestazioni.  
  
-   Se una stored procedure contiene una query che utilizza un parametro passato, evitare di modificare il valore del parametro all'interno della stored procedure prima di utilizzarlo nella query. Le stime della cardinalità per la query sono basate sul valore del parametro passato, non sul valore aggiornato. Per evitare di modificare il valore del parametro, è possibile riscrivere la query in modo da utilizzare due stored procedure.  
  
     La seguente stored procedure `Sales.GetRecentSales` modifica ad esempio il valore del parametro `@date` se `@date is NULL`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     Se la prima chiamata alla stored procedure `Sales.GetRecentSales` passa un valore NULL per il parametro `@date` , Query Optimizer compilerà la stored procedure con la stima della cardinalità per `@date = NULL` anche se il predicato di query non è chiamato con `@date = NULL`. È possibile che tale stima della cardinalità differisca notevolmente rispetto al numero di righe nel risultato della query effettivo. È pertanto possibile che in Query Optimizer venga scelto un piano di query non ottimale. Per evitare che ciò accada, è possibile riscrivere la stored procedure utilizzando due procedure, come illustrato di seguito:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>Miglioramento delle stime della cardinalità con gli hint per la query  
 Per migliorare le stime della cardinalità per le variabili locali, è possibile utilizzare gli hint per la query OPTIMIZE FOR o OPTIMIZE FOR UNKNOWN con RECOMPILE. Per altre informazioni, vedere [Hint per la query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).  
  
 In alcune applicazioni, la ricompilazione della query ogni volta che viene eseguita può richiedere tempi troppo lunghi. L'hint per la query OPTIMIZER FOR può risultare utile anche se non si utilizza l'opzione RECOMPILE. È possibile ad esempio aggiungere un'opzione OPTIMIZER FOR alla stored procedure Sales.GetRecentSales per indicare una data specifica. Nell'esempio seguente viene aggiunta l'opzione OPTIMIZE FOR alla procedura Sales.GetRecentSales.  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>Miglioramento delle stime della cardinalità con le guide di piano  
 È possibile che le linee guida relative alla progettazione delle query non siano valide per alcune applicazioni, in quanto non è possibile modificare la query o l'utilizzo dell'hint per la query RECOMPILE potrebbe causare un numero eccessivo di ricompilazioni. È possibile utilizzare le guide di piano per specificare altri hint, ad esempio USE PLAN, in modo da controllare il comportamento della query mentre si collabora con il fornitore dell'applicazione per esaminarne le modifiche. Per altre informazioni sulle guide di piano, vedere [Guide di piano](../performance/plan-guides.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREAZIONE di statistiche &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-statistics-transact-sql)   
 [AGGIORNARE le statistiche &#40;&#41;Transact-SQL](/sql/t-sql/statements/update-statistics-transact-sql)   
 [sp_updatestats &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)   
 [DBCC SHOW_STATISTICS &#40;&#41;Transact-SQL](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)   
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [DROP STATISTICs &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [Creare indici filtrati](../indexes/create-filtered-indexes.md)  
