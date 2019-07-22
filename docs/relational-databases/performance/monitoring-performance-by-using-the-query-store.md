---
title: Monitoraggio delle prestazioni con Query Store | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0b0fc97b52f6c79ef14944b3d807ac259dd6727
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018758"
---
# <a name="monitoring-performance-by-using-the-query-store"></a>Monitoraggio delle prestazioni con Query Store
[!INCLUDE[appliesto-ss-asdb-xxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  La funzionalità Archivio query di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra informazioni dettagliate sulle prestazioni e sulla scelta del piano di query. Semplifica la risoluzione dei problemi di prestazioni in quanto consente di individuare rapidamente le variazioni delle prestazioni causate da modifiche nei piani di query. Archivio query acquisisce automaticamente una cronologia delle query, dei piani e delle statistiche di runtime e li conserva per la consultazione. I dati vengono separati in base a intervalli di tempo, consentendo di visualizzare i modelli di utilizzo del database e capire quando sono state apportate modifiche al piano di query nel server. Per configurare l'archivio query, è possibile usare l'opzione [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) . 
  
 Per informazioni sul funzionamento di Query Store nel [!INCLUDE[ssSDS](../../includes/sssds-md.md)] di Azure, vedere [Uso di Query Store nel database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/).  
 
> [!IMPORTANT]
> Se si usa Query Store per informazioni dettagliate sui carichi di lavoro Just-In-Time in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], prevedere l'installazione delle correzioni di scalabilità delle prestazioni in [KB 4340759](https://support.microsoft.com/help/4340759) appena possibile. 
  
##  <a name="Enabling"></a> Abilitazione di Archivio query  
 Per impostazione predefinita, la funzionalità Archivio query non è attiva per i nuovi database.  
  
#### <a name="use-the-query-store-page-in-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Usare la pagina Archivio query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un database e quindi scegliere **Proprietà**.  
  
    > [!NOTE]  
    > È necessaria almeno la versione 16 di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Nella finestra di dialogo **Proprietà database** selezionare la pagina **Archivio query** .  
  
3.  Nella casella **Modalità operativa (richiesta)** selezionare **Lettura/Scrittura**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="use-transact-sql-statements"></a>Usare istruzioni Transact-SQL  
  
Per abilitare l'archivio query, usare l'istruzione **ALTER DATABASE** . Esempio:  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET QUERY_STORE (OPERATION_MODE = READ_WRITE); 
```  
  
Per altre opzioni della sintassi correlate all'archivio query, vedere [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
> [!NOTE]  
> Non è possibile abilitare l'archivio query per il database **master** o **tempdb** .  
 
> [!IMPORTANT]
> Per informazioni sull'abilitazione di Query Store e su come mantenerlo allineato al carico di lavoro, vedere [Procedure consigliate per l'archivio query](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure).
 
## <a name="About"></a> Informazioni presenti in Archivio query  
 I piani di esecuzione per query specifiche in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in genere cambiano nel tempo per motivi diversi, quali modifiche delle statistiche, modifiche dello schema, creazione/eliminazione di indici e così via. Nella cache delle procedure, dove sono archiviati i piani di query memorizzati nella cache, viene archiviato solo il piano di esecuzione più recente. La rimozione dei piani dalla cache dei piani può dipendere anche da problemi di memoria. Di conseguenza, le regressioni delle prestazioni di esecuzione delle query causate da modifiche del piano di esecuzione possono essere rilevanti e richiedere tempo per la risoluzione.  
  
 Dal momento che nell'archivio query vengono mantenuti più piani di esecuzione per ogni query, è possibile applicare i criteri in modo che il processore di query usi un piano di esecuzione specifico per una query. Questo processo viene chiamato utilizzo forzato del piano. Per applicare l'utilizzo forzato del piano in Archivio query, viene usato un meccanismo simile all'hint per la query [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) , che però non richiede modifiche nelle applicazioni utente. Grazie all'utilizzo forzato del piano è possibile risolvere molto rapidamente una regressione delle prestazioni di esecuzione delle query causata da una modifica del piano.  

> [!NOTE]
> Query Store raccoglie i piani per le istruzioni DML come SELECT, INSERT, UPDATE, DELETE, MERGE e BULK INSERT.

 Le **statistiche di attesa** sono un'altra fonte di informazione con le quali è possibile risolvere i problemi di prestazioni in SQL Server. Per molto tempo le statistiche di attesa sono state disponibili solo a livello di istanza, il che rendeva difficile l'esecuzione del backtracking per la query effettiva. In SQL Server 2017 e nel database SQL di Azure è stata aggiunta un'altra dimensione in Query Store che tiene traccia delle statistiche di attesa. 

 La funzionalità Archivio query viene usata in genere negli scenari seguenti:  
  
-   Individuare e correggere rapidamente una regressione delle prestazioni di esecuzione delle query forzando un piano di query precedente. Correggere le query in cui si è verificata di recente una regressione delle prestazioni a causa di modifiche del piano di esecuzione.  
-   Determinare il numero di volte in cui una query è stata eseguita in un determinato intervallo di tempo, in modo da assistere un amministratore di database nella risoluzione dei problemi relativi alle prestazioni delle risorse.  
-   Identificare le prime *n* query (in base al tempo di esecuzione, al consumo della memoria e così via) nelle ultime *x* ore.  
-   Controllare la cronologia dei piani di query per una determinata query.  
-   Analizzare i modelli di utilizzo delle risorse (CPU, I/O e memoria) per un determinato database.  
-   Identificare le prime query n in attesa su risorse. 
-   Comprendere la natura di attesa per una query o un piano in particolare.
  
In Query Store sono contenuti tre archivi:
- Un **archivio piani** per il salvataggio in modo permanente delle informazioni sul piano di esecuzione.     
- a **archivio statistiche runtime**: per il salvataggio in modo permanente delle informazioni sulle statistiche di esecuzione.    
- a **archivio statistiche di attesa**: per il salvataggio in modo permanente delle informazioni sulle statistiche di attesa.     
 
Il numero di piani univoci che è possibile archiviare per una query nell'archivio piani è limitato dall'opzione di configurazione **max_plans_per_query** . Per migliorare le prestazioni, le informazioni vengono scritte negli archivi in modo asincrono. Per ridurre al minimo l'utilizzo dello spazio, le statistiche di esecuzione di runtime nell'archivio delle statistiche di runtime vengono aggregate in un intervallo di tempo fisso. Per visualizzare le informazioni contenute in questi archivi, è possibile eseguire una query sulle viste del catalogo dell'archivio query.  
  
La query seguente restituisce le informazioni sulle query e sui piani inclusi nell'archivio query.  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
INNER JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
INNER JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
##  <a name="Regressed"></a> Usare la funzionalità Query regredite  
Dopo aver abilitato Archivio query, aggiornare la parte del database del riquadro Esplora oggetti per aggiungere la sezione **Archivio query** .  
  
![Struttura ad albero di Query Store di SQL Server 2016 in Esplora oggetti di SSMS](../../relational-databases/performance/media/objectexplorerquerystore.PNG "Struttura ad albero di Query Store di SQL Server 2016 in Esplora oggetti di SSMS")   ![Struttura ad albero di Query Store di SQL Server 2017 in Esplora oggetti di SSMS](../../relational-databases/performance/media/objectexplorerquerystore_sql17.PNG "Struttura ad albero di Query Store di SQL Server 2017 in Esplora oggetti di SSMS") 
  
Selezionare **Query regredite** per aprire il riquadro **Query regredite** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Nel riquadro Query regredite sono visualizzati i piani e le query presenti nell'archivio query. Usare le caselle a discesa nella parte superiore per filtrare le query in base a criteri diversi: **Durata (ms)** (predefinito), Tempo CPU (ms), Letture logiche (KB), Scritture logiche (KB), Letture fisiche (KB), Tempo CLR (ms), DOP, Utilizzo memoria (KB), Conteggio righe, Memoria log usata (KB), Memoria database temporaneo usata (KB) e Tempo di attesa (ms).  
Selezionare un piano per visualizzare il piano di query con interfaccia grafica. Sono disponibili pulsanti che consentono di visualizzare la query di origine, forzare e annullare la forzatura di un piano di query, passare dai formati griglia ai grafici e viceversa, confrontare piani selezionati (se è selezionato più di un piano) e aggiornare la visualizzazione.  
  
![Query regredite di SQL Server 2016 in Esplora oggetti di SSMS](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "Query regredite di SQL Server 2016 in Esplora oggetti di SSMS")  
  
Per forzare un piano, selezionare una query e un piano, quindi fare clic su **Forza piano**. È possibile forzare solo piani che sono stati salvati dalla funzionalità del piano di query e che sono ancora presenti nella relativa cache.

##  <a name="Waiting"></a> Ricerca di query di attesa

A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CTP 2.0 e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], in Query Store sono disponibili le statistiche di attesa per ogni query nel corso del tempo. In Query Store i tipi di attesa sono raggruppati in **categorie di attesa**. In [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md#wait-categories-mapping-table) è disponibile il mapping delle categorie di attesa ai tipi di attesa.

Selezionare **Statistiche di attesa query** per aprire il riquadro **Statistiche di attesa query** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18 o versione successiva. Il riquadro Statistiche di attesa query visualizza un grafico a barre contenente le categorie di attesa principali in Query Store. Usare l'elenco a discesa nella parte superiore per selezionare un criterio di aggregazione per il tempo di attesa: medio, max, min, deviazione standard e **totale** (impostazione predefinita).

 ![Statistiche di attesa query di SQL Server 2017 in Esplora oggetti di SSMS](../../relational-databases/performance/media/query-store-waits.PNG "Statistiche di attesa query di SQL Server 2017 in Esplora oggetti di SSMS")

Selezionare una categoria di attesa facendo clic sulla barra. Verrà visualizzata una vista dettagliata sulla categoria di attesa selezionata. Questo nuovo grafico a barre contiene le query che hanno contribuito a tale categoria di attesa. 
  
 ![Vista dettagliata delle statistiche di attesa query di SQL Server 2017 in Esplora oggetti di SSMS](../../relational-databases/performance/media/query-store-waits-detail.PNG "Vista dettagliata delle statistiche di attesa query di SQL Server 2017 in Esplora oggetti di SSMS")

Usare la casella nella parte superiore per filtrare le query in base a diversi criteri di tempo di attesa per la categoria di attesa selezionata: medio, max, min, deviazione standard e **totale** (impostazione predefinita). Selezionare un piano per visualizzare il piano di query con interfaccia grafica. Sono disponibili pulsanti per visualizzare la query di origine, forzare e annullar e la forzatura di un piano di query e aggiornare la visualizzazione.  

Le **categorie di attesa** raggruppano tipi di attesa diversi in bucket simili per natura. Per le varie categorie di attesa è necessario un'analisi di completamento diversa per risolvere il problema. Per i tipi di attesa della stessa categoria la risoluzione dei problemi è invece molto simile. Specificando la query interessata come prima nelle attese, si indica la parte mancante necessaria a completare le analisi in modo corretto.

Di seguito sono descritti alcuni esempi su come ottenere informazioni dettagliate riguardanti il carico di lavoro prima e dopo aver introdotto le categorie di attesa in Query Store:

|||| 
|-|-|-|  
|Esperienza precedente|Esperienza successiva|Azione|
|Attese di RESOURCE_SEMAPHORE elevate per database|Attese di memoria elevate in Query Store per query specifiche|Individuare le prime query per utilizzo della memoria in Query Store. È probabile che queste query ritardino il successivo l'avanzamento delle query interessate. È consigliabile usare l'hint per la query MAX_GRANT_PERCENT per queste query o per le query interessate.|
|Attese di LCK_M_X elevate per database|Attese di blocco elevate in Query Store per query specifiche|Controllare i testi di query per le query interessate e identificare le entità di destinazione. In Query Store cercare altre query che modificano la stessa entità, che vengono eseguite frequentemente e/o hanno una durata elevata. Dopo aver individuato queste query, provare a modificare la logica dell'applicazione per migliorare la concorrenza, oppure usare un livello di isolamento meno restrittivo.|
|Attese di PAGEIOLATCH_SH elevate per database|Attese di I/O del buffer elevate in Query Store per query specifiche|Individuare le query con un numero elevato di letture fisiche in Query Store. Se corrispondono alle query con attese di I/O elevate, provare a introdurre un indice nell'entità sottostante, in modo da eseguire ricerche anziché analisi e ridurre così al minimo il sovraccarico di I/O delle query.|
|Attese di SOS_SCHEDULER_YIELD elevate per database|Attese di CPU elevate in Query Store per query specifiche|Individuare la prime query per utilizzo CPU in Query Store. Tra queste query identificare quelle in cui la tendenza di utilizzo CPU elevato è correlata ad attese di CPU elevate per le query interessate. Concentrarsi sull'ottimizzazione di queste query: considerare la possibilità di una regressione del piano o la mancanza di un indice.|

##  <a name="Options"></a> Opzioni di configurazione 
Le opzioni seguenti sono disponibili per la configurazione dei parametri dell'archivio query.

*OPERATION_MODE*  
È possibile leggere **READ_WRITE** (impostazione predefinita) o READ_ONLY.  
  
*CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)*  
Configurare l'argomento `STALE_QUERY_THRESHOLD_DAYS` per specificare il numero di giorni per la conservazione dei dati in Query Store. Il valore predefinito è 30. Per l'edizione [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic, l'impostazione predefinita è **7** giorni.
  
*DATA_FLUSH_INTERVAL_SECONDS*  
Determina la frequenza con cui i dati scritti nell'archivio query vengono mantenuti su disco. Per ottimizzare le prestazioni, i dati raccolti dall'archivio query vengono scritti in modo asincrono sul disco. La frequenza con cui si verifica questo trasferimento asincrono è configurabile tramite `DATA_FLUSH_INTERVAL_SECONDS`. Il valore predefinito **900** (15 min).  
  
*MAX_STORAGE_SIZE_MB*  
Consente di configurare le dimensioni massime dell'archivio query. Se i dati in Query Store raggiungono il limite impostato in `MAX_STORAGE_SIZE_MB`, lo stato passa da lettura/scrittura a sola lettura e la raccolta di nuovi dati viene interrotta.  Il valore predefinito è 100 MB. Per l'edizione [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium, il valore predefinito è **1 GB**, mentre per l'edizione [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic, il valore predefinito è **10 MB**.
  
*INTERVAL_LENGTH_MINUTES*  
Determina l'intervallo di tempo in cui vengono aggregati i dati delle statistiche di esecuzione di runtime nell'archivio query. Per ottimizzare l'utilizzo dello spazio, le statistiche di esecuzione di runtime nell'archivio delle statistiche di runtime vengono aggregate in un intervallo di tempo fisso. L'intervallo di tempo predefinito viene configurato tramite `INTERVAL_LENGTH_MINUTES`. Il valore predefinito è **60**. 
  
*SIZE_BASED_CLEANUP_MODE*  
Determina se il processo di pulizia viene attivato automaticamente quando la quantità totale di dati sta per raggiungere le dimensioni massime. Può essere **AUTO** (impostazione predefinita) o OFF.  
  
*QUERY_CAPTURE_MODE*  
Determina se Archivio dati acquisisce tutte le query oppure le query pertinenti in base a conteggio esecuzioni e consumo delle risorse oppure se interrompe l'aggiunta delle nuove query e tiene semplicemente traccia delle query correnti. Può essere **ALL** (acquisire tutte le query), AUTO (ignorare le query poco frequenti e quelle con una durata di compilazione e di esecuzione non significativa) o NONE (arrestare l'acquisizione di nuove query). Il valore predefinito in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) è ALL, mentre in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] di Azure è AUTO.
  
*MAX_PLANS_PER_QUERY*  
Intero che rappresenta il numero massimo di piani mantenuti per ogni query. Il valore predefinito è **200**.  
 
*WAIT_STATS_CAPTURE_MODE*  
Controlla se Query Store acquisisce informazioni sulle statistiche relative all'attesa. Può essere OFF o **ON** (impostazione predefinita).  
 
Per determinare le opzioni correnti dell'archivio query, eseguire una query sulla vista **sys.database_query_store_options** . Per altre informazioni sui valori, vedere [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
Per altre informazioni sull'impostazione di opzioni con istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , vedere [Gestione delle opzioni](#OptionMgmt).  
  
## <a name="Related"></a> Viste, funzioni e procedure correlate  
 È possibile visualizzare e gestire Archivio query con [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oppure usando le viste e le procedure seguenti.  

### <a name="query-store-functions"></a>Funzioni di Query Store  
 Le funzioni facilitano l'uso di Query Store. 
 
||| 
|-|-|  
|[sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)|| 
  
### <a name="query-store-catalog-views"></a>Viste del catalogo di Archivio query  
 Le informazioni su Query Store vengono presentate nelle viste del catalogo.  

||| 
|-|-|  
|[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)|[sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)|  
|[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)|[sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)|  
|[sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|[sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)|  
|[sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)|[sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)|  
  
### <a name="query-store-stored-procedures"></a>Stored procedure di Archivio query  
 Per configurare Query Store vengono usate le stored procedure.  

||| 
|-|-|  
|[sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)|[sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)|  
|[sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)|[sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)|  
|[sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)|[sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)|  
|sp_query_store_consistency_check &#40;Transact-SQL&#41;||  
 
##  <a name="Scenarios"></a> Principali scenari di utilizzo  
  
###  <a name="OptionMgmt"></a> Gestione delle opzioni  
 Questa sezione fornisce alcune linee guida per la gestione della funzionalità Archivio query.  
  
 **Come sapere se la funzionalità Archivio query è attualmente attiva**  
  
 I dati della funzionalità Query Store vengono archiviati nel database utente ed è quindi previsto un limite per le dimensioni, che viene configurato con `MAX_STORAGE_SIZE_MB`. Se i dati in Archivio query raggiungono tale limite, lo stato cambia automaticamente da lettura/scrittura a sola lettura e la raccolta di nuovi dati viene interrotta.  
  
 Eseguire una query su [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) per determinare se la funzionalità Query Store è attualmente attiva e se è in corso la raccolta delle statistiche di runtime.  
  
```sql  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 Lo stato di Archivio query è determinato dalla colonna actual_state. Se è diverso dallo stato previsto, la colonna `readonly_reason` contiene maggiori informazioni.   
Quando le dimensioni di Archivio query superano la quota, la funzionalità passa alla modalità readon_only.  
  
 **Ottenere le opzioni di Archivio query**  
  
 Per informazioni dettagliate sullo stato di Archivio query, eseguire l'istruzione seguente in un database utente.  
  
```sql  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **Impostazione dell'intervallo di Archivio query**  
  
 È possibile ignorare l'intervallo per l'aggregazione delle statistiche di runtime delle query (impostazione predefinita: 60 minuti).  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 > [!NOTE]
 > I valori arbitrari non sono consentiti per `INTERVAL_LENGTH_MINUTES`. Usare uno dei seguenti: 1, 5, 10, 15, 30, 60 o 1440 minuti.  
  
 Il nuovo valore per l'intervallo viene esposto mediante la visualizzazione **sys.database_query_store_options** .  
  
 **Utilizzo dello spazio di Archivio query**  
  
 Per controllare le dimensioni e i limiti correnti di Archivio query, eseguire l'istruzione seguente nel database utente.  
  
```sql  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 Se lo spazio di archiviazione di Archivio query è esaurito, usare l'istruzione seguente per estenderlo.  
  
```sql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **Impostare tutte le opzioni di Archivio query**  
  
 È possibile impostare più opzioni di Archivio query contemporaneamente con un'unica istruzione ALTER DATABASE.  
  
```sql  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000,
    WAIT_STATS_CAPTURE_MODE = ON 
);  
```  
  
 **Pulizia dello spazio**  
  
 Le tabelle interne di Archivio query vengono create nel filegroup PRIMARY durante la creazione del database e tale configurazione non è modificabile in un secondo momento. Se si esaurisce lo spazio, è possibile cancellare dati di Archivio query meno recenti usando l'istruzione seguente.  
  
```sql  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 In alternativa, è possibile cancellare solo dati di query ad hoc perché sono meno rilevanti per le ottimizzazioni query e l'analisi del piano, ma occupano molto spazio.  
  
 **Eliminare query ad-hoc** È possibile eliminare le query che sono state eseguite solo una volta e che risalgono a più di 24 ore prima.  
  
```sql  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 Per la cancellazione dei dati non più necessari, è possibile definire procedure personalizzate con logiche diverse.  
  
 Per rimuovere i dati non necessari, nell'esempio precedente viene usata la stored procedure estesa **sp_query_store_remove_query** . È anche possibile usare:  
  
-   **sp_query_store_reset_exec_stats** per cancellare le statistiche di runtime per un piano specifico.  
-   **sp_query_store_remove_plan** per rimuovere un singolo piano.  
 
  
###  <a name="Peformance"></a> Controllo delle prestazioni e risoluzione dei problemi  
 Archivio query conserva la cronologia delle metriche relative a compilazione e runtime per tutte le esecuzioni delle query e questo consente di ottenere facilmente informazioni sul carico di lavoro.  
  
 **Ultime *n* query eseguite sul database?**  
  
```sql  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **Numero di esecuzioni per ogni query.**  
  
```sql  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **Numero di query con il tempo medio di esecuzione maggiore nell'ultima ora.**  
  
```sql  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **Numero di query con il maggior numero medio di letture I/O fisiche nelle ultime 24 ore, con il numero medio di righe e di esecuzioni corrispondente.**  
  
```sql  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **Query con più piani.** Queste query sono particolarmente interessanti perché sono candidati a regressioni in seguito alla modifica del piano selezionato. La query seguente consente di identificare queste query unitamente a tutti i piani:  
  
```sql  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **Query in cui si è verificata di recente una regressione delle prestazioni (confrontando momenti diversi).** L'esempio di query seguente restituisce tutte le query in cui il tempo di esecuzione è raddoppiato nelle ultime 48 ore in seguito alla modifica del piano selezionato. La query confronta tutti gli intervalli delle statistiche di runtime affiancandoli.  
  
```sql  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 Per visualizzare tutte le regressioni delle prestazioni, non solo quelle correlate alla modifica del piano selezionato, è sufficiente rimuovere la condizione `AND p1.plan_id <> p2.plan_id` dalla query precedente.  

 **Query che rimangono più a lungo in attesa**
Questa query restituirà le prime 10 query che rimangono più a lungo in attesa. 
 
 ```sql 
  SELECT TOP 10
    qt.query_text_id,
    q.query_id,
    p.plan_id,
    sum(total_query_wait_time_ms) AS sum_total_wait_ms
FROM sys.query_store_wait_stats ws
JOIN sys.query_store_plan p ON ws.plan_id = p.plan_id
JOIN sys.query_store_query q ON p.query_id = q.query_id
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
GROUP BY qt.query_text_id, q.query_id, p.plan_id
ORDER BY sum_total_wait_ms DESC
 ```
 
 **Query in cui si è verificata di recente una regressione delle prestazioni (confrontando esecuzioni recenti e della cronologia).** La query successiva confronta le esecuzioni di query in base ai periodi di esecuzione. In questo specifico esempio la query confronta le esecuzioni nel periodo recente (1 ora) con il periodo della cronologia (ultimo giorno) e identifica quelle che hanno introdotto `additional_duration_workload`. Questa metrica viene ottenuta moltiplicando la differenza tra l'esecuzione media recente e quella media della cronologia e il numero delle esecuzioni recenti. Rappresenta in effetti la quantità di esecuzioni recenti con durata aggiuntiva introdotte rispetto alla cronologia:  
  
```sql  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time <= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time <= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time <= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time <= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
###  <a name="Stability"></a> Misure per garantire la stabilità delle prestazioni di esecuzione delle query  
Per le query eseguite più volte è possibile notare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa piani diversi che comportano durate e utilizzi diversi delle risorse. Archivio query consente di rilevare il momento in cui si verifica una regressione delle prestazioni di esecuzione delle query e di determinare il piano ottimale in un periodo di interesse. È quindi possibile forzare il piano ottimale per le future esecuzioni delle query.  
  
È anche possibile identificare incoerenze nelle prestazioni di una query con parametri (impostati sia automaticamente che manualmente). Tra i diversi piani è possibile identificare quello più rapido e adatto per tutti o per la maggior parte dei valori di parametro e forzarne l'uso in modo da garantire prestazioni prevedibili per un ampio numero di scenari utente.  
  
### <a name="force-a-plan-for-a-query-apply-forcing-policy"></a>Forzare un piano per una query (applicando criteri di utilizzo forzato)

Quando si forza un piano per una determinata query, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prova a forzare il piano in Query Optimizer. Se l'uso forzato del piano ha esito negativo, viene generato un XEvent e a query optimizer viene richiesto di ottimizzare in modo normale.

```sql  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
Se si usa **sp_query_store_force_plan** , è possibile forzare solo piani che sono stati registrati da Archivio query come piani per tale query. In altre parole, gli unici piani disponibili per una query sono quelli già usati per eseguire tale query mentre Archivio query era attivo.  

#### <a name="a-namectp23a-plan-forcing-support-for-fast-forward-and-static-cursors"></a><a name="ctp23"><a/> Supporto dell'uso forzato del piano per cursori fast forward e statici
  
Query Store di [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3 supporta la possibilità di forzare i piani di esecuzione query per i cursori T-SQL e API fast forward e statici. L'uso forzato è ora supportato tramite `sp_query_store_force_plan` o tramite i report di Query Store in SQL Server Management Studio.

### <a name="remove-plan-forcing-for-a-query"></a>Rimuovere l'utilizzo forzato del piano per una query

Per impiegare di nuovo Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per calcolare il piano di query ottimale, usare **sp_query_store_unforce_plan** per annullare l'utilizzo forzato del piano selezionato per la query.  
  
```sql  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  



## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate per l'archivio query](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Uso di Archivio query con OLTP in-memoria](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Scenari di utilizzo dell'Archivio query](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [Come Archivio query raccoglie i dati](../../relational-databases/performance/how-query-store-collects-data.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitoraggio e ottimizzazione delle prestazioni](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [Aprire Monitoraggio attività &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Statistiche sulle query dinamiche](../../relational-databases/performance/live-query-statistics.md)   
 [Monitoraggio attività](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Uso dell'archivio query nel database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  
