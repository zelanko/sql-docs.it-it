---
title: sp_add_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16468053ee1e0d09b5be37c034800c122c1d16c9
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493289"
---
# <a name="spaddschedule-transact-sql"></a>sp_add_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una pianificazione che può essere utilizzata da un numero qualsiasi di processi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]  
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @schedule_name = ] 'schedule_name'` Il nome della pianificazione. *schedule_name* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @enabled = ] enabled` Indica lo stato corrente della pianificazione. *abilitata* viene **tinyint**, il valore predefinito è **1** (abilitato). Se **0**, la pianificazione non è abilitata. Quando la pianificazione non è abilitata, non viene eseguito alcun processo su questa pianificazione.  
  
`[ @freq_type = ] freq_type` Un valore che indica quando un processo deve essere eseguito. *freq_type* viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile, relativa a *freq_interval*|  
|**64**|All'avvio del servizio SQLServerAgent|  
|**128**|Quando il computer è inattivo|  
  
`[ @freq_interval = ] freq_interval` Giorni in cui viene eseguito un processo. *freq_interval* viene **int**, il valore predefinito è **1**e dipende dal valore del *freq_type*.  
  
|Value of *freq_type*|Effetto su *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (once)|*freq_interval* risulta inutilizzato.|  
|**4** (giornaliera)|Ogni *freq_interval* giorni.|  
|**8** (settimanale)|*freq_interval* corrisponde a uno o più dei valori seguenti (in combinazione con un operatore logico OR):<br /><br /> **1** = Sunday<br /><br /> **2** = lunedì<br /><br /> **4** = martedì<br /><br /> **8** = mercoledì<br /><br /> **16** = giovedì<br /><br /> **32** = venerdì<br /><br /> **64** = Saturday|  
|**16** (mensile)|Nel *freq_interval* giorno del mese.|  
|**32** (mensile relativo)|*freq_interval* è uno dei seguenti:<br /><br /> **1** = Sunday<br /><br /> **2** = lunedì<br /><br /> **3** = martedì<br /><br /> **4** = mercoledì<br /><br /> **5** = giovedì<br /><br /> **6** = Friday<br /><br /> **7** = sabato<br /><br /> **8** = giorno<br /><br /> **9** = giorno feriale<br /><br /> **10** = giorno festivo|  
|**64** (all'avvio del servizio SQLServerAgent)|*freq_interval* risulta inutilizzato.|  
|**128**|*freq_interval* risulta inutilizzato.|  
  
`[ @freq_subday_type = ] freq_subday_type` Specifica l'unità di misura *freq_subday_interval*. *freq_subday_type* viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (unità)|  
|-----------|--------------------------|  
|**0x1**|All'ora specificata|  
|**0x2**|Secondi|  
|**0x4**|Minutes|  
|**0x8**|Ore|  
  
`[ @freq_subday_interval = ] freq_subday_interval` I numerosi *freq_subday_type* periodi intercorrere tra ogni esecuzione di un processo. *freq_subday_interval* viene **int**, il valore predefinito è **0**. Nota: Intervallo deve essere più di 10 secondi. *freq_subday_interval* viene ignorato nei casi in cui *freq_subday_type* è uguale a **1**.  
  
`[ @freq_relative_interval = ] freq_relative_interval` Occorrenza di un processo di *freq_interval* ogni mese, se *freq_interval* è 32 (mensile relativa). *freq_relative_interval* viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti. *freq_relative_interval* viene ignorato nei casi in cui *freq_type* non è uguale a 32.  
  
|Value|Descrizione (unità)|  
|-----------|--------------------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` Il numero di settimane o mesi tra le esecuzioni pianificate di un processo. *freq_recurrence_factor* viene usato solo se *freq_type* viene **8**, **16**, o **32**. *freq_recurrence_factor* viene **int**, il valore predefinito è **0**.  
  
`[ @active_start_date = ] active_start_date` La data in cui è possibile avviare l'esecuzione di un processo. *active_start_date* viene **int**, e il valore predefinito è NULL, che indica data odierna. La data è nel formato AAAAMMGG. Se *active_start_date* non è NULL, la data deve essere maggiore o uguale a 19900101.  
  
 Al termine della creazione della pianificazione, esaminare la data di inizio per verificare che corrisponda alla data corretta. Per altre informazioni, vedere la sezione "Pianificazione Start Date" nella [creare e collegare pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 Per le pianificazioni settimanali o mensili, tramite Agent viene ignorato se la data di active_start_date è già passata e viene invece utilizzata la data corrente. Quando una pianificazione di SQL Agent viene creata utilizzando sp_add_schedule è possibile specificare il parametro active_start_date che rappresenta la data di avvio dell'esecuzione del processo. Se il tipo di pianificazione è settimanale o mensile e il parametro active_start_date è impostato su una data già trascorsa, il parametro active_start_date viene ignorato e la data corrente verrà utilizzata per active_start_date.  
  
`[ @active_end_date = ] active_end_date` La data in cui è possibile arrestare l'esecuzione di un processo. *active_end_date* viene **int**, il valore predefinito è **99991231**, che indica il 31 dicembre 9999. La data è nel formato AAAAMMGG.  
  
`[ @active_start_time = ] active_start_time` Il tempo compresa tra *active_start_date* e *active_end_date* per avviare l'esecuzione di un processo. *active_start_time* viene **int**, il valore predefinito è **000000**, a indicare 12:00:00 A.M. nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @active_end_time = ] active_end_time` Il tempo compresa tra *active_start_date* e *active_end_date* per terminare l'esecuzione di un processo. *active_end_time* viene **int**, il valore predefinito è **235959**, a indicare 59: 11:59 P.M. nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
`[ @owner_login_name = ] 'owner_login_name'` Il nome dell'entità server proprietaria della pianificazione. *owner_login_name* viene **sysname**, con un valore predefinito è NULL, che indica che la pianificazione è di proprietà dell'autore.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT` Identificatore univoco per la pianificazione. *valore schedule_uid* è una variabile di tipo **uniqueidentifier**.  
  
`[ @schedule_id = ] _schedule_idOUTPUT` Un identificatore per la pianificazione. *schedule_id* è una variabile di tipo **int**.  
  
`[ @originating_server = ] server_name` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-schedule"></a>A. Creazione di una pianificazione  
 Nell'esempio seguente viene creata una pianificazione denominata `RunOnce`. La pianificazione viene eseguita una volta, alle `23:30` del giorno in cui è stata creata.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>b. Creazione di una pianificazione e associazione della pianificazione a più processi  
 Nell'esempio seguente viene creata una pianificazione denominata `NightlyJobs`. I processi che utilizzano questa pianificazione vengono eseguiti ogni giorno quando l'ora indicata dal server è `01:00`. Nell'esempio la pianificazione viene collegata al processo `BackupDatabase` e al processo `RunReports`.  
  
> [!NOTE]  
>  In questo esempio si presuppone che il processo `BackupDatabase` e il processo `RunReports` esistano già.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e collegare pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Pianificare un processo](../../ssms/agent/schedule-a-job.md)   
 [Creare una pianificazione](../../ssms/agent/create-a-schedule.md)   
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
