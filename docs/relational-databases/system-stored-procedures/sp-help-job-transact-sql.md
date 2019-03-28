---
title: sp_help_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_job_TSQL
- sp_help_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_job
ms.assetid: 8a8b6104-e0e4-4d07-a2c3-f4243ee0d6fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 509dd27a784fd14b5aefc811065b265f37c3f6c3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528143"
---
# <a name="sphelpjob-transact-sql"></a>sp_help_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui processi utilizzati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'esecuzione di attività automatizzate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_job { [ @job_id = ] job_id  
[ @job_name = ] 'job_name' }   
     [ , [ @job_aspect = ] 'job_aspect' ]   
     [ , [ @job_type = ] 'job_type' ]   
     [ , [ @owner_login_name = ] 'login_name' ]   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @enabled = ] enabled ]   
     [ , [ @execution_status = ] status ]   
     [ , [ @date_comparator = ] 'date_comparison' ]   
     [ , [ @date_created = ] date_created ]   
     [ , [ @date_last_modified = ] date_modified ]   
     [ , [ @description = ] 'description_pattern' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` ID del processo. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Per visualizzare un processo specifico, ovvero *job_id* oppure *job_name* deve essere specificato.  Omettere entrambe *job_id* e *job_name* per restituire informazioni su tutti i processi.
  
`[ @job_aspect = ] 'job_aspect'` Attributo del processo da visualizzare. *job_aspect* viene **varchar(9)**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**ALL**|Informazioni sugli attributi del processo|  
|**JOB**|Informazioni sul processo|  
|**PIANIFICAZIONI**|Informazioni sulla pianificazione|  
|**STEPS**|Informazioni sui passaggi del processo|  
|**TARGETS**|Informazioni sul server di destinazione|  
  
`[ @job_type = ] 'job_type'` Il tipo di processo da includere nel report. *job_type* viene **varchar(12)**, con un valore predefinito è NULL. *job_type* può essere **locale** oppure **MULTISERVER**.  
  
`[ @owner_login_name = ] 'login_name'` Il nome di account di accesso del proprietario del processo. *login_name* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subsystem = ] 'subsystem'` Il nome del sottosistema. *sottosistema* viene **nvarchar (40)**, con un valore predefinito è NULL.  
  
`[ @category_name = ] 'category'` Il nome della categoria. *categoria* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @enabled = ] enabled` Un numero che indica se visualizzare informazioni per abilitata i processi o per quelli disabilitati. *abilitata* viene **tinyint**, con un valore predefinito è NULL. **1** indica i processi abilitati, e **0** quelli disabilitati.  
  
`[ @execution_status = ] status` Lo stato di esecuzione per i processi. *lo stato* viene **int**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Restituisce solo i processi non inattivi o sospesi.|  
|**1**|In esecuzione.|  
|**2**|In attesa di un thread.|  
|**3**|Tra due tentativi.|  
|**4**|Operazione inattiva.|  
|**5**|Sospeso.|  
|**7**|Esecuzione delle azioni finali in corso.|  
  
`[ @date_comparator = ] 'date_comparison'` Operatore di confronto da utilizzare nei confronti tra *date_created* e *date_modified*. *date_comparison* viene **char (1)** e può essere =, \<, o >.  
  
`[ @date_created = ] date_created` Data che di creazione del processo. *Date_Created*viene **datetime**, con un valore predefinito è NULL.  
  
`[ @date_last_modified = ] date_modified` La data che dell'ultima modifica del processo. *date_modified* viene **datetime**, con un valore predefinito è NULL.  
  
`[ @description = ] 'description_pattern'` La descrizione del processo. *description_pattern* viene **nvarchar(512)**, con un valore predefinito è NULL. *description_pattern* può includere i caratteri jolly di SQL Server per criteri di ricerca.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Se viene specificato alcun argomento, **sp_help_job** restituisce questo set di risultati.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ID univoco del processo.|  
|**originating_server**|**nvarchar(30)**|Nome del server di provenienza del processo.|  
|**name**|**sysname**|Nome del processo|  
|**enabled**|**tinyint**|Indica se il processo è abilitato per l'esecuzione.|  
|**description**|**nvarchar(512)**|Descrizione del processo.|  
|**start_step_id**|**int**|ID del passaggio del processo da cui deve iniziare l'esecuzione.|  
|**category**|**sysname**|Categoria del processo.|  
|**owner**|**sysname**|Proprietario del processo.|  
|**notify_level_eventlog**|**int**|**Maschera di bit** che indica in quali circostanze un evento di notifica deve essere registrato nel registro applicazioni di Microsoft Windows. I possibili valori sono i seguenti:<br /><br /> **0** = Never<br /><br /> **1** = in caso di esito positivo del processo<br /><br /> **2** = in caso di esito negativo del processo<br /><br /> **3** = ogni volta che il completamento del processo (indipendentemente dal risultato processo)|  
|**notify_level_email**|**int**|**Maschera di bit** che indica in quali circostanze deve essere inviato un messaggio di posta elettronica di notifica quando un processo viene completato. I valori possibili sono uguali a quelle per **notify_level_eventlog**.|  
|**notify_level_netsend**|**int**|**Maschera di bit** che indica in quali circostanze deve essere inviato un messaggio di rete quando un processo viene completato. I valori possibili sono uguali a quelle per **notify_level_eventlog**.|  
|**notify_level_page**|**int**|**Maschera di bit** che indica in quali casi una pagina deve essere inviata quando un processo viene completato. I valori possibili sono uguali a quelle per **notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|Nome di posta elettronica dell'operatore a cui inviare la notifica.|  
|**notify_netsend_operator**|**sysname**|Nome di computer o di utente specificato quando si invia un messaggio in rete.|  
|**notify_page_operator**|**sysname**|Nome di computer o di utente specificato quando si invia un messaggio su cercapersone.|  
|**delete_level**|**int**|**Maschera di bit** che indica in quali circostanze l'eliminazione di un processo al termine. I valori possibili sono uguali a quelle per **notify_level_eventlog**.|  
|**date_created**|**datetime**|Data di creazione del processo.|  
|**date_modified**|**datetime**|Data dell'ultima modifica del processo.|  
|**version_number**|**int**|Versione del processo aggiornata automaticamente in corrispondenza di ogni modifica del processo.|  
|**last_run_date**|**int**|Data dell'ultimo avvio dell'esecuzione del processo.|  
|**last_run_time**|**int**|Ora dell'ultimo avvio dell'esecuzione del processo.|  
|**last_run_outcome**|**int**|Risultato dell'ultima esecuzione del processo:<br /><br /> **0** = non è riuscita<br /><br /> **1** = Succeeded<br /><br /> **3** = annullato<br /><br /> **5** = sconosciuto|  
|**next_run_date**|**int**|Data pianificata per la successiva esecuzione del processo.|  
|**next_run_time**|**int**|Ora pianificata per la successiva esecuzione del processo.|  
|**next_run_schedule_id**|**int**|ID della successiva pianificazione di esecuzione.|  
|**current_execution_status**|**int**|Stato di esecuzione corrente.|  
|**current_execution_step**|**sysname**|Passaggio di esecuzione corrente all'interno del processo.|  
|**current_retry_attempt**|**int**|Se il processo è in esecuzione e il passaggio è stato ripetuto, indica il numero del tentativo in corso.|  
|**has_step**|**int**|Numero di passaggi del processo.|  
|**has_schedule**|**int**|Numero di pianificazioni del processo.|  
|**has_target**|**int**|Numero di server di destinazione del processo.|  
|**type**|**int**|Tipo del processo.<br /><br /> 1 = Processo locale.<br /><br /> **2** = processo multiserver.<br /><br /> **0** = processo non dispone di alcun server di destinazione.|  
  
 Se *job_id* oppure *job_name* è specificato **sp_help_job** restituisce questi set di risultati aggiuntivi per i passaggi di processo, le pianificazioni dei processi e i server di destinazione di processo.  
  
 Il set di risultati per i passaggi del processo è il seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificatore univoco (all'interno del processo) del passaggio.|  
|**step_name**|**sysname**|Nome del passaggio.|  
|**subsystem**|**nvarchar(40)**|Sottosistema in cui eseguire il comando del passaggio.|  
|**comando**|**nvarchar(3200)**|Comando da eseguire.|  
|**flags**|**nvarchar(4000)**|**Maschera di bit** dei valori che controllano il funzionamento del passaggio.|  
|**cmdexec_success_code**|**int**|Per un **CmdExec** passaggio, questo è il codice di uscita del processo di un comando eseguito correttamente.|  
|**on_success_action**|**nvarchar(4000)**|Azione da eseguire se il passaggio viene eseguito correttamente:<br /><br /> **1** = uscita in caso di esito positivo.<br /><br /> **2** = uscita in caso di esito negativo.<br /><br /> **3** = andare al passaggio successivo.<br /><br /> **4** = esecuzione di un passaggio.|  
|**on_success_step_id**|**int**|Se **on_success_action** viene **4**, indica il passaggio da eseguire.|  
|**on_fail_action**|**nvarchar(4000)**|Azione da eseguire se il passaggio non viene eseguito correttamente. I valori sono uguali a quelle per **on_success_action**.|  
|**on_fail_step_id**|**int**|Se **on_fail_action** viene **4**, indica il passaggio da eseguire.|  
|**server**|**sysname**|Riservato.|  
|**database_name**|**sysname**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], indica il database in cui verrà eseguito il comando.|  
|**database_user_name**|**sysname**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], indica il contesto utente del database in cui viene eseguito il comando.|  
|**retry_attempts**|**int**|Numero massimo di tentativi di esecuzione del comando (nel caso in cui non sia stato eseguito correttamente) oltre il quale il passaggio viene considerato errato.|  
|**retry_interval**|**int**|Intervallo di tempo in minuti che intercorre tra un tentativo e il successivo.|  
|**os_run_priority**|**varchar(4000)**|Riservato.|  
|**output_file_name**|**varchar(200)**|In quale comando deve essere scritto l'output di file ([!INCLUDE[tsql](../../includes/tsql-md.md)] e **CmdExec** solo per i passaggi).|  
|**last_run_outcome**|**int**|Risultato dell'ultima esecuzione del passaggio:<br /><br /> **0** = non è riuscita<br /><br /> **1** = Succeeded<br /><br /> **3** = annullato<br /><br /> **5** = sconosciuto|  
|**last_run_duration**|**int**|Durata in secondi dell'ultima esecuzione del passaggio.|  
|**last_run_retries**|**int**|Numero di tentativi di esecuzione del comando durante l'ultima esecuzione del passaggio.|  
|**last_run_date**|**int**|Data di inizio dell'ultima esecuzione del passaggio.|  
|**last_run_time**|**int**|Ora di inizio dell'ultima esecuzione del passaggio.|  
|**proxy_id**|**int**|Proxy per il passaggio del processo.|  
  
 Il set di risultati per le pianificazioni del processo è il seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID della pianificazione, univoco per tutti i processi.|  
|**schedule_name**|**sysname**|Nome della pianificazione, univoco soltanto per il processo specificato.|  
|**enabled**|**int**|Indica se la pianificazione è attiva (**1**) o No (**0**).|  
|**freq_type**|**int**|Valore che indica la frequenza di esecuzione del processo:<br /><br /> **1** = Once<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa al **freq_interval**<br /><br /> **64** = vengono eseguite quando **SQLServerAgent** all'avvio del servizio.|  
|**freq_interval**|**int**|Giorni in cui viene eseguito il processo. Il valore dipende dal valore della **freq_type**. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_type**|**Int**|Unità di misura per **freq_subday_interval**. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_interval**|**int**|Numerosi **freq_subday_type** periodi intercorrere tra ogni esecuzione del processo. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_relative_interval**|**int**|Pianificata del processo dei **freq_interval** ogni mese. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_recurrence_factor**|**int**|Numero di mesi tra l'esecuzione pianificata del processo.|  
|**active_start_date**|**int**|Data di inizio dell'esecuzione del processo.|  
|**active_end_date**|**int**|Data di fine dell'esecuzione del processo.|  
|**active_start_time**|**int**|Ora di inizio dell'esecuzione del processo su **active_start_date.**|  
|**active_end_time**|**int**|Ora di fine dell'esecuzione del processo sul **active_end_date**.|  
|**date_created**|**datetime**|Data di creazione della pianificazione.|  
|**schedule_description**|**nvarchar(4000)**|Descrizione in inglese della pianificazione, se richiesta.|  
|**next_run_date**|**int**|Data della successiva esecuzione del processo in base alla pianificazione.|  
|**next_run_time**|**int**|Ora della successiva esecuzione del processo in base alla pianificazione.|  
|**schedule_uid**|**uniqueidentifier**|Identificatore della pianificazione.|  
|**job_count**|**int**|Restituisce il numero di processi che fanno riferimento a questa pianificazione.|  
  
 Il set di risultati per i server di destinazione del processo è il seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|ID del server di destinazione.|  
|**server_name**|**nvarchar(30)**|Nome di computer del server di destinazione.|  
|**enlist_date**|**datetime**|Data di integrazione del server di destinazione nel server master.|  
|**last_poll_date**|**datetime**|Data dell'ultimo polling del server master eseguito dal server di destinazione.|  
|**last_run_date**|**int**|Data di inizio dell'ultima esecuzione del processo nel server di destinazione.|  
|**last_run_time**|**int**|Ora di inizio dell'ultima esecuzione del processo nel server di destinazione.|  
|**last_run_duration**|**int**|Durata dell'ultima esecuzione del processo nel server di destinazione.|  
|**last_run_outcome**|**tinyint**|Risultato dell'ultima esecuzione del processo nel server specificato:<br /><br /> **0** = non è riuscita<br /><br /> **1** = Succeeded<br /><br /> **3** = annullato<br /><br /> **5** = sconosciuto|  
|**last_outcome_message**|**nvarchar(1024)**|Messaggio visualizzato dopo l'ultima esecuzione del processo nel server di destinazione.|  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** può visualizzare solo i processi che sono proprietari. I membri del **sysadmin**, **SQLAgentReaderRole**, e **SQLAgentOperatorRole** può visualizzare tutti i processi locali e multiserver.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-list-information-for-all-jobs"></a>A. Visualizzazione di un elenco di informazioni per tutti i processi  
 Nell'esempio seguente la stored procedure `sp_help_job` viene eseguita senza parametri in modo da ottenere informazioni su tutti i processi definiti nel database `msdb`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-matching-a-specific-criteria"></a>B. Visualizzazione di un elenco di informazioni per i processi che corrispondono a un criterio specifico  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per i processi multiserver di cui è proprietario `françoisa` dove il processo è attivato e in fase di esecuzione.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job   
   @job_type = N'MULTI-SERVER',  
   @owner_login_name = N'françoisa',  
   @enabled = 1,  
   @execution_status = 1 ;  
GO  
```  
  
### <a name="c-listing-all-aspects-of-information-for-a-job"></a>C. Visualizzazione di un elenco di tutte le informazioni per un processo  
 Nell'esempio seguente viene visualizzato un elenco di tutti gli aspetti correlati alle informazioni per il processo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job  
    @job_name = N'NightlyBackups',  
    @job_aspect = N'ALL' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
