---
title: Usare le viste a gestione dinamica (DMV) di Analysis Services | Microsoft Docs
ms.date: 09/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24dd1bce8d7433f55ba64eecb1e7a08396b9e548
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52984102"
---
# <a name="dynamic-management-views-dmvs"></a>Viste a gestione dinamica (DMV) 

[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

Analysis Services dinamico gestione DMV (viste) sono le query che restituiscono informazioni relative agli oggetti del modello, le operazioni server e lo stato del server. La query, basata su SQL, è un'interfaccia ai *rowset dello schema*. I set di righe dello schema sono tabelle predescribed che contengono informazioni sugli oggetti di Analysis Services e stato del server, incluso lo schema del database, le sessioni attive, connessioni, comandi e dei processi in esecuzione nel server.

Le query DMV rappresentano un'alternativa all'esecuzione di comandi di individuazione XML/A. Per la maggior parte degli amministratori, la scrittura di una query DMV è più semplice poiché la sintassi è basata su SQL. Inoltre, il risultato viene restituito in un formato di tabella che è più facile da leggere e copiare. 
  
DMV la maggior parte delle query usano un **selezionate** istruzione e il **$System** schema con un set di righe dello schema XML/A, ad esempio:  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 Le query DMV restituiscono informazioni sullo stato di server e l'oggetto al momento dell'esecuzione della query. Per monitorare le operazioni in tempo reale, usare invece la traccia. Per altre informazioni in tempo reale grazie alle tracce, vedere Monitoraggio [utilizzare SQL Server Profiler per monitorare Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
## <a name="query-syntax"></a>sintassi di query

Il motore di query per le DMV è il parser di data mining. La sintassi di query DMV è basata su SELECT &#40;DMX&#41; istruzione. Sebbene la sintassi di query DMV sia basata su un'istruzione SQL SELECT, non è supportata la sintassi completa di un'istruzione SELECT. In particolare, non sono supportate le clausole JOIN, GROUP BY, LIKE, CAST e CONVERT.  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
Nell'esempio seguente per DISCOVER_CALC_DEPENDENCY viene illustrato l'utilizzo della clausola WHERE per fornire un parametro alla query:  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
Per set di righe dello schema che prevedono restrizioni, la query deve includere la funzione SYSTEMRESTRICTSCHEMA. L'esempio seguente restituisce i metadati CSDL modelli tabulari a livello di compatibilità 1103 circa. Notare che CATALOG_NAME distingue tra maiuscole e minuscole:  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  

## <a name="examples-and-scenarios"></a>Esempi e scenari

Una query DMV può essere utile per rispondere a domande sulle connessioni e sulle sessioni attive, nonché per verificare quali oggetti stanno utilizzando la maggior parte di memoria o CPU in un momento specifico. Ad esempio:
  
 `Select * from $System.discover_object_activity`  
Questa query fornisce informazioni sull'oggetto attività dall'ultimo avvio del servizio. 
  
 `Select * from $System.discover_object_memory_usage`  
Questa query fornisce informazioni sull'utilizzo di memoria per oggetto.  
  
 `Select * from $System.discover_sessions`  
Questa query fornisce informazioni sulle sessioni attive, incluse la durata e utente della sessione.  
  
 `Select * from $System.discover_locks`   
Questa query restituisce uno snapshot dei blocchi usati in un momento specifico nel tempo.  


## <a name="tools-and-permissions"></a>Strumenti e autorizzazioni

È possibile usare qualsiasi applicazione client che supporta le query MDX o DMX. Nella maggior parte dei casi, è consigliabile usare SQL Server Management Studio. È necessario disporre delle autorizzazioni di amministratore di server nell'istanza di query su una DMV.  
  
 **Per eseguire una query DMV da SQL Server Management Studio**

1. Connettersi al server e l'oggetto modello che si desidera eseguire una query. 
2. Fare doppio clic su oggetto server o database > **nuova Query** > **MDX**.
3. Digitare la query e quindi fare clic su **Execute**, oppure premere F5.
  
## <a name="schema-rowsets"></a>Set di righe dello schema

Non tutti i set di righe dello schema dispongono di un'interfaccia DMV. Per restituire un elenco di tutti i set di righe dello schema su cui è possibile eseguire una query utilizzando DMV, eseguire la query seguente.  
 
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
Se una DMV non è disponibile per un determinato set di righe, il server restituirà l'errore: `The <schemarowset> request type was not recognized by the server.` Tutti gli altri errori indicano problemi con la sintassi.  

I set di righe dello schema sono descritti nelle due protocolli di SQL Server Analysis Services:   

[[MS-SSAS-T]: Protocollo tabulare di SQL Server Analysis Services](https://msdn.microsoft.com/library/mt719260) -descrive i set di righe dello schema per i modelli tabulari a livello di compatibilità 1200 e versioni successive.

[[MS-SSAS]: SQL Server Analysis Services protocollo](https://msdn.microsoft.com/library/ee320606) -descrive i set di righe dello schema per i modelli multidimensionali e modelli tabulari ai livelli di compatibilità 1100 e 1103.

### <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>Set di righe descritto in [MS-SSAS-T]: Protocollo tabulare di SQL Server Analysis Services

|Set di righe  |Descrizione  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|Fornisce informazioni sugli oggetti nel modello di annotazione.|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   Fornisce informazioni sugli oggetti AttributeHierarchy per una colonna.      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  Fornisce informazioni sugli oggetti di colonna in ogni tabella.       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|Fornisce informazioni sugli oggetti ColumnPermission in ogni autorizzazione di tabella.|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|Fornisce informazioni sugli oggetti nel modello di impostazioni cultura.|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   Fornisce informazioni sugli oggetti origine dati nel modello.      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|Fornisce informazioni sugli oggetti DetailRowsDefinition nel modello.|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|Fornisce informazioni sugli oggetti di espressione nel modello.|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|Fornisce informazioni sugli oggetti ExtendedProperty nel modello.|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    Fornisce informazioni sugli oggetti gerarchia in ogni tabella.     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    Fornisce informazioni sugli oggetti KPI nel modello.     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   Vengono fornite informazioni sugli oggetti a livello di ogni gerarchia.      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|Fornisce informazioni sui sinonimi per gli oggetti del modello per una specifica impostazione cultura|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    Fornisce informazioni sugli oggetti di misure in ogni tabella.     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  Specifica un oggetto modello nel database.       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|Fornisce informazioni sulle traduzioni di oggetti diversi per impostazioni cultura.|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     Fornisce informazioni sugli oggetti partizione in ogni tabella.    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   Fornisce informazioni sugli oggetti PerspectiveColumn nell'oggetto PerspectiveTable a ogni.      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  Fornisce informazioni sugli oggetti PerspectiveHierarchy in ogni oggetto PerspectiveTable.       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    Fornisce informazioni sugli oggetti PerspectiveMeasure in ogni oggetto PerspectiveTable.     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    Fornisce informazioni sugli oggetti tabella in una prospettiva.     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     Fornisce informazioni sugli oggetti della prospettiva nel modello.    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    Fornisce informazioni sugli oggetti di relazione nel modello.     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  Fornisce informazioni sugli oggetti RoleMembership in ogni ruolo.      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   Fornisce informazioni sugli oggetti nel modello di ruolo.      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    Vengono fornite informazioni sugli oggetti TablePermission di ogni ruolo.     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   Fornisce informazioni sugli oggetti tabella nel modello.      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|Fornisce informazioni sugli oggetti variazione in ogni colonna.|

### <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>Set di righe descritto in [MS-SSAS]: Protocollo SQL Server Analysis Services

|Set di righe|Descrizione|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|Descrive i cataloghi che sono accessibili nel server.|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|Restituisce una riga per ogni misura, ogni attributo della dimensione del cubo e ogni colonna del set di righe dello schema, esposto come colonna.|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|Identifica i tipi di dati (base) supportati dal server.|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|Restituisce le dimensioni, gruppi di misure o i set di righe dello schema esposti come tabelle.|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| Restituisce informazioni sulle dipendenze di calcolo per un oggetto specificato in un database tabulare o in una query DAX che viene eseguita su un database tabulare. |  
|[DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|Fornisce informazioni sull'utilizzo delle risorse e sulle attività relative agli oggetti utilizzati dal comando a cui si fa riferimento.|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|Fornisce informazioni sull'utilizzo delle risorse e sulle attività relative all'ultimo comando eseguito o attualmente in esecuzione nelle connessioni aperte nel server.|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|Fornisce informazioni sull'utilizzo delle risorse e sulle attività relative alle connessioni attualmente aperte nel server.|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|Restituisce informazioni sui metadati del database per i database in memoria.|  
|[DISCOVER_DATASOURCES](https://msdn.microsoft.com/library/ee320285)|Restituisce un elenco delle origini dati disponibili nel server.|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|Fornisce informazioni sull'utilizzo delle risorse e sulle attività relative alle connessioni attualmente aperte dal server a un database.|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|Restituisce statistiche sulla dimensione specificata.|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|Restituisce un elenco di nomi, tipi di dati e valori di enumerazione di enumeratori supportati dal provider XMLA per un'origine dati specifica.|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|Descrive le istanze nel server.|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|Fornisce informazioni sui processi attivi in esecuzione nel server. Un processo fa parte di un comando che esegue un'attività specifica per conto del comando.|  
|[DISCOVER_KEYWORDS &AMP;#40;XMLA&AMP;#41;](https://msdn.microsoft.com/library/ee301719)|Restituisce informazioni sulle parole chiave riservate dal server di XMLA.|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|Restituisce informazioni sui valori letterali supportati dal server.|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|Restituisce informazioni sul contenuto di un file di backup. |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|Fornisce informazioni sui blocchi correnti presenti nel server.|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|Restituisce la chiave di crittografia master del server.|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|Restituisce un elenco di concessioni di quote di memoria interna recuperate da processi attualmente in esecuzione nel server.|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|Restituisce le statistiche di DISCOVER_MEMORYUSAGE per vari oggetti allocati dal server.|  
|[DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|Fornisce l'utilizzo delle risorse per oggetto dopo l'avvio del servizio.|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|Restituisce le statistiche di DISCOVER_MEMORYUSAGE per vari oggetti allocati dal server.|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|Restituisce statistiche sulla dimensione associata a una partizione.|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|Restituisce statistiche sulle aggregazioni in una partizione specifica.|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|Restituisce il valore di uno o più specifici contatori di prestazioni. |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|Restituisce un elenco di informazioni e valori sulle proprietà supportate dal server per l'origine dati specificata.|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|Restituisce informazioni sui buffer circolare XEvent corrente nel server.|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|Restituisce i nomi, restrizioni, descrizione e altre informazioni per tutte le richieste di individuazione.|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|Fornisce informazioni sull'utilizzo delle risorse e sulle attività relative alle sessioni attualmente aperte nel server.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|Restituisce informazioni sui segmenti di colonna usato per archiviare dati per le tabelle in memoria.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|Contiene informazioni sulle colonne utilizzate per rappresentare le colonne di una tabella in memoria.|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|Restituisce le statistiche sulle tabelle in memoria disponibile nel server.|  
|[DISCOVER_TRACE_COLUMNS](https://msdn.microsoft.com/library/ee301342)||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|Contiene il set di righe dello schema DISCOVER_TRACE_COLUMNS.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|Contiene il set di righe dello schema DISCOVER_TRACE_EVENT_CATEGORIES.|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|Contiene il set di righe dello schema DISCOVER_TRACES.|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|Restituisce il set corrente di transazioni in sospeso nel sistema.|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|Vengono fornite informazioni sulle tracce XEvent attualmente attive nel server.|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|Fornisce informazioni sui pacchetti XEvent descritti nel server.|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|Fornisce informazioni sugli oggetti XEvent descritti nel server.|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|Fornisce informazioni sullo schema degli oggetti XEvent descritti nel server.|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|Fornisce informazioni sulle sessioni XEvent corrente nel server.|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|Fornisce informazioni sulle destinazioni della sessione XEvent corrente nel server.|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|Restituisce un set di righe con una riga e una colonna. |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|Descrive le singole colonne di tutti i modelli di data mining di dati descritti distribuiti nel server.|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|Descrive le funzioni di data mining di dati supportati da algoritmi di data mining disponibili in un server che esegue Analysis Services.|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|Consente all'applicazione client di esplorare il contenuto di un modello di data mining di dati sottoposti a training.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|Restituisce la struttura XML del modello di data mining. Il formato della stringa XML segue lo standard PMML 2.1.|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|Restituisce la struttura XML del modello di data mining. Il formato della stringa XML segue lo standard PMML 2.1.|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|Enumera i modelli di data mining distribuiti nel server.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|Fornisce un elenco dei parametri che è possibile utilizzare per configurare il comportamento di ogni algoritmo di data mining installato nel server.|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|Fornisce informazioni su ogni algoritmo di data mining supportati dal server.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|Descrive le singole colonne di tutte le strutture di data mining distribuite nel server.|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|Enumera informazioni sulle strutture di data mining nel catalogo corrente.|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|Descrive le azioni che possono essere disponibili per l'applicazione client.|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|Descrive la struttura dei cubi all'interno di un database. Le prospettive vengono restituite anche in questo schema.|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|Descrive le dimensioni all'interno di un database.|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|Restituisce informazioni sulle funzioni attualmente disponibili per l'uso nei linguaggi MDX e DAX.|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|Descrive ogni gerarchia all'interno di una determinata dimensione.|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|Descrive gli oggetti origine dei dati descritti all'interno del database.|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|Descrive gli indicatori KPI all'interno di un database.|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|Descrive ogni livello all'interno di una determinata gerarchia.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|Enumera le dimensioni dei gruppi di misure.|  
|[MDSCHEMA_MEASUREGROUPS](https://msdn.microsoft.com/library/ee320601)|Descrive i gruppi di misure all'interno di un database.|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|Descrive ogni misura.|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|Descrive i membri all'interno di un database.|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|Descrive le proprietà dei membri e le proprietà delle celle.|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|Descrive i set attualmente descritti in un database, compresi i set con ambito sessione.|  

> [!NOTE]
> Viste a gestione dinamica di risorse di archiviazione non è un set di righe dello schema descritto nella specifica del protocollo.