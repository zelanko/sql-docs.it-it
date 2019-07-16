---
title: sp_update_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7914e3b56dd02d96c02835bf6b4dcc5eb90e8f4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084881"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica l'impostazione di un passaggio in un processo utilizzato per l'esecuzione di operazioni automatizzate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` Il numero di identificazione del processo a cui appartiene il passaggio. *job_id*viene **uniqueidentifier**, con un valore predefinito è NULL. Entrambi *job_id* oppure *job_name* deve essere specificato ma non è possibile specificarli entrambi.  
  
`[ @job_name = ] 'job_name'` Il nome del processo a cui appartiene il passaggio. *nome_processo*viene **sysname**, con un valore predefinito è NULL. Entrambi *job_id* oppure *job_name* deve essere specificato ma non è possibile specificarli entrambi.  
  
`[ @step_id = ] step_id` Il numero di identificazione per il passaggio del processo da modificare. Questo numero non è modificabile. *step_id*viene **int**, non prevede alcun valore predefinito.  
  
`[ @step_name = ] 'step_name'` È un nuovo nome per il passaggio. *step_name*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subsystem = ] 'subsystem'` Il sottosistema utilizzato da Microsoft SQL Server Agent per eseguire *comando*. *sottosistema* viene **nvarchar (40)** , con un valore predefinito è NULL.  
  
`[ @command = ] 'command'` I comandi da eseguire tramite *sottosistema*. *comando* viene **nvarchar (max)** , con un valore predefinito è NULL.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code` Il valore restituito da una **CmdExec** comando del sottosistema per indicare che *comando* eseguito correttamente. *success_code* viene **int**, con un valore predefinito è NULL.  
  
`[ @on_success_action = ] success_action` L'azione da eseguire se il passaggio ha esito positivo. *success_action* viene **tinyint**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione (azione)|  
|-----------|----------------------------|  
|**1**|Uscita in caso di esito positivo|  
|**2**|Uscita in caso di esito negativo|  
|**3**|Esecuzione del passaggio successivo|  
|**4**|Andare al passaggio *success_step_id.*|  
  
`[ @on_success_step_id = ] success_step_id` Il numero di identificazione del passaggio del processo da eseguire se il passaggio ha esito positivo e *success_action* viene **4**. *success_step_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @on_fail_action = ] fail_action` L'azione da eseguire se il passaggio ha esito negativo. *fail_action* viene **tinyint**, con un valore predefinito è NULL e può avere uno dei valori seguenti.  
  
|Value|Descrizione (azione)|  
|-----------|----------------------------|  
|**1**|Uscita in caso di esito positivo|  
|**2**|Uscita in caso di esito negativo|  
|**3**|Esecuzione del passaggio successivo|  
|**4**|Andare al passaggio *fail_step_id * *.*|  
  
`[ @on_fail_step_id = ] fail_step_id` Il numero di identificazione del passaggio del processo da eseguire se il passaggio ha esito negativo e *fail_action* viene **4**. *fail_step_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *server* viene **nvarchar (128)** , con un valore predefinito è NULL.  
  
`[ @database_name = ] 'database'` Il nome del database in cui eseguire un [!INCLUDE[tsql](../../includes/tsql-md.md)] passaggio. *database*viene **sysname**. I nomi racchiusi tra parentesi quadre ([ ]) non sono ammessi. Il valore predefinito è NULL.  
  
`[ @database_user_name = ] 'user'` Il nome dell'account utente da utilizzare quando viene eseguito un [!INCLUDE[tsql](../../includes/tsql-md.md)] passaggio. *utente*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @retry_attempts = ] retry_attempts` Il numero di tentativi da utilizzare se questo passaggio ha esito negativo. *retry_attempts*viene **int**, con un valore predefinito è NULL.  
  
`[ @retry_interval = ] retry_interval` La quantità di tempo in minuti tra i tentativi di ripetizione dei tentativi. *retry_interval* viene **int**, con un valore predefinito è NULL.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` Il nome del file in cui viene salvato l'output di questo passaggio. *file_name* viene **nvarchar (200)** , con un valore predefinito è NULL. Questo parametro è valido solo con comandi eseguiti nei sottosistemi [!INCLUDE[tsql](../../includes/tsql-md.md)] o CmdExec.  
  
 Per impostare nuovamente output_file_name nuovamente su NULL, è necessario impostare *nuovamente output_file_name* su una stringa vuota (' ') o in una stringa di caratteri vuoti, ma è possibile utilizzare il **CHAR(32)** (funzione). Ad esempio, impostare questo argomento su una stringa vuota nel modo descritto di seguito:  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` Un'opzione che controlla il comportamento. *i flag* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0** (predefinito)|L'output sovrascrive il contenuto del file di output.|  
|**2**|L'output viene aggiunto alla fine del file di output.|  
|**4**|L'output del passaggio del processo Transact-SQL viene scritto nella cronologia dei passaggi|  
|**8**|Il log viene scritto nella tabella. La cronologia esistente viene sovrascritta|  
|**16**|Il log viene scritto nella tabella in aggiunta alla cronologia esistente|  
  
`[ @proxy_id = ] proxy_id` Il numero di ID del proxy che viene eseguito il passaggio del processo. *proxy_id* è di tipo **int**, con un valore predefinito è NULL. Se nessun *proxy_id* è specificato, nessun *proxy_name* viene specificato e non *user_name* viene specificato, il passaggio del processo viene eseguito come account del servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy che viene eseguito il passaggio del processo. *proxy_name* è di tipo **sysname**, con un valore predefinito è NULL. Se nessun *proxy_id* è specificato, nessun *proxy_name* viene specificato e non *user_name* viene specificato, il passaggio del processo viene eseguito come account del servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_update_jobstep** deve essere eseguita la **msdb** database.  
  
 L'aggiornamento di un passaggio di processo comporta un incremento del numero di versione del processo.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** può aggiornare un passaggio di processo appartenente a un altro utente.  
  
 Se il passaggio di processo richiede l'accesso a un proxy, l'autore del passaggio deve disporre dell'accesso al proxy per tale passaggio. Tutti i sottosistemi, a esclusione di Transact-SQL, richiedono un account proxy. I membri del **sysadmin** hanno accesso a tutti i proxy e utilizzare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio agente per il proxy.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificato il numero di tentativi per il primo passaggio del processo `Weekly Sales Data Backup`. Dopo aver eseguito questo esempio, il numero di tentativi sarà `10`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare o modificare processi](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
