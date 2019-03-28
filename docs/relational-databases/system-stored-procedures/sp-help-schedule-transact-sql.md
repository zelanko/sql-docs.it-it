---
title: sp_help_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fff543b074936f8bf1d69d841a1e81e402e9b0ae
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535433"
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di informazioni relative alle pianificazioni.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @schedule_id = ] id` L'identificatore della pianificazione all'elenco. *schedule_name* viene **int**, non prevede alcun valore predefinito. Entrambi *schedule_id* oppure *schedule_name* può essere specificato.  
  
`[ @schedule_name = ] 'schedule_name'` Il nome della pianificazione all'elenco. *schedule_name* viene **sysname**, non prevede alcun valore predefinito. Entrambi *schedule_id* oppure *schedule_name* può essere specificato.  
  
`[ @attached_schedules_only = ] attached_schedules_only ]` Specifica se visualizzare solo le pianificazioni di cui è associato un processo. *attached_schedules_only* viene **bit**, il valore predefinito è **0**. Quando *attached_schedules_only* viene **0**, vengono visualizzate tutte le pianificazioni. Quando *attached_schedules_only* viene **1**, il set di risultati contiene solo le pianificazioni associate a un processo.  
  
`[ @include_description = ] include_description` Specifica se includere le descrizioni nel set di risultati. *include_description* viene **bit**, il valore predefinito è **0**. Quando *include_description* viene **0**, il *schedule_description* colonna del set di risultati contiene un segnaposto. Quando *include_description* viene **1**, la descrizione della pianificazione è incluso nel set di risultati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Questa procedura restituisce il set di risultati seguente:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Numero di identificazione della pianificazione.|  
|**schedule_uid**|**uniqueidentifier**|Identificatore della pianificazione.|  
|**schedule_name**|**sysname**|Nome della pianificazione.|  
|**enabled**|**int**|Se la pianificazione è abilitato (**1**) o non abilitato (**0**).|  
|**freq_type**|**int**|Valore che indica la frequenza di esecuzione del processo:<br /><br /> **1** = Once<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa al **freq_interval**<br /><br /> **64** = esecuzione all'avvio del servizio SQLServerAgent.|  
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
|**schedule_description**|**nvarchar(4000)**|Descrizione in inglese della pianificazione, se richiesta.|  
|**job_count**|**int**|Restituisce il numero di processi che fanno riferimento a questa pianificazione.|  
  
## <a name="remarks"></a>Note  
 Quando viene specificato alcun parametro, **sp_help_schedule** Elenca le informazioni per tutte le pianificazioni nell'istanza.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** possono visualizzare solo le pianificazioni di cui sono proprietari.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. Visualizzazione di un elenco di informazioni per tutte le pianificazioni nell'istanza  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per tutte le pianificazioni nell'istanza.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. Visualizzazione di un elenco di informazioni per una pianificazione specifica  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per la pianificazione denominata `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
