---
title: Agente snapshot repliche | Microsoft Docs
description: In SQL Server Agente snapshot repliche prepara i file di snapshot, li archivia in una cartella e registra i processi di sincronizzazione nel database di distribuzione.
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, executables
- agents [SQL Server replication], Snapshot Agent
- command prompt [SQL Server replication]
- Snapshot Agent, parameter reference
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 9fd89016895d2e106e6c9ff9dcab4873824c7515
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364238"
---
# <a name="replication-snapshot-agent"></a>Agente snapshot repliche
[!INCLUDE[sql-asdb](../../../includes/applies-to-version/sql-asdb.md)]
  Agente snapshot repliche è un file eseguibile che consente di preparare i file di snapshot contenenti lo schema e i dati delle tabelle pubblicate e degli oggetti di database, di archiviare i file nella cartella snapshot e di registrare i processi di sincronizzazione nel database di distribuzione.  
  
> [!NOTE]  
>  - I parametri possono essere specificati in qualsiasi ordine.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="syntax"></a>Sintassi  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-PrefetchTables [0|1] ]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## <a name="arguments"></a>Argomenti  
 **-?**  
 Stampa tutti i parametri disponibili.  
  
 **-Publisher**  _server_name_[ **\\** _instance\_name_]  
 Nome del server di pubblicazione. Specificare server_name per l'istanza predefinita di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Specificare _server\_name_ **\\** _instance\_name_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server.  
  
 **-Publication** _publication_  
 Nome della pubblicazione. Questo parametro è valido solo se la pubblicazione è configurata in modo che sia sempre disponibile uno snapshot per le sottoscrizioni nuove o reinizializzate.  
  
 **-70Subscribers**  
 Deve essere utilizzato se qualsiasi Sottoscrittore esegue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versione 7.0.  
  
 **-BcpBatchSize** _bcp_\_ *batch*\_ *size*  
 Numero di righe da inviare in un'operazione di copia bulk. Quando si esegue un'operazione **bcp in** , la dimensione del batch indica il numero di righe da inviare al server come unica transazione, nonché il numero di righe che devono essere inviate prima che l'agente di distribuzione registri un messaggio di stato **bcp** . Quando si esegue un'operazione **bcp out** , viene utilizzata una dimensione batch fissa di 1000. Il valore 0 indica che non vengono registrati messaggi.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 Percorso del file di definizione dell'agente. Un file di definizione dell'agente contiene argomenti della riga di comando per l'agente. Il contenuto del file viene analizzato come file eseguibile. Utilizzare virgolette doppie (") per specificare valori dell'argomento contenenti caratteri arbitrari.  
  
 **-Distributor** _server_name_[ **\\** _instance\_name_]  
 Nome del database di distribuzione. Specificare *server_name* per l'istanza predefinita di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server. Specificare _server\_name_ **\\** _instance\_name_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in tale server.  
  
 **-DistributorDeadlockPriority** [ **-1**|**0**|**1**]  
 Priorità della connessione dell'agente snapshot con il server di distribuzione quando si verifica un deadlock. Questo parametro è specificato per risolvere deadlock che possono verificarsi tra l'agente snapshot e le applicazioni utente durante la generazione dello snapshot.  
  
|Valore di DistributorDeadlockPriority|Descrizione|  
|---------------------------------------|-----------------|  
|**-1**|Le applicazioni diverse dall'agente snapshot hanno la priorità quando si verifica un deadlock nel server di distribuzione.|  
|**0** (predefinito)|La priorità non è assegnata.|  
|**1**|L'agente snapshot ha la priorità quando si verifica un deadlock nel server di distribuzione.|  
  
 **-DistributorLogin** _distributor_login_  
 Account di accesso utilizzato per la connessione al server di distribuzione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-DistributorPassword** _distributor_password_  
 Password utilizzata per la connessione al server di distribuzione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Specifica la modalità di sicurezza del database di distribuzione. Un valore **0** indica la modalità di autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (impostazione predefinita), mentre un valore **1** indica la modalità di autenticazione di Windows.  
  
 **-DynamicFilterHostName** _dynamic_filter_host_name_  
 Usato per impostare un valore per i filtri per [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) quando viene creato uno snapshot dinamico. Se, ad esempio, per un articolo viene specificata la clausola di filtro di subset `rep_id = HOST_NAME()` e si imposta la proprietà **DynamicFilterHostName** su "FBJones" prima di chiamare l'agente di merge, verranno replicate solo le righe con "FBJones" nella colonna **rep_id** .  
  
 **-DynamicFilterLogin** _dynamic_filter_login_  
 Usato per impostare un valore per i filtri per [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) quando viene creato uno snapshot dinamico. Se, ad esempio, per un articolo viene specificata la clausola di filtro di subset `user_id = SUSER_SNAME()` e si imposta la proprietà **DynamicFilterLogin** su "rsmith" prima di chiamare il metodo **Run** dell'oggetto **SQLSnapshot** , verranno incluse nello snapshot solo le righe con "rsmith" nella colonna **user_id** .  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 Posizione di generazione dello snapshot dinamico.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 Livello di crittografia TLS (Transport Layer Security) noto in precedenza come SSL (Secure Sockets Layer) usato dall'agente di snapshot quando vengono stabilite le connessioni.  
  
|Valore di EncryptionLevel|Descrizione|  
|---------------------------|-----------------|  
|**0**|Specifica che TLS non viene usato.|  
|**1**|Specifica che TLS viene usato, ma l'agente non verifica che il certificato server TLS/SSL sia firmato da un'autorità di certificazione attendibile.|  
|**2**|Specifica che TLS viene usato e che il certificato viene verificato.|  

 > [!NOTE]  
 >  Un certificato TLS/SSL valido è definito con un nome di dominio completo di SQL Server. Affinché l'agente possa connettersi correttamente quando si imposta - EncryptionLevel su 2, creare un alias nel Server SQL locale. Il parametro ‘Nome Alias’ deve essere il nome del server e il parametro ‘Server’ deve essere impostato per il nome completo di SQL Server.
  
 Per altre informazioni, vedere [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 **-FieldDelimiter** _field_delimiter_  
 Carattere o sequenza di caratteri che contrassegna la fine di un campo nel file di dati di copia bulk [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Il valore predefinito è \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Specifica la quantità di cronologia registrata durante un'operazione snapshot. Per ridurre al minimo l'effetto della registrazione della cronologia sulle prestazioni, selezionare **1**.  
  
|Valore di HistoryVerboseLevel|Descrizione|  
|-------------------------------|-----------------|  
|**0**|I messaggi di stato vengono scritti nella console o in un file di output. I record della cronologia non vengono registrati nel database di distribuzione.|  
|**1**|Aggiorna sempre un messaggio di cronologia precedente con lo stesso stato (avvio, avanzamento, esito positivo e così via). Se non è presente un record precedente con lo stesso stato, inserisce un nuovo record.|  
|**2** (impostazione predefinita)|Inserisce nuovi record della cronologia, a meno che il record sia per eventi come messaggi inattivi o messaggi di processo con esecuzione prolungata, nel qual caso aggiorna i record precedenti.|  
|**3**|Inserisce sempre nuovi record, a meno che non si tratti di record per messaggi inattivi.|  
  
 **-HRBcpBlocks** _number_of_blocks_  
 Numero di blocchi di dati **bcp** in coda tra i thread di scrittura e di lettura. Il valore predefinito è 50. **HRBcpBlocks** viene utilizzato solo con pubblicazioni Oracle.  
  
> [!NOTE]  
>  Questo parametro viene utilizzato per ottimizzare le prestazioni di **bcp** da un server di pubblicazione Oracle.  
  
 -**HRBcpBlockSize**_block\_size_  
 Dimensione, in kilobyte (KB), di ogni blocco di dati **bcp** . Il valore predefinito è 64 KB. **HRBcpBlocks** viene utilizzato solo con pubblicazioni Oracle.  
  
> [!NOTE]  
>  Questo parametro viene utilizzato per ottimizzare le prestazioni di **bcp** da un server di pubblicazione Oracle.  
  
 **-HRBcpDynamicBlocks**  
 Indica se la dimensione di ogni blocco di dati **bcp** può o meno crescere dinamicamente. **HRBcpBlocks** viene utilizzato solo con pubblicazioni Oracle.  
  
> [!NOTE]  
>  Questo parametro viene utilizzato per ottimizzare le prestazioni di **bcp** da un server di pubblicazione Oracle.  
  
 **-KeepAliveMessageInterval** _keep_alive_interval_  
 Tempo di attesa, in secondi, da parte dell'agente snapshot prima di registrare un messaggio di attesa del back-end nella tabella [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) . Il valore predefinito è 300 secondi.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 Numero di secondi prima del timeout di accesso. Il valore predefinito è **15** secondi.  
  
 **-MaxBcpThreads** _number_of_threads_  
 Specifica il numero di operazioni di copia bulk che possono essere eseguite in parallelo. Il numero massimo di connessioni ODBC e thread presenti simultaneamente corrisponde a **MaxBcpThreads** o al numero di richieste di copia bulk presenti nella transazione di sincronizzazione nel database di distribuzione, a seconda di quale sia il valore minore. **MaxBcpThreads** deve avere un valore maggiore di **0** e non ha un limite massimo specificato a livello di codice. Il valore predefinito è due volte il numero di processori.  
 
 > [!NOTE]
 > Se l'oggetto replicato ha un filtro, l'agente snapshot genererà un solo file BCP per tale articolo anziché generare più file BCP. 
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Indica se le eliminazioni irrilevanti vengono inviate al Sottoscrittore. Le eliminazioni irrilevanti sono comandi DELETE inviati ai Sottoscrittori per righe che non appartengono alla partizione del Sottoscrittore. Le eliminazioni irrilevanti non influiscono sulla convergenza o sull'integrità dei dati, ma possono comportare traffico di rete non necessario. Il valore predefinito di **MaxNetworkOptimization** è **0**. Impostando **MaxNetworkOptimization** su **1** è possibile ridurre al minimo le possibilità di eliminazioni irrilevanti, riducendo pertanto il traffico e ottimizzando le prestazioni di rete. L'impostazione di questo parametro su **1** comporta inoltre l'aumento dell'archiviazione di metadati e può provocare una riduzione delle prestazioni nel server di pubblicazione se sono presenti più livelli di filtri di join e filtri di subset complessi. Valutare inoltre attentamente la topologia di replica e impostare **MaxNetworkOptimization** su **1** solo se il traffico di rete dovuto a eliminazioni irrilevanti è eccessivo.  
  
> [!NOTE]
>  L'impostazione di questo parametro su **1** è utile solo quando l'opzione di ottimizzazione della sincronizzazione della pubblicazione di tipo merge è impostata su **true** (parametro `@keep_partition_changes**` di [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Output** _output_path_and_file_name_  
 Percorso del file di output dell'agente. Se non viene specificato il nome file, l'output viene inviato alla console. Se il nome file specificato esiste già, l'output viene aggiunto al file.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Specifica se l'output deve essere dettagliato.  
  
|Valore di OutputVerboseLevel|Descrizione|  
|------------------------------|-----------------|  
|**0**|Vengono stampati solo i messaggi di errore.|  
|**1** (impostazione predefinita)|Vengono stampati tutti i messaggi di report di stato (impostazione predefinita).|  
|**2**|Vengono stampati tutti i messaggi di errore e i messaggi di report di stato. Questa opzione è utile per l'esecuzione del debug.|  
  
 **-PacketSize** _packet_size_  
 Dimensione del pacchetto, in byte, utilizzata dall'agente snapshot durante la connessione a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il valore predefinito è 8192 byte.  
  
> [!NOTE]  
>  È consigliabile modificare le dimensioni dei pacchetti solo se si è certi che l'operazione determinerà un miglioramento delle prestazioni. Per la maggior parte delle applicazioni, le dimensioni predefinite risultano ottimali.  

**-PrefetchTables** [ **0**| **1**]  
 Parametro facoltativo che specifica se per gli oggetti tabella verranno eseguite la prelettura e la memorizzazione nella cache.  Il comportamento predefinito prevede la prelettura di determinate proprietà delle tabelle usando il componente SMO in base a un calcolo interno.  Questo parametro può essere utile in scenari in cui l'esecuzione dell'operazione di prelettura SMO richiede molto più tempo. Se questo parametro non viene usato, questa decisione viene presa in fase di esecuzione in base alla percentuale di tabelle che vengono aggiunte come articoli alla pubblicazione.  
  
|Valore di OutputVerboseLevel|Descrizione|  
|------------------------------|-----------------|  
|**0**|La chiamata al metodo Prefetch del componente SMO è disabilitata.|  
|**1**|L'agente di snapshot chiamerà il metodo Prefetch per memorizzare nella cache alcune proprietà di tabella tramite SMO|  

 **-ProfileName** _profile_name_  
 Specifica un profilo agente da utilizzare per i parametri dell'agente. Se **ProfileName** è NULL, il profilo agente è disabilitato. Se **ProfileName** non viene specificato, viene utilizzato il profilo predefinito per il tipo di agente. Per altre informazioni, vedere [Profili degli agenti di replica](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** _publisher_database_  
 Nome del database di pubblicazione. *Questo parametro non è supportato per i server di pubblicazione Oracle*.  
  
 **-PublisherDeadlockPriority** [ **-1**|**0**|**1**]  
 Priorità della connessione dell'agente snapshot con il server di pubblicazione quando si verifica un deadlock. Questo parametro è specificato per risolvere deadlock che possono verificarsi tra l'agente snapshot e le applicazioni utente durante la generazione dello snapshot.  
  
|Valore di PublisherDeadlockPriority|Descrizione|  
|-------------------------------------|-----------------|  
|**-1**|Le applicazioni diverse dall'agente snapshot hanno la priorità quando si verifica un deadlock nel server di pubblicazione.|  
|**0** (predefinito)|La priorità non è assegnata.|  
|**1**|L'agente snapshot ha la priorità quando si verifica un deadlock nel server di pubblicazione.|  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance\_name_]  
 Specifica l'istanza del partner di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che partecipa in una sessione di mirroring del database con il database di pubblicazione. Per altre informazioni, vedere [Mirroring e replica del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** _publisher_login_  
 Account di accesso utilizzato per la connessione al server di pubblicazione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-PublisherPassword**  _publisher_password_  
 Password utilizzata per la connessione al server di pubblicazione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Specifica la modalità di sicurezza del server di pubblicazione. Un valore **0** indica la modalità di autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (impostazione predefinita), mentre un valore **1** indica la modalità di autenticazione di Windows.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 Numero di secondi prima del timeout delle query. Il valore predefinito è 1800 secondi.  
  
 **-ReplicationType** [ **1**| **2**]  
 Specifica il tipo di replica. Un valore **1** indica la replica transazionale, mentre un valore **2** indica la replica di tipo merge.  
  
 **-RowDelimiter** _row_delimiter_  
 Carattere o sequenza di caratteri che contrassegna la fine di una riga nel file di dati di copia bulk [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Il valore predefinito è \n\<,@g>\n.  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 Numero massimo di secondi di attesa da parte dell'agente snapshot quando il numero di processi snapshot dinamici simultanei in esecuzione raggiunge il limite impostato tramite la proprietà `@max_concurrent_dynamic_snapshots` di [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Se viene raggiunto il numero massimo di secondi e l'agente snapshot è ancora in attesa, si chiude. Un valore 0 indica che l'agente attende indefinitamente, sebbene possa essere annullato.  
  
 \- **UsePerArticleContentsView** _use_per_article_contents_view_  
 Questo parametro è deprecato ed è ancora supportato solo per garantire la compatibilità con le versioni precedenti.  
  
## <a name="remarks"></a>Osservazioni  
  
> [!IMPORTANT]  
>  Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è stato installato per l'esecuzione con un account di sistema locale anziché un account utente di dominio (impostazione predefinita), il servizio può accedere solo al computer locale. Se l'agente snapshot in esecuzione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è configurato per l'utilizzo della modalità di autenticazione di Windows durante l'accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'agente snapshot si interrompe. L'impostazione predefinita prevede l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per avviare l'agente snapshot, eseguire **snapshot.exe** dal prompt dei comandi. Per informazioni, vedere [File eseguibili dell'Agente di replica](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione dell'agente di replica](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
