---
title: sp_update_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c12e078505c8049511e59973c26d6a1417c7eae0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537853"
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica gli attributi di un processo.  
  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` Il numero di identificazione del processo da aggiornare. *job_id*is **uniqueidentifier**.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **nvarchar (128)**.  
  
> **NOTA:** Entrambi *job_id* oppure *job_name* deve essere specificato ma non è possibile specificarli entrambi.  
  
`[ @new_name = ] 'new_name'` Il nuovo nome per il processo. *new_name* viene **nvarchar (128)**.  
  
`[ @enabled = ] enabled` Specifica se il processo è abilitato (**1**) o non abilitato (**0**). *abilitata* viene **tinyint**.  
  
`[ @description = ] 'description'` La descrizione del processo. *Descrizione* viene **nvarchar(512)**.  
  
`[ @start_step_id = ] step_id` Il numero di identificazione del primo passaggio da eseguire per il processo. *step_id* viene **int**.  
  
`[ @category_name = ] 'category'` La categoria del processo. *category* is **nvarchar(128)**.  
  
`[ @owner_login_name = ] 'login'` Il nome dell'account di accesso proprietario del processo. *account di accesso* viene **nvarchar (128)** solo i membri del **sysadmin** ruolo predefinito del server è possibile modificare la proprietà dei processi.  
  
`[ @notify_level_eventlog = ] eventlog_level` Specifica quando inserire una voce nel registro applicazioni di Microsoft Windows per questo processo. *eventlog_level*viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (azione)|  
|-----------|----------------------------|  
|**0**|Never|  
|**1**|In caso di esito positivo|  
|**2**|In caso di esito negativo|  
|**3**|Always|  
  
`[ @notify_level_email = ] email_level` Specifica quando inviare un messaggio di posta elettronica al termine del processo. *email_level*viene **int**. *email_level*Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_level_netsend = ] netsend_level` Specifica quando inviare un messaggio di rete al termine del processo. *netsend_level*viene **int**. *netsend_level*Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_level_page = ] page_level` Specifica quando inviare una pagina al termine del processo. *page_level* viene **int**. *page_level*Usa gli stessi valori *eventlog_level*.  
  
`[ @notify_email_operator_name = ] 'operator_name'` Il nome dell'operatore a cui viene inviato il messaggio di posta elettronica quando *email_level* viene raggiunto. *nome_posta_elettronica* viene **nvarchar (128)**.  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` Il nome dell'operatore a cui viene inviato il messaggio di rete. *netsend_operator* is **nvarchar(128)**.  
  
`[ @notify_page_operator_name = ] 'page_operator'` Il nome dell'operatore a cui viene inviata una pagina. *page_operator* viene **nvarchar (128)**.  
  
`[ @delete_level = ] delete_level` Specifica quando eliminare il processo. *delete_value*viene **int**. *i possibili*Usa gli stessi valori *eventlog_level*.  
  
`[ @automatic_post = ] automatic_post` Riservato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_update_job** deve essere eseguita la **msdb** database.  
  
 **sp_update_job** modificare solo le impostazioni per il parametro che vengono specificati i valori. Se si omette un parametro, viene mantenuta l'impostazione corrente.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** può utilizzare questa stored procedure per modificare gli attributi dei processi di proprietà di altri utenti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono modificati il nome, la descrizione e lo stato di attivazione del processo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
