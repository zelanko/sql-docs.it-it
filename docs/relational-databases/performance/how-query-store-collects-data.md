---
title: Modalità di raccolta dei dati dell'archivio query | Microsoft Docs
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
ms.openlocfilehash: 83fbc6c183216cedcbb664a0c3a2e3a9337e1513
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946775"
---
# <a name="how-query-store-collects-data"></a>Come Archivio query raccoglie i dati
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Archivio query funziona come un' **utilità di traccia eventi** che raccoglie costantemente informazioni di compilazione e runtime correlate alle query e ai piani. I dati relativi alle query sono resi persistenti nelle tabelle interne e presentati agli utenti mediante una serie di viste.  
  
## <a name="views"></a>Viste  
 Il diagramma seguente mostra le viste di Archivio query e le loro relazioni logiche, con le informazioni della fase di compilazione presentate come entità blu:  
  
 ![query-store-process-2views](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**Descrizioni delle viste**  
  
|Vista|Descrizione|  
|----------|-----------------|  
|**sys.query_store_query_text**|Presenta i testi delle singole query univoche eseguite sul database. I commenti e gli spazi prima e dopo il testo della query vengono ignorati. I commenti e gli spazi all'interno del testo non vengono ignorati. Ogni istruzione del batch genera una voce diversa nell'elenco dei testi di query.|  
|**sys.query_context_settings**|Presenta combinazioni univoche di impostazioni che influiscono sul piano e con cui sono eseguite le query. Lo stesso testo di query eseguito con impostazioni diverse che influiscono sul piano genera voci di query separate in Archivio query in quanto `context_settings_id` fa parte della chiave della query.|  
|**sys.query_store_query**|Voci di query che vengono monitorate e forzate separatamente nell'Archivio query. Un singolo testo di query può generare più voci di query se viene eseguito con impostazioni di contesto diverse o se viene eseguito all'esterno anziché all'interno di moduli [!INCLUDE[tsql](../../includes/tsql-md.md)] diversi, ovvero stored procedure, trigger e così via.|  
|**sys.query_store_plan**|Presenta il piano stimato per la query con le statistiche della fase di compilazione. Il piano archiviato è equivalente al piano che si otterrebbe usando `SET SHOWPLAN_XML ON`.|  
|**sys.query_store_runtime_stats_interval**|Archivio query divide il tempo in finestre temporali (intervalli) generate automaticamente e archivia le statistiche aggregate per tale intervallo per ogni piano eseguito. La dimensione dell'intervallo è controllata dall'opzione di configurazione Intervallo raccolta statistiche (in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) o `INTERVAL_LENGTH_MINUTES` usando [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**sys.query_store_runtime_stats**|Statistiche di runtime aggregate per i piani eseguiti. Tutte le metriche acquisite sono espresse sotto forma di 4 funzioni statistiche: Media, Minimo, Massimo, Deviazione standard.|  
  
 Per altre informazioni sulle viste di Query Store, vedere la sezione **Viste, funzioni e procedure correlate** di [Monitoraggio delle prestazioni con Query Store](monitoring-performance-by-using-the-query-store.md).  
  
## <a name="query-processing"></a>Elaborazione delle query  
 Archivio query interagisce con la pipeline di elaborazione delle query nei seguenti punti chiave:  
  
1.  Quando la query viene compilata per la prima volta, il testo della query e il piano iniziale vengono inviati ad Archivio query  
  
2.  Quando la query viene ricompilata, il piano viene aggiornato in Archivio query. Se viene creato un nuovo piano, Archivio query aggiunge la nuova voce di piano per la query, mantenendo le precedenti insieme alle relative statistiche di esecuzione.  
  
3.  Al momento dell'esecuzione della query, le statistiche di runtime vengono inviate ad Archivio query. Archivio query mantiene le statistiche aggregate precise per ogni piano che è stato eseguito entro l'intervallo attualmente attivo.  
  
4.  Durante la compilazione e il controllo per le fasi di ricompilazione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina se esiste un piano in Archivio query che deve essere applicato per la query attualmente in esecuzione. Se è presente un piano forzato e il piano nella cache delle procedure è diverso dal piano forzato, la query viene ricompilata, esattamente come se fosse stato applicato PLAN HINT alla query. Questo processo avviene in modo trasparente per l'applicazione dell'utente.  
  
 Il diagramma seguente illustra i punti di integrazione illustrati in precedenza:  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 Per ridurre al minimo il sovraccarico di I/O, i nuovi dati sono acquisiti in memoria. Le operazioni di scrittura sono messe in coda e scaricate sul disco in un secondo momento. Le informazioni relative alle query e ai piani (Archivio piano nel diagramma riportato di seguito) vengono scaricate con latenza minima, mentre le statistiche di runtime (Statistiche runtime) sono mantenute in memoria per un periodo di tempo definito con l'opzione `DATA_FLUSH_INTERVAL_SECONDS` dell'istruzione `SET QUERY_STORE` . La finestra di dialogo Archivio query di SSMS consente di immettere il valore **Intervallo di scaricamento dati (minuti)** , che viene convertito in secondi.  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 In caso di arresto anomalo del sistema, Query Store può perdere i dati di runtime fino alla quantità definita con `DATA_FLUSH_INTERVAL_SECONDS`. Il valore predefinito di 900 secondi (15 minuti) rappresenta un punto di equilibrio ottimale tra le prestazioni di acquisizione delle query e la disponibilità dei dati.  
In caso di uso intenso della memoria nel sistema, le statistiche di runtime possono essere scaricate su disco prima di quanto definito con `DATA_FLUSH_INTERVAL_SECONDS`.  
Durante la lettura dei dati di Archivio query, i dati in memoria e su disco sono unificati in modo trasparente.
Se una sessione viene terminata o in caso di riavvio o arresto anomalo dell'applicazione client, non verranno registrate le statistiche di query.  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Procedure consigliate per l'archivio query](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
