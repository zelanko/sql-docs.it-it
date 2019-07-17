---
title: sp_addmergepushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
ms.openlocfilehash: e24659cc7880a5df34aa451c5051e77b8a4c59d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117948"
---
# <a name="spaddmergepushsubscriptionagent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo processo dell'agente utilizzato per la pianificazione della sincronizzazione di una sottoscrizione push in una replica di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` È la modalità di sicurezza da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_security_mode* viene **int**, con un valore predefinito è 1. Se **0**, specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. Se **1**, specifica l'autenticazione di Windows.  
  
`[ @subscriber_login = ] 'subscriber_login'` È l'account di accesso da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_login* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_login* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_password = ] 'subscriber_password'` Password del sottoscrittore per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. *subscriber_password* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_password* viene **sysname**, con un valore predefinito è NULL. Le password del Sottoscrittore vengono crittografate automaticamente.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @publisher_security_mode = ] publisher_security_mode` È la modalità di sicurezza da utilizzare quando ci si connette a un server di pubblicazione durante la sincronizzazione. *publisher_security_mode* viene **int**, con un valore predefinito è 1. Se **0**, specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. Se **1**, specifica l'autenticazione di Windows.  
  
`[ @publisher_login = ] 'publisher_login'` È l'account di accesso da utilizzare quando ci si connette a un server di pubblicazione durante la sincronizzazione. *publisher_login* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @publisher_password = ] 'publisher_password'` Password utilizzata durante la connessione al server di pubblicazione. *publisher_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @job_login = ] 'job_login'` È l'account di accesso per l'account di Windows con cui viene eseguito l'agente. *job_login* viene **nvarchar(257)** , con un valore predefinito NULL. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al server di distribuzione e per le connessioni al Sottoscrittore e al server di pubblicazione in caso di utilizzo dell'autenticazione integrata di Windows.  
  
`[ @job_password = ] 'job_password'` È la password per l'account di Windows con cui viene eseguito l'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @job_name = ] 'job_name'` È il nome di un processo dell'agente esistente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando la sottoscrizione viene sincronizzata utilizzando un processo esistente anziché un nuovo processo (impostazione predefinita). Se non si è un membro del **sysadmin** ruolo predefinito del server, è necessario specificare *job_login* e *job_password* quando si specifica *job_name*.  
  
`[ @frequency_type = ] frequency_type` È la frequenza con cui pianificare l'agente di Merge. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
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
  
`[ @frequency_interval = ] frequency_interval` Giorni in cui viene eseguito l'agente di Merge. *frequency_interval* viene **int**, e può essere uno dei valori seguenti.  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data dell'agente di Merge. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
|NULL (predefinito)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
`[ @frequency_subday = ] frequency_subday` È la frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
|NULL (predefinito)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'agente di Merge è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno quando si arresta l'agente di Merge viene pianificata, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_date = ] active_start_date` È la data della prima l'agente di Merge pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_date = ] active_end_date` La data di arresto dell'agente di Merge viene pianificata, nel formato aaaammgg. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Specifica se la sottoscrizione può essere sincronizzata tramite Gestione sincronizzazione Microsoft Windows. *enabled_for_syncmgr* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **false**, la sottoscrizione non è registrata con Gestione sincronizzazione Microsoft. Se **true**, la sottoscrizione viene registrata con Gestione sincronizzazione e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_addmergepushsubscription_agent** viene utilizzata nella replica di tipo merge e utilizza funzionalità simili a quelle [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addmergepushsubscription_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
