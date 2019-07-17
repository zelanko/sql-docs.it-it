---
title: sp_addpullsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 220e21713935409d7d85ecd156524883dbbace08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022459"
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
 
  Aggiunge un nuovo processo pianificato dell'agente per la sincronizzazione di una sottoscrizione pull con una pubblicazione transazionale. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]          , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
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
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'_` È il nome del server di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito NULL. *publisher_db* viene ignorata dal server di pubblicazione Oracle.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` È la modalità di sicurezza da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_security_mode* viene **int,** con valore predefinito è NULL. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. L'agente di distribuzione si connette sempre al Sottoscrittore locale utilizzando l'autenticazione di Windows. Se si specifica un valore diverso da NULL oppure **1** viene specificato per questo parametro, viene restituito un messaggio di avviso.  
  
`[ @subscriber_login = ] 'subscriber_login'` È l'account di accesso da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_login* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. Se viene specificato un valore per questo parametro, viene visualizzato un messaggio di avviso, ma il valore viene ignorato.  
  
`[ @subscriber_password = ] 'subscriber_password'` È la password del sottoscrittore. *subscriber_password* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_password* viene **sysname**, con un valore predefinito è NULL. Le password del Sottoscrittore vengono crittografate automaticamente.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. Se viene specificato un valore per questo parametro, viene visualizzato un messaggio di avviso, ma il valore viene ignorato.  
  
`[ @distributor = ] 'distributor'` È il nome del server di distribuzione. *server di distribuzione* viene **sysname**, con un valore predefinito del valore specificato da *server di pubblicazione*.  
  
`[ @distribution_db = ] 'distribution_db'` È il nome del database di distribuzione. *distribution_db* viene **sysname**, con un valore predefinito NULL.  
  
`[ @distributor_security_mode = ] distributor_security_mode` È la modalità di sicurezza da utilizzare quando ci si connette a un server di distribuzione durante la sincronizzazione. *distributor_security_mode* viene **int**, il valore predefinito è **1**. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'` È l'account di accesso da utilizzare quando ci si connette a un server di distribuzione durante la sincronizzazione. *distributor_login* è obbligatorio se *distributor_security_mode* è impostata su **0**. *distributor_login* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @distributor_password = ] 'distributor_password'` È la password del server di distribuzione. *distributor_password* è obbligatorio se *distributor_security_mode* è impostata su **0**. *distributor_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa. Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @optional_command_line = ] 'optional_command_line'` È un prompt dei comandi facoltativo specificato per l'agente di distribuzione. Ad esempio, **- DefinitionFile** C:\Distdef.txt o **- CommitBatchSize** 10. *optional_command_line* viene **nvarchar (4000)** , con un valore predefinito di una stringa vuota.  
  
`[ @frequency_type = ] frequency_type` È la frequenza con cui pianificare l'agente di distribuzione. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2** (impostazione predefinita)|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64**|Avvio automatico|  
|**128**|Periodica|  
  
> [!NOTE]  
>  Se si specifica un valore di **64** fa sì che l'agente di distribuzione per l'esecuzione in modalità continua. Corrisponde all'impostazione di **-continua** parametro per l'agente. Per altre informazioni, vedere [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
`[ @frequency_interval = ] frequency_interval` Il valore da applicare alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è 1.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data dell'agente di distribuzione. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, il valore predefinito è **1**.  
  
`[ @frequency_subday = ] frequency_subday` È la frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, il valore predefinito è **1**.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'agente di distribuzione è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, il valore predefinito è **0**.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno quando si arresta l'agente di distribuzione è pianificata, nel formato HHMMSS. *active_end_time_of_day* viene **int**, il valore predefinito è **0**.  
  
`[ @active_start_date = ] active_start_date` È la data della prima l'agente di distribuzione pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, il valore predefinito è **0**.  
  
`[ @active_end_date = ] active_end_date` La data di arresto dell'agente di distribuzione è pianificata, nel formato aaaammgg. *active_end_date* viene **int**, il valore predefinito è **0**.  
  
`[ @distribution_jobid = ] _distribution_jobidOUTPUT` È l'ID dell'agente di distribuzione per questo processo. *distribution_jobid* viene **Binary (16)** , valore predefinito NULL che è un parametro di OUTPUT.  
  
`[ @encrypted_distributor_password = ] encrypted_distributor_password` L'impostazione *encrypted_distributor_password* non è più supportata. Tentativo di impostare questo **bit** parametro per **1** comporterà un errore.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` È se la sottoscrizione può essere sincronizzata tramite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gestione sincronizzazione. *enabled_for_syncmgr* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **false**, la sottoscrizione non è registrata con Gestione sincronizzazione Microsoft. Se **true**, la sottoscrizione viene registrata con Gestione sincronizzazione e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
`[ @ftp_address = ] 'ftp_address'` Per la compatibilità con le versioni precedenti.  
  
`[ @ftp_port = ] ftp_port` Per la compatibilità con le versioni precedenti.  
  
`[ @ftp_login = ] 'ftp_login'` Per la compatibilità con le versioni precedenti.  
  
`[ @ftp_password = ] 'ftp_password'` Per la compatibilità con le versioni precedenti.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'_` Specifica il percorso della cartella alternativa per lo snapshot. *alternate_snapshot_folder* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
`[ @working_directory = ] 'working_director'` È il nome della directory di lavoro utilizzata per archiviare i file di dati e dello schema per la pubblicazione. *working_directory* viene **nvarchar(255**, con un valore predefinito è NULL. Il nome deve essere specificato in formato UNC.  
  
`[ @use_ftp = ] 'use_ftp'` Specifica l'utilizzo di FTP anziché del protocollo normale per recuperare gli snapshot. *use_ftp* viene **nvarchar(5**, con un valore predefinito è FALSE.  
  
`[ @publication_type = ] publication_type` Specifica il tipo di replica della pubblicazione. *publication_type* è un **tinyint** con valore predefinito è **0**. Se **0**, la pubblicazione è un tipo di transazione. Se **1**, la pubblicazione è un tipo di snapshot. Se **2**, pubblicazione è di tipo merge.  
  
`[ @dts_package_name = ] 'dts_package_name'` Specifica il nome del pacchetto DTS. *dts_package_name* è un **sysname** con valore predefinito è NULL. Per specificare, ad esempio, il nome di pacchetto `DTSPub_Package`, il parametro deve essere `@dts_package_name = N'DTSPub_Package'`.  
  
`[ @dts_package_password = ] 'dts_package_password'` Specifica la password del pacchetto, se presente. *dts_package_password* viene **sysname** con un valore predefinito è NULL, ovvero una password non è incluso nel pacchetto.  
  
> [!NOTE]  
>  È necessario specificare una password se *dts_package_name* è specificato.  
  
`[ @dts_package_location = ] 'dts_package_location'` Specifica il percorso del pacchetto. *dts_package_location* è un **nvarchar (12)** , il valore predefinito è **sottoscrittore**. La posizione del pacchetto può essere **distributore** oppure **sottoscrittore**.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_activation* su un valore diverso da **false** genererà un errore.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_server_name* su qualsiasi valore diverso da NULL, verrà generato un errore.  
  
`[ @job_name = ] 'job_name'` È il nome di un processo dell'agente esistente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando la sottoscrizione verrà sincronizzata mediante un processo esistente anziché un nuovo processo creato (impostazione predefinita). Se non si è un membro del **sysadmin** ruolo predefinito del server, è necessario specificare *job_login* e *job_password* quando si specifica *job_name*.  
  
`[ @job_login = ] 'job_login'` È l'account di accesso per l'account di Windows con cui viene eseguito l'agente. *job_login* viene **nvarchar(257)** , non prevede alcun valore predefinito. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al Sottoscrittore.  
  
`[ @job_password = ] 'job_password'` È la password per l'account di Windows con cui viene eseguito l'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addpullsubscription_agent** viene utilizzata nella replica snapshot e transazionale.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addpullsubscription_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una sottoscrizione pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
