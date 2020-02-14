---
title: Modalità di raccolta dei dati di Query Store | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71974358"
---
# <a name="how-query-store-collects-data"></a>Modalità di raccolta dei dati di Query Store
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Query Store funge da vera e propria scatola nera, raccogliendo costantemente le informazioni di compilazione e runtime relative a query e piani. I dati relativi alle query sono salvati in modo permanente nelle tabelle interne e presentati agli utenti mediante una serie di viste.
  
## <a name="views"></a>Viste 
 Il diagramma seguente mostra le viste di Archivio query e le loro relazioni logiche, con le informazioni della fase di compilazione presentate come entità blu:
  
 ![Viste del processo Query Store](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**Descrizioni delle viste**  
  
|Visualizza|Descrizione|  
|----------|-----------------|  
|**sys.query_store_query_text**|Presenta i testi delle singole query univoche eseguite sul database. I commenti e gli spazi prima e dopo il testo della query vengono ignorati. I commenti e gli spazi all'interno del testo non vengono ignorati. Ogni istruzione del batch genera una voce diversa nell'elenco dei testi di query.|  
|**sys.query_context_settings**|Presenta combinazioni univoche di impostazioni che influiscono sul piano e con cui sono eseguite le query. Lo stesso testo della query eseguito con impostazioni diverse che influiscono sul piano genera una voce di query separata in Query Store in quanto `context_settings_id` fa parte della chiave della query.|  
|**sys.query_store_query**|Voci di query che vengono monitorate e forzate separatamente in Query Store. Un singolo testo della query può generare più voci di query se viene eseguito con impostazioni di contesto diverse o se viene eseguito all'esterno anziché all'interno di moduli [!INCLUDE[tsql](../../includes/tsql-md.md)] diversi, come stored procedure e trigger.|  
|**sys.query_store_plan**|Presenta il piano stimato per la query con le statistiche della fase di compilazione. Il piano archiviato è equivalente a quello che si ottiene usando `SET SHOWPLAN_XML ON`.|  
|**sys.query_store_runtime_stats_interval**|Archivio query divide il tempo in finestre temporali (intervalli) generate automaticamente e archivia le statistiche aggregate per tale intervallo per ogni piano eseguito. La dimensione dell'intervallo è controllata dall'opzione di configurazione **Intervallo di raccolta statistiche** (in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) o `INTERVAL_LENGTH_MINUTES` usando le [opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**sys.query_store_runtime_stats**|Statistiche di runtime aggregate per i piani eseguiti. Tutte le metriche acquisite sono espresse sotto forma di quattro funzioni statistiche: Media, Minimo, Massimo, Deviazione standard.|  
  
 Per altre informazioni sulle viste di Query Store, vedere la sezione "Viste, funzioni e procedure correlate" di [Monitoraggio delle prestazioni con Query Store](monitoring-performance-by-using-the-query-store.md). 
  
## <a name="query-processing"></a>Elaborazione di query
 Query Store interagisce con la pipeline di elaborazione delle query nei seguenti punti chiave:
  
1.  Quando una query viene compilata per la prima volta, il testo della query e il piano iniziale vengono inviati a Query Store.
  
2.  Quando una query viene ricompilata, il piano viene aggiornato in Query Store. Se viene creato un nuovo piano, Query Store aggiunge la nuova voce del piano per la query e mantiene le precedenti insieme alle relative statistiche di esecuzione.
  
3.  Al momento dell'esecuzione della query, le statistiche di runtime vengono inviate a Query Store. Archivio query mantiene le statistiche aggregate precise per ogni piano che è stato eseguito entro l'intervallo attualmente attivo. 
  
4.  Durante la compilazione e il controllo per le fasi di ricompilazione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina se esiste un piano in Query Store che deve essere applicato per la query attualmente in esecuzione. Se è presente un piano forzato e il piano nella cache delle procedure è diverso dal piano forzato, la query viene ricompilata. È esattamente come se PLAN HINT fosse stato applicato alla query. Questo processo avviene in modo trasparente per l'applicazione dell'utente. 
  
 Il diagramma seguente illustra i punti di integrazione spiegati nei passaggi precedenti:
  
 ![Processo Query Store](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Osservazioni
 Per ridurre al minimo il sovraccarico di I/O, i nuovi dati sono acquisiti in memoria. Le operazioni di scrittura sono messe in coda e scaricate su disco in un secondo momento. Le informazioni relative alle query e ai piani, visualizzate come Archivio piani nel diagramma seguente, vengono scaricate con latenza minima, mentre le statistiche di runtime, visualizzate come Statistiche runtime, sono mantenute in memoria per un periodo di tempo definito con l'opzione `DATA_FLUSH_INTERVAL_SECONDS` dell'istruzione `SET QUERY_STORE`. È possibile usare la finestra di dialogo Query Store di [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] per immettere un valore per **Intervallo di scaricamento dati (minuti)** , che viene convertito internamente in secondi. 
  
 ![Piano del processo Query Store](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 Se si verifica un arresto anomalo del sistema quando si usa il [flag di traccia 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery), Query Store può perdere i dati di runtime raccolti ma non ancora salvati in modo permanente, fino a un intervallo di tempo definito con `DATA_FLUSH_INTERVAL_SECONDS`. Si consiglia il valore predefinito di 900 secondi (15 minuti) che rappresenta un buon compromesso tra le prestazioni di acquisizione delle query e la disponibilità dei dati.
 
 > [!IMPORTANT] 
 > Il limite **Dimensioni massime (MB)** non è necessariamente applicato. Le dimensioni di archiviazione vengono controllate solo quando Query Store scrive i dati su disco. Questo intervallo viene impostato dal valore di **Intervallo di scaricamento dati**. Se Query Store ha violato il limite di dimensioni massime tra i controlli delle dimensioni di archiviazione, passa alla modalità di sola lettura. Se è abilitata la **Modalità di pulizia basata sulle dimensioni**, viene attivato anche il meccanismo di pulizia per applicare il limite di dimensioni massime.
 
 > [!NOTE]
 > In caso di uso intenso della memoria nel sistema, le statistiche di runtime possono essere scaricate su disco prima di quanto definito con `DATA_FLUSH_INTERVAL_SECONDS`.
 
 Durante la lettura dei dati di Query Store, i dati in memoria e su disco sono unificati in modo trasparente. 
 
 Se una sessione viene terminata o in caso di riavvio o arresto anomalo dell'applicazione client, non verranno registrate le statistiche di query. 
  
 ![Informazioni sul piano del processo Query Store](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>Vedere anche
 [Monitoraggio delle prestazioni con Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Procedure consigliate per Query Store](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
