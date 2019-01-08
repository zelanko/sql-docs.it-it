---
title: sp_addsubscription (Transact-SQL) | Microsoft Docs
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords:
- sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a0064787eee6c3ac267b3ababcd9881e794ff2e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206390"
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge una sottoscrizione a una pubblicazione e imposta lo stato del Sottoscrittore. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @publication=] '*publication*'  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ @article=] '*articolo*'  
 Articolo in cui viene sottoscritta la pubblicazione. *articolo* viene **sysname**, con un valore predefinito è all. Se si specifica all, viene aggiunta una sottoscrizione a tutti gli articoli della pubblicazione specificata. Per i server di pubblicazione Oracle sono supportati solo i valori all o NULL.  
  
 [ @subscriber=] '*sottoscrittore*'  
 Nome del Sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
 [ @destination_db=] '*destination_db*'  
 Nome del database di destinazione in cui verranno inseriti i dati replicati. *destination_db* viene **sysname**, con un valore predefinito è NULL. Quando è NULL, *destination_db* è impostato sul nome del database di pubblicazione. Per i server di pubblicazione Oracle *destination_db* deve essere specificato. Per un non - SQL Server sottoscrittore, specificare un valore (destinazione predefinita) per *destination_db*.  
  
 [ @sync_type=] '*sync_type*'  
 Tipo di sincronizzazione per la sottoscrizione. *sync_type* viene **nvarchar(255**, e può essere uno dei valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|none|Il Sottoscrittore dispone già dello schema e dei dati iniziali per le tabelle pubblicate.<br /><br /> Nota: Questa opzione è deprecata. In alternativa, utilizzare il valore replication support only.|  
|automatic (predefinito)|Lo schema e i dati iniziali per le tabelle pubblicate vengono trasferiti per primi nel Sottoscrittore.|  
|replication support only|Esegue nel Sottoscrittore la generazione automatica di stored procedure e trigger personalizzati degli articoli che supportano l'aggiornamento delle sottoscrizioni, se appropriato. Presuppone che nel Sottoscrittore siano già disponibili lo schema e i dati iniziali per le tabelle pubblicate. Durante la configurazione di una topologia di replica transazionale peer-to-peer, assicurarsi che i dati in tutti i nodi della topologia siano identici. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).<br /><br /> *Non è supportata per le sottoscrizioni a pubblicazioni non SQL Server.*|  
|initialize with backup|Lo schema e i dati iniziali per le tabelle pubblicate vengono recuperati da un backup del database di pubblicazione. Si presuppone che il Sottoscrittore abbia accesso a un backup del database di pubblicazione. Il percorso del tipo di backup e il supporto per il backup vengono specificati da *backupdevicename* e *backupdevicetype*. Se si utilizza questa opzione, non sarà necessario mettere in stato di inattività la topologia di replica transazionale peer-to-peer durante la configurazione.<br /><br /> *Non è supportata per le sottoscrizioni a pubblicazioni non SQL Server.*|  
|initialize from lsn|Utilizzato quando si aggiunge un nodo a una topologia di replica transazionale peer-to-peer. Utilizzato con @subscriptionlsn perché tutte le transazioni pertinenti vengano replicate nel nuovo nodo. Presuppone che nel Sottoscrittore siano già disponibili lo schema e i dati iniziali per le tabelle pubblicate. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
> [!NOTE]  
>  Le tabelle e i dati di sistema vengono sempre trasferiti.  
  
 [ @status=] '*stato*'  
 Stato della sottoscrizione. *lo stato* viene **sysname**, con un valore predefinito NULL. Se non è impostato in modo esplicito, questo parametro viene impostato automaticamente dalla replica su uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|active|La sottoscrizione è inizializzata e in grado di accettare modifiche. Questa opzione viene impostata quando il valore di *sync_type* è none, initialize con backup o replication support only.|  
|subscribed|La sottoscrizione deve essere inizializzata. Questa opzione viene impostata quando il valore di *sync_type* è automatica.|  
  
 [ @subscription_type=] '*subscription_type*'  
 Tipo di sottoscrizione. *subscription_type* viene **nvarchar(4)**, con un valore predefinito è push. I possibili valori sono push o pull. Gli agenti di distribuzione delle sottoscrizioni push si trovano nel server di distribuzione, mentre gli agenti di distribuzione delle sottoscrizioni pull si trovano nel Sottoscrittore. *subscription_type* può essere pull per creare una sottoscrizione pull denominata nota al server di pubblicazione. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md).  
  
> [!NOTE]  
>  Con le sottoscrizioni anonime non è necessario utilizzare questa stored procedure.  
  
 [ @update_mode=] '*update_mode*'  
 È il tipo di aggiornamento. *update_mode* viene **nvarchar(30)**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|read only (predefinito)|La sottoscrizione è di sola lettura. Le modifiche apportate nel Sottoscrittore non vengono ritrasmesse al server di pubblicazione.|  
|sync tran|Abilita il supporto per sottoscrizioni ad aggiornamento immediato. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|queued tran|Abilita la sottoscrizione per l'aggiornamento in coda. Le modifiche dei dati possono essere apportate nel Sottoscrittore, archiviate in una coda e quindi distribuite al server di pubblicazione. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|failover|Abilita la sottoscrizione per l'aggiornamento immediato sostituito dall'aggiornamento in coda in caso di failover. Le modifiche dei dati possono essere apportate nel Sottoscrittore e distribuite immediatamente al server di pubblicazione. Se il server di pubblicazione e il Sottoscrittore non sono connessi, la modalità di aggiornamento può essere modificata in modo tale che le modifiche apportate ai dati nel Sottoscrittore vengano archiviate in una coda fino alla riconnessione del Sottoscrittore e del server di pubblicazione. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|queued failover|Abilita la sottoscrizione come sottoscrizione con aggiornamento in coda con la possibilità di passare alla modalità di aggiornamento immediato. Le modifiche ai dati possono essere apportate nel Sottoscrittore e archiviate in una coda fino alla riconnessione del Sottoscrittore e del server di pubblicazione. Quando viene ristabilita una connessione continua, la modalità di aggiornamento può essere modificata nella modalità di aggiornamento immediato. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
  
 Si noti che i valori synctran e queued tran non sono consentite se la pubblicazione da sottoscrivere supporta DTS.  
  
 [ @loopback_detection=] '*loopback_detection*'  
 Indica se l'agente di distribuzione reinvia al Sottoscrittore le transazioni generate nel Sottoscrittore stesso. *loopback_detection* viene **nvarchar(5**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|true|L'agente di distribuzione non reinvia le transazioni generate nel Sottoscrittore al Sottoscrittore. Utilizzato con la replica transazionale bidirezionale. Per altre informazioni, vedere [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|false|L'agente di distribuzione reinvia le transazioni generate nel Sottoscrittore al Sottoscrittore.|  
|NULL (predefinito)|Impostato automaticamente su true per un Sottoscrittore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e su false per un Sottoscrittore non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 [ @frequency_type=] *frequency_type*  
 Frequenza di pianificazione dell'attività di distribuzione. *frequency_type* è di tipo int, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|1|Una volta|  
|2|Su richiesta|  
|4|Ogni giorno|  
|8|Settimanale|  
|16|Mensile|  
|32|Mensile relativa|  
|64 (impostazione predefinita)|Avvio automatico|  
|128|Periodica|  
  
 [ @frequency_interval=] *frequency_interval*  
 Il valore da applicare alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è NULL.  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 Data dell'agente di distribuzione. Questo parametro viene utilizzato quando *frequency_type* è impostato su 32 (mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|1|Primo|  
|2|Secondo|  
|4|Terzo|  
|8|Quarto|  
|16|Ultimo|  
|NULL (predefinito)||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
 [ @frequency_subday=] *frequency_subday*  
 Frequenza di ripianificazione in minuti durante il periodo definito. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|1|Una volta|  
|2|Secondo|  
|4|Minuto|  
|8|Ora|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata dell'agente di distribuzione nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata dell'agente di distribuzione, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [ @active_start_date=] *active_start_date*  
 Data della prima esecuzione pianificata dell'agente di distribuzione nel formato AAAAMMGG. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
 [ @active_end_date=] *active_end_date*  
 Data dell'ultima esecuzione pianificata dell'agente di distribuzione, nel formato AAAAMMGG. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
 [ @optional_command_line=] '*optional_command_line*'  
 Prompt dei comandi facoltativo da eseguire. *optional_command_line* viene **nvarchar (4000)**, con un valore predefinito è NULL.  
  
 [ @reserved=] '*riservato*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 È se la sottoscrizione può essere sincronizzata tramite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gestione sincronizzazione Microsoft Windows. *enabled_for_syncmgr* viene **nvarchar(5**, con un valore predefinito è FALSE. Se il valore è false, la sottoscrizione non viene registrata con Gestione sincronizzazione Microsoft Windows. Se il valore è true, la sottoscrizione viene registrata con Gestione sincronizzazione Microsoft Windows e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Questa proprietà non è supportata per server di pubblicazione Oracle.  
  
 [ @offloadagent=] '*remote_agent_activation*'  
 Specifica se è possibile o meno attivare l'agente in remoto. *remote_agent_activation* viene **bit** con valore predefinito è 0.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
 [ @offloadserver=] '*remote_agent_server_name*'  
 Specifica il nome di rete del server da utilizzare per l'attivazione remota. *remote_agent_server_name*viene **sysname**, con un valore predefinito è NULL.  
  
 [ @dts_package_name=] '*dts_package_name*'  
 Specifica il nome del pacchetto Data Transformation Services (DTS). *dts_package_name* è un **sysname** con valore predefinito è NULL. Ad esempio, per specificare il pacchetto DTSPub_Package, il parametro deve essere `@dts_package_name = N'DTSPub_Package'`. Questo parametro è disponibile per sottoscrizioni push. Per aggiungere informazioni sul pacchetto DTS a una sottoscrizione pull, utilizzare sp_addpullsubscription_agent.  
  
 [ @dts_package_password=] '*dts_package_password*'  
 Password del pacchetto, se è disponibile. *dts_package_password* viene **sysname** con valore predefinito è NULL.  
  
> [!NOTE]  
>  È necessario specificare una password se *dts_package_name* è specificato.  
  
 [ @dts_package_location=] '*dts_package_location*'  
 Specifica la posizione del pacchetto. *dts_package_location* è un **nvarchar (12)**, con un valore predefinito del server di distribuzione. Per la posizione del pacchetto è possibile specificare distributor o subscriber.  
  
 [ @distribution_job_name=] '*job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher=] '*server di pubblicazione*'  
 Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere specificato per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
 [ @backupdevicetype=] '*backupdevicetype*'  
 Specifica il tipo di dispositivo di backup utilizzato durante l'inizializzazione di un Sottoscrittore da un backup. *backupdevicetype* viene **nvarchar(20)**, i possibili valori sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|logical (predefinito)|Il dispositivo di backup è un dispositivo logico.|  
|disk|Il dispositivo di backup è l'unità disco.|  
|tape|Il dispositivo di backup è l'unità nastro.|  
  
 *backupdevicetype* viene utilizzato solo quando *sync_method*è impostato su initialize_with_backup.  
  
 [ @backupdevicename=] '*backupdevicename*'  
 Specifica il nome del dispositivo utilizzato durante l'inizializzazione di un Sottoscrittore da un backup. *backupdevicename* viene **nvarchar(1000)**, con un valore predefinito è NULL.  
  
 [ @mediapassword=] '*mediapassword*'  
 Specifica una password per il set di supporti se durante la formattazione dei supporti è stata impostata una password. *MEDIAPASSWORD* viene **sysname**, con un valore predefinito NULL.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password=] '*password*'  
 Specifica una password per il backup se durante la creazione del backup è stata impostata una password. *la password*viene **sysname**, con un valore predefinito NULL.  
  
 [ @fileidhint=] *fileidhint*  
 Identifica un valore ordinale del set di backup da ripristinare. *fileidhint* viene **int**, con un valore predefinito NULL.  
  
 [ @unload=] *scaricamento*  
 Specifica se è necessario scaricare un dispositivo di backup su nastro dopo il completamento dell'inizializzazione dal backup. *scaricamento* viene **bit**, con un valore predefinito 1. il valore 1 specifica che il nastro deve essere scaricato. *scaricamento* viene utilizzato solo quando *backupdevicetype* è un nastro.  
  
 [ @subscriptionlsn=] *subscriptionlsn*  
 Specifica il numero di sequenza del file di log (LSN) al quale una sottoscrizione deve iniziare a recapitare le modifiche a un nodo in una topologia di replica transazionale peer-to-peer. Usato con un @sync_type valore di initialize from lsn per assicurarsi che tutte le transazioni pertinenti vengano replicate in un nuovo nodo. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 [ @subscriptionstreams=] *subscriptionstreams*  
 Numero di connessioni consentite per agente di distribuzione per l'applicazione di batch di modifiche in parallelo a un Sottoscrittore, conservando molte delle caratteristiche transazionali disponibili quando si utilizza un singolo thread. *subscriptionstreams* viene **tinyint**, con un valore predefinito NULL. È supportato un intervallo di valori compreso tra 1 e 64. Questo parametro non è supportato per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori, server di pubblicazione Oracle o sottoscrizioni peer-to-peer. Ogni volta che vengono utilizzati flussi di sottoscrizioni, vengono aggiunte nuove righe nella tabella msreplication_subscriptions (1 per stream) con agent_id impostato su NULL.  
  
> [!NOTE]  
>  Subscriptionstreams non funziona per gli articoli configurati per fornire [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per utilizzare subscriptionstreams, configurare gli articoli per fornire invece chiamate di stored procedure.  
  
 [ @subscriber_type=] *subscriber_type*  
 Tipo di Sottoscrittore. *subscriber_type* viene **tinyint**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0 (predefinito)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sottoscrittore|  
|1|Server dell'origine dei dati ODBC.|  
|2|Database [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|3|Provider OLE DB|  
  
 [ @memory_optimized=] *memory_optimized*  
 Indica che la sottoscrizione supporta le tabelle ottimizzate per la memoria. *memory_optimized* viene **bit**, dove 1 è uguale a true (la sottoscrizione supporta le tabelle ottimizzate per la memoria).  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 La stored procedure sp_addsubscription viene utilizzata per la replica snapshot e transazionale.  
  
 Se la stored procedure sp_addsubscription viene eseguita da un membro del ruolo predefinito del server sysadmin per creare una sottoscrizione push, il processo dell'agente di distribuzione viene creato in modo implicito e viene eseguito utilizzando l'account del servizio SQL Server Agent. È consigliabile eseguirla [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) e specificare le credenziali di un account Windows diverso specifico dell'agente per @job_login e @job_password. Per altre informazioni, vedere [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 La stored procedure sp_addsubscription impedisce ai Sottoscrittori ODBC e OLE DB di accedere ai seguenti tipi di pubblicazione:  
  
-   Sono stati creati con l'oggetto nativo *sync_method* nella chiamata a [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
-   Contiene articoli che sono state aggiunte per la pubblicazione con il [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) stored procedure che aveva un *pre_creation_cmd* valore del parametro di 3 (troncamento).  
  
-   Tentativo di impostazione *update_mode* su sync tran.  
  
-   Pubblicazioni che includono un articolo configurato per l'utilizzo di istruzioni con parametri.  
  
 Inoltre, se una pubblicazione include il *allow_queued_tran* opzione impostata su true (che consente l'accodamento delle modifiche nel Sottoscrittore finché possono essere applicate nel server di pubblicazione), la colonna timestamp in un articolo viene inserita nello script come **timestamp**, e le modifiche in tale colonna vengono inviate al sottoscrittore. Nel Sottoscrittore viene quindi generato e aggiornato il valore della colonna timestamp. Per un Sottoscrittore ODBC o OLE DB, sp_addsubscription ha esito negativo se viene effettuato un tentativo di sottoscrivere una pubblicazione che include *allow_queued_tran* impostata su true e articoli che includono colonne timestamp.  
  
 Se una sottoscrizione non utilizza un pacchetto DTS, non può sottoscrivere una pubblicazione che è impostata su *allow_transformable_subscriptions*. Se la tabella della pubblicazione deve essere replicata sia come sottoscrizione DTS che come sottoscrizione non DTS, è necessario creare due pubblicazioni distinte, una per ogni tipo di sottoscrizione.  
  
 In caso di selezione delle opzioni **sync_type** , i parametri *replication support only*, *initialize with backup*o *initialize from lsn*e l'agente di lettura log devono essere in esecuzione dopo aver eseguito **sp_addsubscription**, in modo che gli script impostati vengano scritti nel database di distribuzione. L'agente di lettura log deve essere in esecuzione con un account membro del ruolo predefinito del server **sysadmin** . Quando l'opzione **sync_type** è impostata su *Automatic*, non sono richieste azioni dell'agente di lettura log speciali.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server sysadmin o del ruolo predefinito del database db_owner possono eseguire sp_addsubscription. Per le sottoscrizioni pull, gli utenti che dispongono di un account di accesso nell'elenco di accesso della pubblicazione possono eseguire sp_addsubscription.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Creare una sottoscrizione per un Sottoscrittore non SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
