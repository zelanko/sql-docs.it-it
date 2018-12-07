---
title: Amministrare e monitorare Change Data Capture (SQL Server) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fd3fc6793ce2c95bfbb03d80e0413d0b0f6148d1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404986"
---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>Amministrare e monitorare Change Data Capture (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come amministrare ed eseguire il monitoraggio dell'acquisizione dati delle modifiche.  
  
##  <a name="Capture"></a> Processo di acquisizione  
 Il processo di acquisizione viene avviato eseguendo la stored procedure **sp_MScdc_capture_job**senza parametri. Questa stored procedure estrae prima i valori configurati per *maxtrans*, *maxscans*, *continuous*e *pollinginterval* necessari per il processo di acquisizione da msdb.dbo.cdc_jobs. Questi valori configurati vengono poi passati come parametri alla stored procedure **sp_cdc_scan**, usata per chiamare **sp_replcmds** con cui eseguire l'analisi del log.  
  
### <a name="capture-job-parameters"></a>Parametri del processo di acquisizione  
 Per acquisire familiarità con il comportamento del processo di acquisizione, è necessario comprendere come i parametri configurabili vengono usati dalla stored procedure **sp_cdc_scan**.  
  
#### <a name="maxtrans-parameter"></a>Parametro maxtrans  
 Il parametro *maxtrans* specifica il numero massimo di transazioni che possono essere elaborate in un singolo ciclo di analisi del log. Se durante l'analisi il numero di transazioni da elaborare raggiunge tale limite, nell'analisi corrente non viene inclusa alcuna transazione aggiuntiva. Al termine di un ciclo di analisi, il numero di transazioni elaborate sarà sempre minore o uguale a *maxtrans*.  
  
#### <a name="maxscans-parameter"></a>Parametro maxscans  
 Il parametro *maxscans* specifica il numero massimo di tentativi di cicli di analisi per svuotare il log prima dell’uscita (parametro continuous = 0) o dell'esecuzione di un'istruzione WAITFOR (parametro continuous = 1).  
  
#### <a name="continous-parameter"></a>Parametro continous  
 Il parametro *continuous* determina se **sp_cdc_scan** cede il controllo in seguito allo svuotamento del log o all'esecuzione del numero massimo di cicli di analisi (modalità di esecuzione singola). Determina anche se l'esecuzione di **sp_cdc_scan** deve continuare fino a quando non viene arrestata in modo esplicito (modalità continua).  
  
##### <a name="one-shot-mode"></a>Modalità di esecuzione singola  
 In modalità di esecuzione singola il processo di acquisizione chiede a **sp_cdc_scan** di eseguire un numero di analisi pari al valore indicato dal parametro *maxtrans* per provare a svuotare il log ed uscire. Qualsiasi transazione aggiuntiva rispetto al parametro *maxtrans* presente nel log verrà elaborata nelle analisi successive.  
  
 La modalità di esecuzione singola viene utilizzata in test controllati, in cui è noto il volume di transazioni da elaborare e in cui la chiusura automatica del processo al suo completamento costituisce un aspetto vantaggioso. L'utilizzo della modalità di esecuzione singola non è consigliabile in un ambiente di produzione, in quanto t si basa sulla pianificazione del processo per gestire la frequenza di esecuzione del ciclo di analisi.  
  
 In caso di esecuzione in modalità di esecuzione singola, è possibile calcolare un limite superiore per la velocità effettiva del processo di acquisizione, espressa in transazioni al secondo, utilizzando il calcolo seguente:  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 Anche se il tempo necessario per eseguire l'analisi del log e popolare le tabelle delle modifiche non differisce notevolmente da 0, la velocità effettiva media del processo non può superare il valore ottenuto dividendo per il numero di secondi che separano le elaborazioni del log il prodotto del numero massimo di transazioni consentite per una singola analisi per il numero massimo di analisi consentite.  
  
 Se è necessario utilizzare la modalità di esecuzione singola per regolare l'analisi del log, il numero di secondi tra le elaborazioni del log deve essere determinato dalla pianificazione del processo. Se si desidera ottenere questo tipo di comportamento, l'esecuzione del processo di acquisizione in modalità continua rappresenta un metodo migliore per gestire la ripianificazione dell'analisi del log.  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>Modalità continua e intervallo di polling  
 In modalità continua il processo di acquisizione richiede l'esecuzione continua di **sp_cdc_scan** . In questo modo, la stored procedure può gestire il proprio ciclo di attesa fornendo non solo i valori per maxtrans e maxscans ma anche un valore per il numero di secondi tra le elaborazioni del log (intervallo di polling). Dal momento che viene eseguito in questa modalità, il processo di acquisizione rimane attivo, eseguendo un'istruzione **WAITFOR** tra le analisi del log.  
  
> [!NOTE]  
>  Quando il valore dell'intervallo di polling è maggiore di 0, il limite superiore relativo alla velocità effettiva per il processo ricorrente in modalità di esecuzione singola viene applicato anche all'operazione del processo in modalità continua. Di conseguenza, la divisione di (*maxtrans* \* *maxscans*) per un intervallo di polling diverso da zero comporterà l'applicazione di un limite superiore per il numero medio di transazioni che possono essere elaborate dal processo di acquisizione.  
  
### <a name="capture-job-customization"></a>Personalizzazione del processo di acquisizione  
 Per il processo di acquisizione è possibile applicare logica aggiuntiva per determinare se una nuova analisi debba iniziare immediatamente o se venga imposta una sospensione prima di avviare una nuova analisi anziché basarsi su un intervallo di polling fisso. La scelta può essere basata solo sull'ora del giorno, applicando eventualmente sospensioni prolungate durante i periodi di attività massima, e prevedere anche il passaggio a un intervallo di polling pari a zero alla fine del giorno quando è importante completare l'elaborazione giornaliera e preparare le esecuzioni notturne. Può inoltre essere necessario monitorare lo stato del processo di acquisizione per determinare il momento in cui tutte le transazioni di cui è stato eseguito il commit entro mezzanotte sono state sottoposte ad analisi e inserite nelle tabelle delle modifiche. Ciò consente il completamento del processo di acquisizione, che verrà riavviato in base a una pianificazione giornaliera. Sostituendo la chiamata a **sp_cdc_scan** da parte del passaggio del processo recapitato con una chiamata a un wrapper scritto dall'utente per **sp_cdc_scan**, è possibile ottenere un comportamento molto personalizzato con un minimo sforzo aggiuntivo.  
  
##  <a name="Cleanup"></a> Processo di pulizia  
 In questa sezione vengono fornite informazioni sul funzionamento del processo di pulizia di Change Data Capture.  
  
### <a name="structure-of-the-cleanup-job"></a>Struttura del processo di pulizia  
 Change Data Capture utilizza una strategia di pulizia basata su memorizzazione per gestire le dimensioni delle tabelle delle modifiche. Il meccanismo di pulizia è costituito da un processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di [!INCLUDE[tsql](../../includes/tsql-md.md)] Agent creato durante l'abilitazione della prima tabella di database. Un singolo processo di pulizia gestisce la pulizia per tutte le tabelle delle modifiche del database e applica lo stesso valore di memorizzazione a tutte le istanze di acquisizione definite.  
  
 Il processo di pulizia viene avviato eseguendo la stored procedure **sp_MScdc_cleanup_job**senza parametri. Questa stored procedure estrae prima i valori di memorizzazione e soglia configurati per il processo di pulizia da **msdb.dbo.cdc_jobs**. Il valore di memorizzazione viene utilizzato per calcolare un nuovo limite minimo per le tabelle delle modifiche. Il numero di minuti specificato viene sottratto dal valore *msdb.dbo.cdc_jobs* massimo della tabella **cdc.lsn_time_mapping** per ottenere il nuovo valore minimo espresso come valore datetime. La tabella CDC.lsn_time_mapping viene quindi usata per convertire questo valore datetime in un valore **lsn** corrispondente. Se più voci della tabella condividono la stessa ora di esecuzione del commit, come nuovo limite minimo viene scelto il valore **lsn** corrispondente alla voce associata al valore **lsn** minore. Il valore **lsn** viene passato a **sp_cdc_cleanup_change_tables** per rimuovere le voci dalle tabelle delle modifiche del database.  
  
> [!NOTE]  
>  L'utilizzo dell'ora di esecuzione del commit della transazione recente come base per il calcolo del nuovo limite minimo offre il vantaggio di poter mantenere le modifiche nelle tabelle delle modifiche per il tempo specificato. Questa situazione si verifica anche quando è in esecuzione il processo di acquisizione sottostante. Tutte le voci associate alla stessa ora del commit del limite minimo corrente continuano a essere rappresentate all'interno delle tabelle delle modifiche scegliendo il valore **lsn** minore associato all'ora del commit condivisa per il limite minimo effettivo.  
  
 Quando viene eseguita una pulizia, il limite minimo per tutte le istanze di acquisizione viene inizialmente aggiornato in una singola transazione. Viene quindi effettuato il tentativo di rimozione delle voci obsolete dalle tabelle delle modifiche e dalla tabella cdc.lsn_time_mapping. Il valore soglia configurabile limita il numero di voci eliminate in ogni singola istruzione. La mancata esecuzione dell'eliminazione in una singola tabella non impedirà il tentativo di eliminazione nelle altre.  
  
### <a name="cleanup-job-customization"></a>Personalizzazione del processo di pulizia  
 Per il processo di pulizia, la possibilità di personalizzazione consiste nella strategia utilizzata per determinare le voci delle tabelle delle modifiche da ignorare. L'unica strategia supportata nel processo di pulizia è basata sul tempo. In questa situazione, il nuovo limite minimo viene calcolato sottraendo il periodo di memorizzazione consentito dall'ora di esecuzione del commit dell'ultima transazione elaborata. Dato che le procedure di pulizia sottostanti sono basate su **lsn** anziché sul tempo, è possibile usare qualsiasi strategia per determinare il valore **lsn** più basso da mantenere nelle tabelle di modifica. Solo alcuni di questi valori sono rigorosamente basati sul tempo. È possibile, ad esempio, utilizzare le informazioni sui client come valida alternativa in caso di mancata esecuzione dei processi a valle che richiedono l'accesso alle tabelle delle modifiche. Anche se la strategia predefinita applica lo stesso valore **lsn** per pulire tutte le tabelle delle modifiche dei database, è possibile chiamare la procedura di pulizia sottostante anche per eseguire la pulizia a livello di istanza di acquisizione.  
  
##  <a name="Monitor"></a> Monitoraggio del processo Change Data Capture  
 Il monitoraggio del processo Change Data Capture consente di determinare se le modifiche vengono scritte correttamente e con una latenza ragionevole nelle tabelle delle modifiche. L'esecuzione il monitoraggio può consentire anche di identificare gli errori che si potrebbero verificare. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono incluse due DMV per monitorare Change Data Capture: [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) e [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md).  
  
### <a name="identify-sessions-with-empty-result-sets"></a>Identificazione di sessioni con set di risultati vuoti  
 Ogni riga in sys.dm_cdc_log_scan_sessions rappresenta una sessione di analisi del log, ad eccezione della riga con ID 0. Una sessione di analisi del log è equivalente a un'esecuzione di [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md). Durante una sessione, l'analisi può restituire modifiche o un risultato vuoto. Se il set di risultati è vuoto, la colonna empty_scan_count in sys.dm_cdc_log_scan_sessions è impostata su 1. Se si ottengono set di risultati vuoti consecutivi, ad esempio nel caso in cui il processo di acquisizione viene eseguito in modo continuo, il valore di empty_scan_count nell'ultima riga esistente viene incrementato. Se ad esempio sys.dm_cdc_log_scan_sessions contiene già 10 righe per analisi che hanno restituito modifiche e in una riga sono presenti cinque risultati vuoti, la vista contiene 11 righe. L'ultima riga presenta il valore 5 nella colonna empty_scan_count. Per determinare le sessioni per cui l'analisi è risultata vuota, eseguire la query seguente:  
  
```sql
SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0
```
  
### <a name="determine-latency"></a>Determinazione della latenza  
 La vista a gestione dinamica sys.dm_cdc_log_scan_sessions include una colonna in cui viene registrata la latenza per ogni sessione di acquisizione. Con il termine latenza si definisce il tempo che trascorre tra una transazione, il cui commit viene eseguito in una tabella di origine e l'ultima transazione acquisita, il cui commit viene eseguito nella tabella delle modifiche. La colonna della latenza viene popolata solo per le sessioni attive. Per le sessioni con un valore maggiore di 0 nella colonna empty_scan_count, la colonna della latenza è impostata su 0. La query seguente restituisce la latenza media per le sessioni più recenti:  
  
```sql
SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0
```
  
 È possibile utilizzare i dati della latenza da determinare la velocità con la quale il processo di acquisizione elabora le transazioni. Questi dati dimostrano tutta la loro utilità quando il processo di acquisizione viene eseguito in modo continuo. Se il processo di acquisizione viene eseguito in base a una pianificazione, la latenza può aumentare a causa del tempo che trascorre tra le transazioni di cui viene eseguito il commit nella tabella di origine, con il processo di acquisizione che continua a essere eseguito in base alla pianificazione.  
  
 Un altro importante indicatore di prestazioni del processo di acquisizione è la velocità effettiva. Si tratta del numero medio di comandi al secondo elaborati durante ogni sessione. Per determinare la velocità effettiva di una sessione, dividere il valore presente nella colonna command_count per il valore presente nella colonna della durata. La query seguente restituisce la velocità effettiva media per le sessioni più recenti:  
  
```sql
SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0
```
  
### <a name="use-data-collector-to-collect-sampling-data"></a>Utilizzo dell'agente di raccolta dati per raccogliere dati di campionamento  
 L'agente di raccolta dati disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di raccogliere snapshot di dati da qualsiasi tabella o DMV e compilare un data warehouse contenente dati relativi alle prestazioni. Quando Change Data Capture è abilitato in un database, è possibile raccogliere snapshot delle viste sys.dm_cdc_log_scan_sessions e sys.dm_cdc_errors a intervalli regolari per poterli analizzare. Nella procedura seguente viene impostato un agente di raccolta dati per raccogliere dati di campionamento dalla vista a gestione dinamica sys.dm_cdc_log_scan_sessions.  
  
 **Configurazione della raccolta dati**  
  
1.  Abilitare l'agente di raccolta dati e configurare un data warehouse di gestione. Per altre informazioni, vedere [Gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md).  
  
2.  Eseguire il codice seguente per creare un agente di raccolta personalizzato per Change Data Capture.  
  
    ```sql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @parameters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @parameters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @parameters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]espandere **Gestione**, quindi espandere **Raccolta dati**. Fare clic con il pulsante destro del mouse su **CDC Performance Data Collector**, quindi fare clic su **Avvia set di raccolta dati**.  
  
4.  Nel data warehouse configurato nel passaggio 1 trovare la tabella custom_snapshots.cdc_log_scan_data. In questa tabella viene fornito uno snapshot cronologico di dati dalle sessioni di analisi del log. Questi dati possono essere utilizzati per analizzare nel corso del tempo latenza, velocità effettiva e altri indicatori di prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Tenere traccia delle modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Abilitare e disabilitare Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Usare i dati delle modifiche &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  
