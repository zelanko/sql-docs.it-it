---
title: sp_addmergepullsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba75dc83e8fb4ce5a9ad31876b2b2592b22b7197
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791783"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo processo agente utilizzato per pianificare la sincronizzazione di una sottoscrizione pull con una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
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
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@name =** ] **'***nome***'**  
 Nome dell'agente. *nome* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_db =** ] **'***publisher_db***'**  
 Nome del database del server di pubblicazione. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publication =** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 Modalità di sicurezza da utilizzare quando si effettua la connessione a un server di pubblicazione per la sincronizzazione. *publisher_security_mode* viene **int**, con un valore predefinito è 1. Se **0**, specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. Se **1**, specifica l'autenticazione di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 Account di accesso da utilizzare per la connessione a un server di pubblicazione in fase di sincronizzazione. *publisher_login* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 Password utilizzata per la connessione al server di pubblicazione. *publisher_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
 [  **@publisher_encrypted_password =** ]*publisher_encrypted_password*  
 L'impostazione *publisher_encrypted_password* non è più supportata. Tentativo di impostare questo **bit** parametro per **1** comporterà un errore.  
  
 [  **@subscriber =** ] **'***sottoscrittore***'**  
 Nome del Sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 Nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 Modalità di sicurezza da utilizzare quando si effettua la connessione a un Sottoscrittore per la sincronizzazione. *subscriber_security_mode* viene **int**, con un valore predefinito è 1. Se **0**, specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. Se **1**, specifica l'autenticazione di Windows.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. L'agente di merge si connette sempre al Sottoscrittore locale utilizzando l'autenticazione di Windows. Se si specifica un valore per questo parametro, viene restituito un messaggio di avviso, ma il valore viene ignorato.  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 Account di accesso da utilizzare quando ci si connette a un Sottoscrittore per la sincronizzazione. *subscriber_login* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_login* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. Se si specifica un valore per questo parametro, viene restituito un messaggio di avviso, ma il valore viene ignorato.  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 Password del Sottoscrittore per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *subscriber_password* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. Se si specifica un valore per questo parametro, viene restituito un messaggio di avviso, ma il valore viene ignorato.  
  
 [  **@distributor =** ] **'***distributore***'**  
 Nome del server di distribuzione. *server di distribuzione* viene **sysname**, il valore predefinito è *server di pubblicazione*; vale a dire, il server di pubblicazione è anche il server di distribuzione.  
  
 [  **@distributor_security_mode =** ] *distributor_security_mode*  
 Modalità di sicurezza da utilizzare quando si effettua la connessione a un server di distribuzione per la sincronizzazione. *distributor_security_mode* viene **int**, con un valore predefinito è 0. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login =** ] **'***distributor_login***'**  
 Account di accesso da utilizzare quando ci si connette a un server di distribuzione per la sincronizzazione. *distributor_login* è obbligatorio se *distributor_security_mode* è impostata su **0**. *distributor_login* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@distributor_password =** ] **'***distributor_password***'**  
 Password del database di distribuzione. *distributor_password* è obbligatorio se *distributor_security_mode* è impostata su **0**. *distributor_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
 [  **@encrypted_password =** ] *encrypted_password*  
 L'impostazione *encrypted_password* non è più supportata. Tentativo di impostare questo **bit** parametro per **1** comporterà un errore.  
  
 [  **@frequency_type =** ] *frequency_type*  
 Frequenza per l'esecuzione pianificata dell'agente di merge. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64**|Avvio automatico|  
|**128**|Periodica|  
|NULL (predefinito)||  
  
> [!NOTE]  
>  Se si specifica un valore di **64** fa sì che l'agente di Merge per l'esecuzione in modalità continua. Corrisponde all'impostazione di **-continua** parametro per l'agente. Per altre informazioni, vedere [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Giorno o giorni in cui viene eseguito l'agente di merge. *frequency_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Domenica|  
|**2**|Lunedì|  
|**3**|Martedì|  
|**4**|Mercoledì|  
|**5**|Giovedì|  
|**6**|Venerdì|  
|**7**|Sabato|  
|**8**|Day|  
|**9**|Giorni feriali|  
|**10**|Giorni festivi|  
|NULL (predefinito)||  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 Data dell'agente di merge. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
|NULL (predefinito)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 Frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
|NULL (predefinito)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata dell'agente di merge, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata dell'agente di merge, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Data della prima esecuzione pianificata dell'agente di merge, nel formato AAAAMMGG. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Data dell'ultima esecuzione pianificata dell'agente di merge, nel formato AAAAMMGG. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
 [  **@optional_command_line =** ] **'***optional_command_line***'**  
 Prompt dei comandi facoltativo specificato per l'agente di merge. *optional_command_line* viene **nvarchar(255**, valore predefinito è ' '. Può essere utilizzato per rendere disponibili ulteriori parametri all'agente di merge, come nell'esempio seguente, in cui il timeout predefinito per le query viene aumentato a `600`:  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
 [  **@merge_jobid =** ] *merge_jobid*  
 Parametro di output per l'ID del processo. *merge_jobid* viene **Binary (16)**, con un valore predefinito è NULL.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 Specifica se la sottoscrizione può essere sincronizzata tramite Gestione sincronizzazione Microsoft Windows. *enabled_for_syncmgr* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **false**, la sottoscrizione non è registrata con Gestione sincronizzazione Microsoft. Se **true**, la sottoscrizione viene registrata con Gestione sincronizzazione e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [  **@ftp_address =** ] **'***ftp_address***'**  
 Disponibile solo per compatibilità con le versioni precedenti.  
  
 [  **@ftp_port =** ] *ftp_port*  
 Disponibile solo per compatibilità con le versioni precedenti.  
  
 [  **@ftp_login =** ] **'***ftp_login***'**  
 Disponibile solo per compatibilità con le versioni precedenti.  
  
 [  **@ftp_password =** ] **'***ftp_password***'**  
 Disponibile solo per compatibilità con le versioni precedenti.  
  
 [  **@alt_snapshot_folder =** ] **'***alternate_snapshot_folder***'**  
 Posizione da cui prelevare i file di snapshot. *alternate_snapshot_folder* viene **nvarchar(255**, con un valore predefinito è NULL. che indica che i file di snapshot vengono prelevati dal percorso predefinito specificato dal server di pubblicazione.  
  
 [  **@working_directory =** ] **'***working_directory***'**  
 Nome della directory di lavoro utilizzata per l'archiviazione temporanea dei file di dati e dello schema della pubblicazione quando i file di snapshot vengono trasferiti tramite FTP. *working_directory* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
 [  **@use_ftp =** ] **'***use_ftp***'**  
 Specifica l'utilizzo di FTP anziché del protocollo utilizzato normalmente per il recupero degli snapshot. *use_ftp* viene **nvarchar(5**, con un valore predefinito è FALSE.  
  
 [  **@reserved =** ] **'***riservato***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@use_interactive_resolver =** ] **'***use_interactive_resolver***'** ]  
 Specifica l'utilizzo del sistema di risoluzione interattivo per tutti gli articoli che supportano la risoluzione interattiva. *use_interactive_resolver* viene **nvarchar(5**, con un valore predefinito è FALSE.  
  
 [  **@offloadagent =** ] **'***remote_agent_activation***'**  
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_activation* su un valore diverso da **false** genererà un errore.  
  
 [  **@offloadserver =** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_server_name* su qualsiasi valore diverso da NULL, verrà generato un errore.  
  
 [  **@job_name =** ] **'***job_name***'** ]  
 Nome di un processo esistente dell'agente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando la sottoscrizione verrà sincronizzata mediante un processo esistente anziché un nuovo processo creato (impostazione predefinita). Se non si è un membro del **sysadmin** ruolo predefinito del server, è necessario specificare *job_login* e *job_password* quando si specifica *job_name*.  
  
 [  **@dynamic_snapshot_location =** ] **'***dynamic_snapshot_location***'** ]  
 Percorso della cartella in cui vengono letti i file di snapshot se è necessario utilizzare uno snapshot dei dati filtrati. *dynamic_snapshot_location* viene **nvarchar(260)**, con un valore predefinito è NULL. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 [  **@use_web_sync =** ] *use_web_sync*  
 Indica che la sincronizzazione Web è abilitata. *use_web_sync* viene **bit**, con un valore predefinito è 0. **1** specifica che la sottoscrizione pull può essere sincronizzata su internet tramite HTTP.  
  
 [  **@internet_url =** ] **'***internet_url***'**  
 Percorso del listener per la replica (REPLISAPI.DLL) per la sincronizzazione Web. *internet_url* viene **nvarchar(260)**, con un valore predefinito è NULL. *internet_url* è un URL completo nel formato `https://server.domain.com/directory/replisapi.dll`. Se il server è configurato per l'attesa su una porta diversa dalla porta 80, è necessario specificare anche il numero di porta nel formato `https://server.domain.com:portnumber/directory/replisapi.dll`, dove `portnumber` rappresenta la porta.  
  
 [  **@internet_login =** ] **'***internet_login***'**  
 Account di accesso utilizzato dall'agente di merge per la connessione al server Web che ospita la sincronizzazione Web tramite l'autenticazione di base HTTP. *internet_login* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@internet_password =** ] **'***internet_password***'**  
 Password utilizzata dall'agente di merge per la connessione al server Web che ospita la sincronizzazione Web tramite l'autenticazione di base HTTP. *internet_password* viene **nvarchar(524**, con un valore predefinito NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [  **@internet_security_mode =** ] *internet_security_mode*  
 Metodo di autenticazione utilizzato dall'agente di merge per la connessione al server Web durante la sincronizzazione Web tramite HTTPS. *internet_security_mode* viene **int** i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Viene utilizzata l'autenticazione di base.|  
|**1** (impostazione predefinita)|Viene utilizzata l'autenticazione integrata di Windows.|  
  
> [!NOTE]  
>  È consigliabile utilizzare l'autenticazione di base per la sincronizzazione Web. Per utilizzare la sincronizzazione Web è necessario stabilire una connessione SSL al server Web. Per altre informazioni, vedere [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
 [  **@internet_timeout =** ] *internet_timeout*  
 Periodo di tempo, espresso in secondi, trascorso il quale una richiesta di sincronizzazione Web scade. *internet_timeout* viene **int**, il valore predefinito è **300** secondi.  
  
 [  **@hostname =** ] **'***hostname***'**  
 Sostituisce il valore di HOST_NAME() quando questa funzione viene utilizzata nella clausola WHERE di un filtro con parametri. *nome host* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@job_login =** ] **'***job_login***'**  
 Account di accesso per l'account di Windows utilizzato per l'esecuzione dell'agente. *job_login* viene **nvarchar(257)**, non prevede alcun valore predefinito. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al Sottoscrittore e per le connessioni al server di distribuzione e al server di pubblicazione quando viene utilizzata l'autenticazione integrata di Windows.  
  
 [  **@job_password =** ] **'***job_password***'**  
 Password dell'account di Windows utilizzato per l'esecuzione dell'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per una sicurezza ottimale, i nomi e le password degli account di accesso dovrebbero essere passati in fase di esecuzione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_addmergepullsubscription_agent** viene utilizzata nella replica di tipo merge e utilizza funzionalità simili a quelle [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
 Per un esempio di come specificare correttamente le impostazioni di sicurezza quando si esegue **sp_addmergepullsubscription_agent**, vedere [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addmergepullsubscription_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
