---
title: sp_help_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7ddacb0951b25469404b96d41ec81d2eaaba9cc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530579"
---
# <a name="sphelpjobstep-transact-sql"></a>sp_help_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui passaggi di un processo utilizzato dal servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'esecuzione di attività automatizzate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] 'job_id'` ID del processo per cui restituire informazioni sul processo. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @step_id = ] step_id` Il numero di identificazione del passaggio del processo. Se viene omesso, vengono inclusi tutti i passaggi del processo. *step_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @step_name = ] 'step_name'` Il nome del passaggio del processo. *step_name* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @suffix = ] suffix` Un flag che indica se aggiungere una descrizione di testo per il **flag** colonna nell'output. *suffisso*viene **bit**, il valore predefinito **0**. Se *suffisso* viene **1**, aggiungere una descrizione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificatore univoco del passaggio.|  
|**step_name**|**sysname**|Nome del passaggio del processo.|  
|**subsystem**|**nvarchar(40)**|Sottosistema in cui eseguire il comando del passaggio.|  
|**comando**|**nvarchar(max)**|Comando eseguito nel passaggio.|  
|**flags**|**int**|Maschera di bit dei valori che controllano il funzionamento del passaggio.|  
|**cmdexec_success_code**|**int**|Per un **CmdExec** passaggio, questo è il codice di uscita del processo di un comando eseguito correttamente.|  
|**on_success_action**|**tinyint**|Azione da eseguire se il passaggio viene eseguito correttamente:<br /><br /> **1** = Quit il processo completato correttamente.<br /><br /> **2** = Quit di esito negativo.<br /><br /> **3** = andare al passaggio successivo.<br /><br /> **4** = esecuzione di un passaggio.|  
|**on_success_step_id**|**int**|Se **on_success_action** è 4, indica il passaggio da eseguire.|  
|**on_fail_action**|**tinyint**|Azione da eseguire se il passaggio non viene eseguito correttamente. I valori sono uguali a quelli **on_success_action**.|  
|**on_fail_step_id**|**int**|Se **on_fail_action** è 4, indica il passaggio da eseguire.|  
|**server**|**sysname**|Riservato.|  
|**database_name**|**sysname**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], indica il database in cui viene eseguito il comando.|  
|**database_user_name**|**sysname**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], indica il contesto utente del database in cui viene eseguito il comando.|  
|**retry_attempts**|**int**|Numero massimo di tentativi di esecuzione del comando (nel caso in cui non sia stato eseguito correttamente).|  
|**retry_interval**|**int**|Intervallo in minuti che intercorre tra un tentativo e il successivo.|  
|**os_run_priority**|**int**|Riservato.|  
|**output_file_name**|**nvarchar(200)**|In quale comando deve essere scritto l'output di file ([!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, e **PowerShell** solo per i passaggi).|  
|**last_run_outcome**|**int**|Risultato dell'ultima esecuzione del passaggio:<br /><br /> **0** = non è riuscita<br /><br /> **1** = Succeeded<br /><br /> **2** = Retry<br /><br /> **3** = annullato<br /><br /> **5** = sconosciuto|  
|**last_run_duration**|**int**|Durata in secondi dell'ultima esecuzione del passaggio.|  
|**last_run_retries**|**int**|Numero di tentativi di esecuzione del comando durante l'ultima esecuzione del passaggio.|  
|**last_run_date**|**int**|Data di inizio dell'ultima esecuzione del passaggio.|  
|**last_run_time**|**int**|Ora di inizio dell'ultima esecuzione del passaggio.|  
|**proxy_id**|**int**|Proxy per il passaggio del processo.|  
  
## <a name="remarks"></a>Note  
 **sp_help_jobstep** è il **msdb** database.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** possono visualizzare solo i passaggi di processo per cui sono proprietari.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. Restituzione di informazioni su tutti i passaggi di un processo specifico  
 In questo esempio vengono restituiti tutti i passaggi del processo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>B. Restituzione di informazioni su un determinato passaggio di un processo  
 Nell'esempio seguente vengono restituite informazioni sul primo passaggio del processo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
