---
title: sp_help_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36e00cf0e5d39722fee1c60fc86f0e6f81fd7e43
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100356"
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulla pianificazione dei processi utilizzati da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per l'esecuzione di attività automatizzate.  
 
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@job_id=** ] *job_id*  
 Numero di identificazione del processo. *job_id*viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
 [  **@job_name=** ] **'**_job_name_**'**  
 Nome del processo. *nome_processo*viene **sysname**, con un valore predefinito è NULL.  
  
> **NOTA:** Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
 [  **@schedule_name=** ] **'**_schedule_name_**'**  
 Nome dell'elemento di pianificazione per il processo. *schedule_name*viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@schedule_id=** ] *schedule_id*  
 Numero di identificazione dell'elemento di pianificazione per il processo. *schedule_id*viene **int**, con un valore predefinito è NULL.  
  
 [  **@include_description=** ] *include_description*  
 Specifica se includere la descrizione della pianificazione nel set dei risultati. *include_description* viene **bit**, il valore predefinito è **0**. Quando *include_description* viene **0**, la descrizione della pianificazione non è incluso nel set di risultati. Quando *include_description* viene **1**, la descrizione della pianificazione è incluso nel set di risultati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Numero di identificazione della pianificazione.|  
|**schedule_name**|**sysname**|Nome della pianificazione.|  
|**enabled**|**int**|Se la pianificazione è abilitato (**1**) o non abilitato (**0**).|  
|**freq_type**|**int**|Valore che indica la frequenza di esecuzione del processo:<br /><br /> **1** = una sola volta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa al **freq_interval**<br /><br /> **64** = vengono eseguite quando **SQLServerAgent** all'avvio del servizio.|  
|**freq_interval**|**int**|Giorni in cui viene eseguito il processo. Il valore dipende dal valore della **freq_type**. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Unità di misura per **freq_subday_interval**. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Numerosi **freq_subday_type** periodi intercorrere tra ogni esecuzione del processo. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|Pianificata del processo dei **freq_interval** ogni mese. Per altre informazioni, vedere [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Numero di mesi tra l'esecuzione pianificata del processo.|  
|**active_start_date**|**int**|Data di attivazione della pianificazione.|  
|**active_end_date**|**int**|Data di fine della pianificazione.|  
|**active_start_time**|**int**|Ora di inizio della pianificazione.|  
|**active_end_time**|**int**|Ora di fine della pianificazione.|  
|**date_created**|**datetime**|Data di creazione della pianificazione.|  
|**schedule_description**|**nvarchar(4000)**|Descrizione in inglese della pianificazione derivata dai valori **sysschedules**. Quando *include_description* viene **0**, questa colonna contiene testo indicante che la descrizione non è stato richiesto.|  
|**next_run_date**|**int**|Data della successiva esecuzione del processo in base alla pianificazione.|  
|**next_run_time**|**int**|Ora della successiva esecuzione del processo in base alla pianificazione.|  
|**schedule_uid**|**uniqueidentifier**|Identificatore della pianificazione.|  
|**job_count**|**int**|Numero di processi restituiti.|  
  
> **Nota: sp_help_jobschedule** restituisce valori dalle **dbo. sysjobschedules** e **dbo. sysschedules** tabelle di sistema **msdb**. **sysjobschedules** ogni 20 minuti. Ciò potrebbe influire sui valori restituiti dalla stored procedure.  
  
## <a name="remarks"></a>Note  
 I parametri del **sp_help_jobschedule** può essere usato solo in determinate combinazioni. Se *schedule_id* è specificato, né *job_id* né *job_name* può essere specificato. In caso contrario, il *job_id* oppure *job_name* parametri possono essere utilizzati con *schedule_name*.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** può visualizzare solo le proprietà delle pianificazioni dei processi che sono proprietari.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. Restituzione della pianificazione di un processo specifico  
 Nell'esempio seguente vengono restituite informazioni sulla pianificazione del processo `BackupDatabase`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>b. Restituzione della pianificazione di un processo per una pianificazione specifica  
 Nell'esempio seguente vengono restituite informazioni sulla pianificazione `NightlyJobs` e sul processo `RunReports`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. Restituzione della pianificazione di un processo e della descrizione della pianificazione per una pianificazione specifica  
 Nell'esempio seguente vengono restituite informazioni sulla pianificazione `NightlyJobs` e sul processo `RunReports`. Il set dei risultati restituiti include una descrizione della pianificazione.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
