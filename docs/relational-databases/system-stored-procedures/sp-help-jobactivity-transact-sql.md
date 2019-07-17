---
title: sp_help_jobactivity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
author: stevestein
ms.author: sstein
ms.openlocfilehash: 95283eee1a38dbafd9824986188df565103de06c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054982"
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elenca le informazioni sullo stato di run-time dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` ID del processo. *job_id*viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo*viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @session_id = ] session_id` L'id di sessione per segnalare informazioni. *session_id* viene **int**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il set di risultati seguente:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Numero di identificazione della sessione dell'agente.|  
|**job_id**|**uniqueidentifier**|Identificatore del processo.|  
|**job_name**|**sysname**|Nome del processo|  
|**run_requested_date**|**datetime**|Data e ora previste per l'esecuzione del processo.|  
|**run_requested_source**|**sysname**|Origine dalla richiesta di esecuzione del processo. I possibili valori sono i seguenti:<br /><br /> **1** = esecuzione in base a una pianificazione<br /><br /> **2** = esecuzione in risposta a un avviso<br /><br /> **3** = esecuzione all'avvio<br /><br /> **4** = esecuzione da parte dell'utente<br /><br /> **6** = esecuzione in una pianificazione di inattività CPU|  
|**queued_date**|**datetime**|Data e ora di inserimento della richiesta nella coda. NULL se il processo è stato eseguito direttamente.|  
|**start_execution_date**|**datetime**|Data e ora di assegnazione del processo a un thread eseguibile.|  
|**last_executed_step_id**|**int**|ID dell'ultimo passaggio del processo eseguito.|  
|**last_exectued_step_date**|**datetime**|Data e ora di inizio dell'esecuzione dell'ultimo passaggio del processo.|  
|**stop_execution_date**|**datetime**|Data e ora di arresto dell'esecuzione del processo.|  
|**next_scheduled_run_date**|**datetime**|Data e ora pianificate per la successiva esecuzione del processo.|  
|**job_history_id**|**int**|Identificatore della cronologia processo nella tabella delle cronologie processi.|  
|**message**|**nvarchar(1024)**|Messaggio generato durante l'ultima esecuzione del processo.|  
|**run_status**|**int**|Stato restituito dall'ultima esecuzione del processo:<br /><br /> **0** = operazione non riuscita<br /><br /> **1** = ha avuto esito positivo<br /><br /> **3** = annullato<br /><br /> **5** = stato sconosciuto|  
|**operator_id_emailed**|**int**|ID dell'operatore comunicato tramite posta elettronica al completamento del processo.|  
|**operator_id_netsent**|**int**|Numero ID dell'operatore comunicato tramite **net send** al completamento del processo.|  
|**operator_id_paged**|**int**|ID dell'operatore comunicato tramite cercapersone al completamento del processo.|  
  
## <a name="remarks"></a>Note  
 Tramite questa procedura viene generato uno snapshot dello stato corrente dei processi. I risultati restituiti rappresentano le informazioni disponibili al momento dell'elaborazione della richiesta.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent crea un ID di sessione ogni volta che viene avviato. L'id di sessione viene archiviato nella tabella **syssessions**.  
  
 Se non si specifica *session_id* è specificato, elenca le informazioni relative alla sessione più recente.  
  
 Se non si specifica *nome_processo* oppure *job_id* è specificato, elenca le informazioni per tutti i processi.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, i membri del **sysadmin** ruolo predefinito del server può eseguire questa stored procedure. Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** può visualizzare l'attività dei processi di proprietà di altri utenti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sull'attività di tutti i processi per i quali l'utente corrente dispone dell'autorizzazione di visualizzazione.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
