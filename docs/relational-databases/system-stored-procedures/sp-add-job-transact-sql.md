---
title: sp_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb371603230c0c3b6fbee0012c89ce402711fb6e
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493233"
---
# <a name="spaddjob-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo processo eseguito dal servizio SQLServerAgent.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_name = ] 'job_name'` Il nome del processo. Il nome deve essere univoco e non può contenere la percentuale (**%**) caratteri. *nome_processo*viene **nvarchar (128)**, non prevede alcun valore predefinito.  
  
`[ @enabled = ] enabled` Indica lo stato del processo aggiunto. *abilitata*viene **tinyint**, con un valore predefinito è 1 (abilitato). Se **0**, il processo non è abilitato e non viene eseguito in base alla relativa pianificazione; tuttavia, può essere eseguito manualmente.  
  
`[ @description = ] 'description'` La descrizione del processo. *Descrizione* viene **nvarchar(512)**, con un valore predefinito è NULL. Se *descrizione* viene non omesso, viene utilizzata "Nessuna descrizione disponibile".  
  
`[ @start_step_id = ] step_id` Il numero di identificazione del primo passaggio da eseguire per il processo. *step_id*viene **int**, con un valore predefinito è 1.  
  
`[ @category_name = ] 'category'` La categoria per il processo. *categoria*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @category_id = ] category_id` Un meccanismo indipendente dal linguaggio per specificare una categoria di processi. *category_id*viene **int**, con un valore predefinito è NULL.  
  
`[ @owner_login_name = ] 'login'` Il nome dell'account di accesso proprietario del processo. *account di accesso*viene **sysname**, con un valore predefinito è NULL, che viene interpretato come nome account di accesso corrente. Solo i membri del **sysadmin** ruolo predefinito del server può impostare o modificare il valore per **@owner_login_name**. Se gli utenti che non sono membri del **sysadmin** ruolo impostare o modificare il valore di **@owner_login_name**, esecuzione di questa stored procedure ha esito negativo e viene restituito un errore.  
  
`[ @notify_level_eventlog = ] eventlog_level` Un valore che indica quando inserire una voce nel registro applicazioni di Microsoft Windows per questo processo. *eventlog_level*viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Never|  
|**1**|In caso di esito positivo|  
|**2** (impostazione predefinita)|In caso di esito negativo|  
|**3**|Always|  
  
`[ @notify_level_email = ] email_level` Un valore che indica quando inviare un messaggio di posta elettronica al termine del processo. *email_level*viene **int**, il valore predefinito è **0**, non ovvero mai. *email_level*Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_level_netsend = ] netsend_level` Un valore che indica quando inviare un messaggio di rete al termine del processo. *netsend_level*viene **int**, il valore predefinito è **0**, non ovvero mai. *netsend_level* Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_level_page = ] page_level` Un valore che indica quando inviare una pagina al termine del processo. *page_level*viene **int**, il valore predefinito è **0**, non ovvero mai. *page_level*Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_email_operator_name = ] 'email_name'` Il nome di posta elettronica della persona a cui inviare il messaggio di posta elettronica quando *email_level* viene raggiunto. *nome_posta_elettronica* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @notify_netsend_operator_name = ] 'netsend_name'` Il nome dell'operatore a cui viene inviato il messaggio di rete dopo il completamento del processo. *netsend_name*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @notify_page_operator_name = ] 'page_name'` Il nome della persona a cercapersone al termine del processo. *page_name*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @delete_level = ] delete_level` Un valore che indica quando eliminare il processo. *delete_value*viene **int**, valore predefinito è 0, non ovvero mai. *i possibili*Usa gli stessi valori *eventlog_level*.  
  
> [!NOTE]  
>  Quando *i possibili* viene **3**, il processo viene eseguito una sola volta, indipendentemente dalle pianificazioni definite per il processo. Inoltre, se un processo si autoelimina, viene eliminato anche il contenuto della cronologia corrispondente.  
  
`[ @job_id = ] _job_idOUTPUT` Numero di identificazione assegnato al processo se creato correttamente. *job_id*è una variabile di output di tipo **uniqueidentifier**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **@originating_server** esiste **sp_add_job** ma non è elencato nella sezione argomenti. **@originating_server** è riservato per uso interno.  
  
 Dopo aver **sp_add_job** è stata eseguita per aggiungere un processo **sp_add_jobstep** può essere utilizzato per aggiungere i passaggi che eseguono le attività per il processo. **sp_add_jobschedule** può essere usato per creare la pianificazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio agente utilizza per eseguire il processo. Uso **sp_add_jobserver** per impostare le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza in cui viene eseguito il processo, e **sp_delete_jobserver** per rimuovere il processo dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza.  
  
 Se il processo verrà eseguito in uno o più server di destinazione in un ambiente multiserver, utilizzare **sp_apply_job_to_targets** per impostare i server di destinazione o i gruppi di server per il processo di destinazione. Per rimuovere i processi dal server di destinazione o gruppi di server di destinazione, usare **sp_remove_job_from_targets**.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa stored procedure, gli utenti devono essere un membro del **sysadmin** ruolo predefinito del server, oppure disporre di uno dei seguenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente ruoli predefiniti del database, che si trovano nel **msdb** database:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni sulle autorizzazioni specifiche che sono associati a ognuno di questi ruoli del database, vedere [ruoli predefiniti del Database SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** ruolo predefinito del server può impostare o modificare il valore per **@owner_login_name**. Se gli utenti che non sono membri del **sysadmin** ruolo impostare o modificare il valore di **@owner_login_name**, esecuzione di questa stored procedure ha esito negativo e viene restituito un errore.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-adding-a-job"></a>A. Aggiunta di un processo  
 In questo esempio viene aggiunto il nuovo processo denominato `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>b. Aggiunta di un processo con informazioni inviate tramite il cercapersone, la posta elettronica e la rete  
 In questo esempio viene creato il processo `Ad hoc Sales Data Backup` che in caso di esito negativo invia una notifica all'operatore `François Ajenstat` (tramite cercapersone, posta elettronica o messaggio popup di rete), mentre in caso di esito positivo si autoelimina.  
  
> [!NOTE]  
>  In questo esempio si presuppone che l'operatore `François Ajenstat` e l'account di accesso `françoisa` esistano già.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
