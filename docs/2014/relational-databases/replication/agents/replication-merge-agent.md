---
title: Agente merge repliche | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Merge Agent, executables
- Merge Agent, parameter reference
- agents [SQL Server replication], Merge Agent
- command prompt [SQL Server replication]
ms.assetid: fe1e7f60-b0c8-45e9-a5e8-4fedfa73d7ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec21ff98d49cff26bde48452a30fd347c23782fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63216005"
---
# <a name="replication-merge-agent"></a>Agente merge repliche
  Agente merge repliche è un eseguibile dell'utilità che consente di applicare lo snapshot iniziale incluso nelle tabelle di database ai Sottoscrittori. Consente inoltre di unire le modifiche ai dati incrementali apportate nel server di pubblicazione dopo la creazione dello snapshot iniziale e di riconciliare i conflitti in base alle regole configurate oppure utilizzando un sistema di risoluzione personalizzato.  
  
> [!NOTE]  
>  I parametri possono essere specificati in qualsiasi ordine. Quando i parametri facoltativi non vengono specificati, vengono usati i valori delle impostazioni predefinite del Registro di sistema nel computer locale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      replmerg [-?]   
-Publisherserver_name[\instance_name]  
-PublisherDBpublisher_database-Publicationpublication-Subscriberserver_name[\instance_name]  
-SubscriberDBsubscriber_database  
[-AltSnapshotFolderalt_snapshot_folder_path]  
[-Continuous]  
[-DefinitionFiledef_path_and_file_name]  
[-DestThreadsnumber_of_destination_threads]  
[-Distributorserver_name[\instance_name]]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-DownloadGenerationsPerBatchdownload_generations_per_batch]  
[-DownloadReadChangesPerBatchdownload_read_changes_per_batch]  
[-DownloadWriteChangesPerBatchdownload_write_changes_per_batch]  
[-DynamicSnapshotLocationdynamic_snapshot_location]  
[-EncryptionLevel [0|1|2]]  
[-ExchangeType [1|2|3]]  
[-FastRowCount [0|1]]  
[-FileTransferType [0|1]]  
[-ForceConvergenceLevel [0|1|2 (Publisher|Subscriber|Both)]]  
[-FtpAddressftp_address]  
[-FtpPasswordftp_password]  
[-FtpPortftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostnamehost_name]  
[-InteractiveResolution [0|1]]  
[-InternetLogininternet_login]  
[-InternetPasswordinternet_password]  
[-InternetProxyLogininternet_proxy_login]  
[-InternetProxyPasswordinternet_proxy_password]  
[-InternetProxyServerinternet_proxy_server]  
[-InternetSecurityMode [0|1]]  
[-InternetTimeoutinternet_timeout]  
[-InternetURL internet_url]  
[-KeepAliveMessageIntervalkeep_alive_message_interval_seconds]  
[-LoginTimeOutlogin_time_out_seconds]  
[-MakeGenerationIntervalmake_generation_interval_seconds]  
[-MaxBcpThreadsnumber_of_threads]  
[-MaxDownloadChangesnumber_of_download_changes]  
[-MaxUploadChangesnumber_of_upload_changes]  
[-MetadataRetentionCleanup [0|1]]  
[-Output]  
[-OutputVerboseLevel [0|1|2]]  
[-ParallelUploadDownload [0|1]]  
[-PacketSizepacket_size]   
[-PollingIntervalpolling_interval]  
[-ProfileNameprofile_name]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-PublisherLoginpublisher_login]  
[-PublisherPassword publisher_password]  
[-PublisherSecurityMode [0|1]]  
[-QueryTimeOutquery_time_out_seconds]  
[-SrcThreadsnumber_of_source_threads]  
[-StartQueueTimeoutstart_queue_timeout_seconds]  
[-SubscriberConflictClean [0|1]]  
[-SubscriberDatabasePathsubscriber_path]  
[-SubscriberDBAddOption [0|1|2|3]]  
[-SubscriberLoginsubscriber_login]  
[-SubscriberPasswordsubscriber_password   
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|2|3|4|5|6|7|8|9]]  
[-SubscriptionType [0|1|2]]  
[-SyncToAlternate [0|1]  
[-UploadGenerationsPerBatchupload_generations_per_batch]  
[-UploadReadChangesPerBatchupload_read_changes_per_batch]  
[-UploadWriteChangesPerBatchupload_write_changes_per_batch]  
[-UseInprocLoader]  
[-Validate [0|1|2|3]]  
[-ValidateIntervalvalidate_interval]  
```  
  
## <a name="arguments"></a>Argomenti  
 **-?**  
 Stampa tutti i parametri disponibili.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 Nome del server di pubblicazione. Specificare *server_name* per l'istanza predefinita di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Specificare _server_name_ **\\** _instance_name_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server.  
  
 **-PublisherDB** _publisher_database_  
 Nome del database del server di pubblicazione.  
  
 **-Publication** _publication_  
 Nome della pubblicazione. Questo parametro è valido solo se la pubblicazione è configurata in modo che sia sempre disponibile uno snapshot per le sottoscrizioni nuove o reinizializzate.  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 Nome del Sottoscrittore. Specificare *server_name* per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Specificare _server_name_ **\\** _instance_name_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server.  
  
 **-SubscriberDB** _subscriber_database_  
 Nome del database Sottoscrittore.  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 Percorso della cartella che contiene lo snapshot iniziale per una sottoscrizione.  
  
 **-Continuous**  
 Specifica se l'agente tenta di eseguire continuamente il polling delle transazioni replicate. Se specificato, l'agente esegue il polling delle transazioni replicate dall'origine in base agli intervalli di polling, anche se non vi sono transazioni in sospeso.  
  
 **-DestThreads** _number_of_destination_threads_  
 Specifica il numero di thread di destinazione utilizzati dall'agente di merge per applicare le modifiche nella destinazione. La destinazione è costituita dal server di pubblicazione durante il caricamento e dal Sottoscrittore durante il download. Il valore predefinito è 4.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 Percorso del file di definizione dell'agente. Un file di definizione dell'agente contiene argomenti del prompt dei comandi per l'agente. Il contenuto del file viene analizzato come file eseguibile. Utilizzare virgolette doppie (") per specificare valori dell'argomento contenenti caratteri arbitrari.  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 Nome del database di distribuzione. Specificare *server_name* per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Specificare _server_name_ **\\** _instance_name_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Per la distribuzione (push) del database di distribuzione, per impostazione predefinita viene utilizzato il nome dell'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel computer locale.  
  
 **-DistributorLogin** _distributor_login_  
 Nome dell'account di accesso del database di distribuzione.  
  
 **-DistributorPassword** _distributor_password_  
 Password del database di distribuzione.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Specifica la modalità di sicurezza del database di distribuzione. Un valore **0** indica la modalità di autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (impostazione predefinita), mentre un valore **1** indica la modalità di autenticazione di Windows.  
  
 **-DownloadGenerationsPerBatch** _download_generations_per_batch_  
 Numero di generazioni da elaborare in un singolo batch durante il download delle modifiche dal server di pubblicazione al Sottoscrittore. Una generazione è definita come un gruppo logico di modifiche per articolo. Il valore predefinito per un collegamento di comunicazione affidabile è 100. Il valore predefinito per un collegamento di comunicazione non affidabile è 10.  
  
 **-DownloadReadChangesPerBatch** _download_read_changes_per_batch_  
 Numero di modifiche da leggere in un singolo batch durante il download delle modifiche dal server di pubblicazione al Sottoscrittore. Il valore predefinito è 100.  
  
 **-DownloadWriteChangesPerBatch** _download_write_changes_per_batch_  
 Numero di modifiche da applicare in un singolo batch durante il download delle modifiche dal server di pubblicazione al Sottoscrittore. Il valore predefinito è 100.  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 Posizione dei file di snapshot dei dati filtrati quando nella pubblicazione vengono utilizzati filtri di riga con parametri.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Livello di crittografia SSL (Secure Sockets Layer) utilizzato dall'agente di merge quando vengono stabilite le connessioni.  
  
|Valore di EncryptionLevel|Descrizione|  
|---------------------------|-----------------|  
|**0**|Specifica che SSL non viene utilizzato.|  
|**1**|Specifica che SSL viene utilizzato, ma l'agente non verifica che il certificato server SSL sia firmato da un'autorità emittente attendibile.|  
|**2**|Specifica che SSL viene utilizzato e che il certificato viene verificato.|  

 > [!NOTE]  
 >  Un certificato SSL valido è definito con un nome di dominio completo del Server SQL. Affinché l'agente possa connettersi correttamente quando si imposta - EncryptionLevel su 2, creare un alias nel Server SQL locale. Il parametro 'Nome alias' deve corrispondere al nome del server e il parametro 'Server' deve essere impostato sul nome completo dell'istanza di SQL Server.
  
 Per altre informazioni, vedere [la sicurezza della replica di SQL Server](../security/view-and-modify-replication-security-settings.md).  
  
 **-ExchangeType** [ **1**| **2**| **3**]  
 > [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Per limitare il caricamento, utilizzare in alternativa `@subscriber_upload_options` di `sp_addmergearticle`.  
  
 Specifica il tipo di scambio di dati durante la sincronizzazione. I possibili valori sono i seguenti:  
  
|Valore di ExchangeType|Descrizione|  
|------------------------|-----------------|  
|**1**|L'agente deve caricare le modifiche ai dati dal Sottoscrittore al server di pubblicazione.|  
|**2**|L'agente deve eseguire il download delle modifiche ai dati dal server di pubblicazione al Sottoscrittore.|  
|**3** (valore predefinito)|L'agente deve prima caricare le modifiche ai dati dal Sottoscrittore al server di pubblicazione, quindi eseguirne il download dal server di pubblicazione al Sottoscrittore. È necessario utilizzare questa opzione con la sincronizzazione Web.|  
  
 Gli articoli di solo download consentono di controllare il comportamento della sincronizzazione dei singoli articoli in una pubblicazione e possono offrire un vantaggio a livello di prestazioni. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 Se si utilizza `ExchangeType` per separare la fase di caricamento e download della replica di tipo merge in sessioni distinte, è necessario prima eseguire l'agente di merge con `ExchangeType` impostato su 1 e poi eseguire nuovamente l'agente di merge con il valore 2. L'esito negativo dell'esecuzione dell'agente di merge per entrambi i parametri causa l'eliminazione dei metadati e la rinizializzazione della sottoscrizione senza caricamento.  
  
 **-FastRowCount** [**0**|**1**]  
 Specifica il tipo di metodo di calcolo del conteggio delle righe che deve essere utilizzato per la convalida mediante il conteggio delle righe. Un valore **1** (impostazione predefinita) indica il metodo rapido. Un valore **0** indica il metodo di conteggio delle righe completo.  
  
 **-FileTransferType** [**0**|**1**]  
 Specifica il tipo di trasferimento di file. Un valore **0** indica UNC (Universal Naming Convention), mentre un valore **1** indica FTP (File Transfer Protocol).  
  
 **-ForceConvergenceLevel** [**0**|**1**|**2** ( **Publisher**| **Subscriber**| **Both**)]  
 Specifica il livello di convergenza che l'agente di merge deve utilizzare. I possibili valori sono i seguenti:  
  
|Valore di ForceConvergenceLevel|Descrizione|  
|---------------------------------|-----------------|  
|**0** (predefinito)|Valore predefinito. Esegue un'operazione di merge standard senza convergenza aggiuntiva.|  
|**1**|Forza la convergenza per tutte le generazioni.|  
|**2**|Forza la convergenza per tutte le generazioni e corregge le derivazioni danneggiate. Quando si specifica questo valore, specificare dove devono essere corrette le derivazioni, ovvero nel server di pubblicazione, nel Sottoscrittore o in entrambi.|  
  
 **-FtpAddress** _ftp_address_  
 Indirizzo di rete del servizio FTP per il database di distribuzione. Quando non è specificato, viene utilizzato **Distributor** .  
  
 **-FtpPassword** _ftp_password_  
 Password utente utilizzata per la connessione al servizio FTP.  
  
 **-FtpPort** _ftp_port_  
 Numero di porta del servizio FTP per il database di distribuzione. Quando non è specificato, viene utilizzato il numero di porta predefinito per il servizio FTP, ovvero 21.  
  
 **-FtpUserName** _ftp_user_name_  
 Nome utente utilizzato per la connessione al servizio FTP. Quando non è specificato, viene utilizzato anonymous.  
  
 **-HistoryVerboseLevel** [**1**|**2**|**3**]  
 Specifica la quantità di cronologia registrata durante un'operazione di unione. Per ridurre al minimo l'effetto della registrazione della cronologia sulle prestazioni, selezionare **1**.  
  
|Valore di HistoryVerboseLevel|Descrizione|  
|-------------------------------|-----------------|  
|**0**|Registra il messaggio di stato dell'agente finale, i dettagli di sessione finali ed eventuali errori.|  
|**1**|Registra i dettagli di sessione incrementali a ogni stato della sessione, inclusa la percentuale di completamento, oltre al messaggio di stato dell'agente finale, ai dettagli di sessione finali e a eventuali errori.|  
|**2**|Valore predefinito. Registra sia i dettagli di sessione incrementali a ogni stato della sessione che i dettagli di sessione a livello di articolo, inclusa la percentuale di completamento, oltre al messaggio di stato dell'agente finale, ai dettagli di sessione finali e a eventuali errori. Vengono inoltre registrati i messaggi di stato dell'agente.|  
|**3**|Equivale a **-HistoryVerboseLevel** = **2**, ad eccezione del fatto che viene registrato un numero maggiore di messaggi di stato dell'agente.|  
  
 **-Hostname** _host_name_  
 Nome di rete del computer locale. Il valore predefinito è il nome del computer locale.  
  
 **-InteractiveResolution** [**0**|**1**]  
 Specifica se viene utilizzata la risoluzione dei conflitti interattiva quando si verifica un conflitto durante la sincronizzazione. Il valore predefinito è **0**, che indica che la risoluzione dei conflitti interattiva non viene utilizzata.  
  
 **-InternetLogin** _internet_login_  
 Specifica il nome di accesso utilizzato per la connessione a una DLL ISAPI del listener per la replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che richiede l'autenticazione.  
  
 **-InternetPassword** _internet_password_  
 Specifica la password utilizzata per la connessione a una DLL ISAPI del listener per la replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che richiede l'autenticazione.  
  
 **-InternetProxyLogin**  *internet_proxy_login*  
 Specifica il nome di accesso utilizzato per la connessione a un server proxy, definito in *internet_proxy_server*, che richiede l'autenticazione.  
  
 **-InternetProxyPassword** *internet_proxy_password*  
 Specifica la password utilizzata per la connessione a un server proxy, definito in *internet_proxy_server*, che richiede l'autenticazione.  
  
 **-InternetProxyServer**  *internet_proxy_server*  
 Specifica il server proxy da utilizzare per l'accesso alla risorsa HTTP specificata in *internet_url*.  
  
 **-InternetSecurityMode** [**0**|**1**]  
 Specifica la modalità di sicurezza di IIS da utilizzare per la connessione al server Web durante la sincronizzazione Web. Un valore **0** indica l'autenticazione di base, mentre un valore **1** indica l'autenticazione integrata di Windows (impostazione predefinita).  
  
 **-InternetTimeout** _internet_timeout_  
 Numero di secondi prima che si verifichi il timeout di una connessione alla DLL ISAPI del listener per la replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-InternetURL** _internet_url_  
 Specifica l'URL utilizzato per la connessione alla DLL ISAPI del listener per la replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . È necessario specificare questa proprietà.  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 Numero di secondi prima che il thread per la cronologia controlli se una delle connessioni esistenti è in attesa di una risposta dal server. Questo valore può essere ridotto per evitare che l'agente di controllo contrassegni l'agente di merge come sospetto in caso di esecuzione di un batch con esecuzione prolungata. Il valore predefinito è **300** secondi.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 Numero di secondi prima del timeout di accesso. Il valore predefinito è **15** secondi.  
  
 **-MakeGenerationInterval** _make_generation_interval_seconds_  
 Numero di secondi di attesa tra la creazione di generazioni, o batch di modifiche, per il download nel client. Il valore predefinito è **1** secondo.  
  
 Makegeneration è il processo che prepara il download delle modifiche del server di pubblicazione nei Sottoscrittori e può rappresentare un collo di bottiglia per le prestazioni durante i download. Se è stato già eseguito all'interno dell'intervallo specificato da **- MakeGenerationInterval**, il processo viene ignorato per la sessione di sincronizzazione corrente. Questa operazione può procurare vantaggio alla simultaneità della sincronizzazione e risulta particolarmente utile se i Sottoscrittori non prevedono il download di modifiche.  
  
 **-MaxBcpThreads** _number_of_threads_  
 Specifica il numero di operazioni di copia bulk che possono essere eseguite in parallelo. Il numero massimo di connessioni ODBC e thread presenti simultaneamente corrisponde a **MaxBcpThreads** o al numero di richieste di copia bulk presenti nella tabella di sistema **sysmergeschemachange** nel database di pubblicazione, a seconda di quale sia il valore minore. **MaxBcpThreads** deve avere un valore maggiore di 0 e non ha un limite massimo specificato a livello di codice. L'impostazione predefinita è **1**.  
  
 **-MaxDownloadChanges** _number_of_download_changes_  
 Specifica il numero massimo di righe modificate che possono essere scaricate dal server di pubblicazione al Sottoscrittore. Il numero di righe scaricate può essere superiore al valore massimo specificato se vengono elaborate generazioni complete e possono essere eseguiti thread di destinazione paralleli, ognuno dei quali elabora almeno 100 modifiche nel primo passaggio. Per impostazione predefinita, tutte le modifiche pronte per essere scaricate vengono inviate.  
  
 **-MaxUploadChanges** _number_of_upload_changes_  
 Specifica il numero massimo di righe modificate che possono essere caricate dal Sottoscrittore al server di pubblicazione. Il numero di righe caricate può essere superiore al valore massimo specificato se vengono elaborate generazioni complete e possono essere eseguiti thread di destinazione paralleli, ognuno dei quali elabora almeno 100 modifiche nel primo passaggio. Per impostazione predefinita, tutte le modifiche pronte per essere caricate vengono inviate.  
  
 **-MetadataRetentionCleanup** [**0**|**1**]  
 Specifica se i metadati vengono rimossi da [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)e [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) in base al periodo di memorizzazione della pubblicazione. Il valore predefinito è **1**, che indica che deve essere eseguita la pulizia. Un valore **0** indica che la pulizia non deve essere eseguita automaticamente.  
  
 **-Output** _output_path_and_file_name_  
 Percorso del file di output dell'agente. Se non viene specificato il nome file, l'output viene inviato alla console. Se il nome file specificato esiste già, l'output viene aggiunto al file.  
  
 **-OutputVerboseLevel** [**0**|**1**|**2**]  
 Specifica se l'output deve essere dettagliato. Se il livello di dettaglio è **0**, vengono stampati solo i messaggi di errore. Se il livello di dettaglio è **1**, vengono stampati tutti i messaggi di report di stato. Se il livello di dettaglio è **2** (impostazione predefinita), vengono stampati tutti i messaggi di errore e i messaggi di report di stato. Questa opzione è utile per l'esecuzione del debug.  
  
 **-ParallelUploadDownload** [**0**|**1**]  
 Specifica se l'agente di merge deve elaborare in parallelo le modifiche caricate nel server di pubblicazione e quelle scaricate nel Sottoscrittore. Questa opzione è utile negli ambienti caratterizzati da volumi di traffico elevati con un'ampia larghezza di banda di rete. Se **ParallelUploadDownload** è **1**, l'elaborazione parallela è abilitata.  
  
 **-PacketSize**  
 Dimensioni del pacchetto, in byte. Il valore predefinito è 4096 byte.  
  
 **-PollingInterval** _polling_interval_  
 Frequenza, in secondi, di esecuzione di query sul server di pubblicazione o sul Sottoscrittore per le modifiche ai dati. Il valore predefinito è 60 secondi.  
  
 **-ProfileName** _profile_name_  
 Specifica un profilo agente da utilizzare per i parametri dell'agente. Se **ProfileName** è NULL, il profilo agente è disabilitato. Se **ProfileName** non viene specificato, viene utilizzato il profilo predefinito per il tipo di agente. Per altre informazioni, vedere [Profili degli agenti di replica](replication-agent-profiles.md).  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 Specifica l'istanza del partner di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che partecipa in una sessione di mirroring del database con il database di pubblicazione. Per altre informazioni, vedere [Mirroring e replica del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** _publisher_login_  
 Nome dell'account di accesso del server di pubblicazione. Se **PublisherSecurityMode** è **0** (per l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), questo parametro deve essere specificato.  
  
 **-PublisherPassword** _publisher_password_  
 Password del server di pubblicazione. Se **PublisherSecurityMode** è **0** (per l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), questo parametro deve essere specificato.  
  
 **-PublisherSecurityMode** [**0**|**1**]  
 Specifica la modalità di sicurezza del server di pubblicazione. Un valore **0** indica la modalità di autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (impostazione predefinita), mentre un valore **1** indica la modalità di autenticazione di Windows.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 Numero di secondi prima del timeout delle query. Il valore predefinito è 300 secondi. L'agente di merge utilizza anche il valore di `QueryTimeout` per determinare quanto tempo aspettare per la generazione di uno snapshot partizionato quando questo valore è maggiore di 1800.  
  
 **-SrcThreads** _number_of_source_threads_  
 Specifica il numero di thread di origine utilizzati dall'agente di merge per enumerare le modifiche dall'origine. L'origine è costituita dal Sottoscrittore durante il caricamento e dal server di pubblicazione durante il download. Il valore predefinito è **3**.  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 Numero massimo di secondi di attesa da parte dell'agente di merge quando il numero di processi di merge simultanei in esecuzione raggiunge il limite impostato tramite la proprietà **@max_concurrent_merge** di **sp_addmergepublication**. Se viene raggiunto il numero massimo di secondi e l'agente di merge è ancora in attesa, si chiude. Un valore 0 indica che l'agente attende indefinitamente, sebbene possa essere annullato.  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 Percorso del database Jet (file con estensione mdb) se **SubscriberType** è **2** (consente una connessione a un database Jet senza un nome origine dati (DNS, Data Source Name) ODBC).  
  
 **-SubscriberDBAddOption** [**0**| **1**| **2**| **3**]  
 Specifica se esiste un database Sottoscrittore.  
  
|Valore di SubscriberDBAddOption|Descrizione|  
|---------------------------------|-----------------|  
|**0**|Utilizza il database esistente (impostazione predefinita).|  
|**1**|Crea un nuovo database Sottoscrittore vuoto.|  
|**2**|Crea un nuovo database e lo collega al file specificato.|  
|**3**|Crea un nuovo database, collega il database e abilita tutte le sottoscrizioni che potrebbero essere presenti nel file.|  
  
> [!NOTE]  
>  Quando si utilizzano i valori **2** e **3**, il percorso del database per il Sottoscrittore deve essere specificato nell'opzione **SubscriberDatabasePath** .  
  
 **-SubscriberLogin** _subscriber_login_  
 Nome dell'account di accesso del Sottoscrittore. Se **SubscriberSecurityMode** è **0** (per l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), questo parametro deve essere specificato.  
  
 **-SubscriberPassword** _subscriber_password_  
 Password del Sottoscrittore. Se **SubscriberSecurityMode** è **0** (per l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), questo parametro deve essere specificato.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 Specifica la modalità di sicurezza del Sottoscrittore. Un valore **0** indica la modalità di autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (impostazione predefinita), mentre un valore **1** indica la modalità di autenticazione di Windows.  
  
 **-SubscriberConflictClean** [ **0**| **1**]  
 Indica se le tabelle dei conflitti vengono pulite nel Sottoscrittore durante il processo di sincronizzazione. Il valore **1** indica che le tabelle dei conflitti vengono pulite nel Sottoscrittore. Questo parametro viene utilizzato solo per le sottoscrizioni alle pubblicazioni con registrazione dei conflitti decentralizzata.  
  
 **-SubscriberType** [ **0**| **1**| **3**| **4**| **5**| **6**| **7**| **8**]  
 Specifica il tipo di connessione al Sottoscrittore utilizzato dall'agente di merge. Per questo parametro è supportato solo il valore predefinito **0** .  
  
 **-SubscriptionType**[ **0**| **1**| **2**]  
 Specifica il tipo di sottoscrizione per la distribuzione. Un valore **0** indica una sottoscrizione push (impostazione predefinita), un valore **1** indica una sottoscrizione pull e un valore **2** indica una sottoscrizione anonima.  
  
 **-SyncToAlternate** [ **0|1**]  
 Specifica se l'agente di merge sta eseguendo la sincronizzazione tra un Sottoscrittore e un server di pubblicazione alternativo. Un valore **1** indica che si tratta di un server di pubblicazione alternativo. Il valore predefinito è **0**.  
  
 **-UploadGenerationsPerBatch** _upload_generations_per_batch_  
 Numero di generazioni da elaborare in un singolo batch mentre vengono caricate le modifiche dal Sottoscrittore al server di pubblicazione. Una generazione è definita come un gruppo logico di modifiche per articolo. Il valore predefinito per un collegamento di comunicazione affidabile è **100**. Il valore predefinito per un collegamento di comunicazione non affidabile è **1**.  
  
 **-UploadReadChangesPerBatch** _upload_read_changes_per_batch_  
 Numero di modifiche da leggere in un singolo batch mentre vengono caricate le modifiche dal Sottoscrittore al server di pubblicazione. Il valore predefinito è **100**.  
  
 **-UploadWriteChangesPerBatch** _upload_write_changes_per_batch_  
 Numero di modifiche da applicare in un singolo batch mentre vengono caricate le modifiche dal Sottoscrittore al server di pubblicazione. Il valore predefinito è **100**.  
  
 **-UseInprocLoader**  
 Migliora le prestazioni dello snapshot iniziale facendo in modo che l'agente di merge utilizzi il comando BULK INSERT in caso di applicazione dei file di snapshot al Sottoscrittore. Questo parametro è deprecato in quanto non è compatibile con il tipo di dati XML. Se non si sta eseguendo la replica di dati XML, è possibile utilizzare questo parametro. Questo parametro non può essere utilizzato con snapshot in modalità carattere. Se si utilizza questo parametro, l'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel Sottoscrittore deve disporre di autorizzazioni di lettura nella directory in cui si trovano i file di dati di snapshot, con estensione bcp. Quando questo parametro non viene utilizzato, il driver ODBC caricato dall'agente legge dai file, pertanto il contesto di sicurezza dell'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non viene utilizzato.  
  
 **-Validate** [**0**|**1**|**2**|**3**]  
 Specifica se la convalida deve essere effettuata al termine della sessione di merge, e, in tal caso, indica il tipo di convalida. Il valore consigliato è **3** .  
  
|Valore di Validate|Descrizione|  
|--------------------|-----------------|  
|**0** (predefinito)|Nessuna convalida.|  
|**1**|Convalida solo tramite conteggio delle righe.|  
|**2**|Convalida mediante conteggio delle righe e checksum.|  
|**3**|Convalida mediante conteggio delle righe e checksum binario.|  
  
> [!NOTE]  
>  La convalida eseguita mediante checksum o checksum binario può segnalare erroneamente un problema se nel Sottoscrittore vi sono tipi di dati diversi rispetto al server di pubblicazione. Per altre informazioni, vedere la sezione "Considerazioni sulla convalida dei dati" in [Convalidare i dati replicati](../validate-data-at-the-subscriber.md).  
  
 **-ValidateInterval** _validate_interval_  
 Frequenza, in minuti, di convalida della sottoscrizione in modalità continua. Il valore predefinito è **60** minuti.  
  
## <a name="remarks"></a>Note  
  
> [!IMPORTANT]  
>  Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è stato installato per l'esecuzione con un account di sistema locale anziché un account utente di dominio (impostazione predefinita), il servizio può accedere solo al computer locale. Se l'agente di merge in esecuzione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è configurato per l'utilizzo della modalità di autenticazione di Windows durante l'accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'agente di merge si interrompe. L'impostazione predefinita prevede l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per avviare l'agente di merge, eseguire **replmerg.exe** dal prompt dei comandi. Per informazioni, vedere [File eseguibili dell'Agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
 La cronologia dell'agente di merge per la sessione corrente non viene eliminata durante l'esecuzione in modalità continua. Un agente con esecuzione prolungata può comportare un numero elevato di voci nelle tabelle della cronologia di merge che potrebbero ridurre le prestazioni. Per risolvere questo problema, passare alla modalità pianificata o continuare a utilizzare la modalità continua, ma creare un processo dedicato per riavviare periodicamente l'agente di merge oppure ridurre i dettagli del livello di cronologia per diminuire il numero di righe e, pertanto, l'impatto sulle prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione dell'agente di replica](replication-agent-administration.md)  
  
  
