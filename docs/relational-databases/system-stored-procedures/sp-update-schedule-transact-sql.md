---
title: sp_update_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eeff4b38e3736241e0dd56729e42c5e7207f310f
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591805"
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le impostazioni per una pianificazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
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
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@schedule_id =** ] *schedule_id*  
 Identificatore della pianificazione da modificare. *schedule_id* viene **int**, non prevede alcun valore predefinito. Entrambi *schedule_id* oppure *schedule_name* deve essere specificato.  
  
 [  **@name =** ] **'**_schedule_name_**'**  
 Nome della pianificazione da modificare. *schedule_name*viene **sysname**, non prevede alcun valore predefinito. Entrambi *schedule_id* oppure *schedule_name* deve essere specificato.  
  
 [ **@new_name**= ] *new_name*  
 Nuovo nome della pianificazione. *new_name* viene **sysname**, con un valore predefinito è NULL. Quando *new_name* è NULL, il nome della pianificazione rimane invariato.  
  
 [  **@enabled =** ] *abilitata*  
 Indica lo stato corrente della pianificazione. *abilitata*viene **tinyint**, il valore predefinito è **1** (abilitato). Se **0**, la pianificazione non è abilitata. Quando la pianificazione non è abilitata, non viene eseguito alcun processo su questa pianificazione.  
  
 [ **@freq_type =** ] *freq_type*  
 Valore che indica la frequenza di esecuzione di un processo *freq_type*viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile, relativa a *freq intervallo*|  
|**64**|All'avvio del servizio SQLServerAgent|  
|**128**|Quando il computer è inattivo|  
  
 [  **@freq_interval =** ] *freq_interval*  
 Giorni in cui un processo viene eseguito. *freq_interval* viene **int**, il valore predefinito è **0**e dipende dal valore del *freq_type*.  
  
|Value of *freq_type*|Effetto su *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (una volta)|*freq_interval* risulta inutilizzato.|  
|**4** (giornaliera)|Ogni *freq_interval* giorni.|  
|**8** (settimanale)|*freq_interval* corrisponde a uno o più dei valori seguenti (combinati con un' **OR** operatore logico):<br /><br /> **1** = domenica<br /><br /> **2** = lunedì<br /><br /> **4** = martedì<br /><br /> **8** = mercoledì<br /><br /> **16** = giovedì<br /><br /> **32** = venerdì<br /><br /> **64** = sabato|  
|**16** (mensile)|Nel *freq_interval* giorno del mese.|  
|**32** (mensile relativo)|*freq_interval* è uno dei seguenti:<br /><br /> **1** = domenica<br /><br /> **2** = lunedì<br /><br /> **3** = martedì<br /><br /> **4** = mercoledì<br /><br /> **5** = giovedì<br /><br /> **6** = venerdì<br /><br /> **7** = sabato<br /><br /> **8** = giorno<br /><br /> **9** = giorno feriale<br /><br /> **10** = giorno festivo|  
|**64** (all'avvio del servizio SQLServerAgent)|*freq_interval* risulta inutilizzato.|  
|**128**|*freq_interval* risulta inutilizzato.|  
  
 [ **@freq_subday_type =** ] *freq_subday_type*  
 Specifica le unità per *freq_subday_interval * *.* *freq_subday_type*viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (unità)|  
|-----------|--------------------------|  
|**0x1**|All'ora specificata|  
|**0x2**|Secondi|  
|**0x4**|Minutes|  
|**0x8**|Ore|  
  
 [ **@freq_subday_interval =** ] *freq_subday_interval*  
 I numerosi *freq_subday_type* periodi intercorrere tra ogni esecuzione di un processo. *freq_subday_interval*viene **int**, il valore predefinito è **0**.  
  
 [  **@freq_relative_interval =** ] *freq_relative_interval*  
 Occorrenza di un processo di *freq_interval* ogni mese, se *freq_interval* viene **32** (frequenza mensile relativa). *freq_relative_interval*viene **int**, il valore predefinito è **0**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (unità)|  
|-----------|--------------------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
 [  **@freq_recurrence_factor =** ] *freq_recurrence_factor*  
 Numero di settimane o mesi tra le esecuzioni pianificate di un processo. *freq_recurrence_factor* viene usato solo se *freq_type* viene **8**, **16**, o **32**. *freq_recurrence_factor*viene **int**, il valore predefinito è **0**.  
  
 [ **@active_start_date =** ]  *active_start_date*  
 Data dalla quale è possibile avviare l'esecuzione del processo. *active_start_date*viene **int**, e il valore predefinito è NULL, che indica data odierna. La data è nel formato AAAAMMGG. Se *active_start_date* non è NULL, la data deve essere maggiore o uguale a 19900101.  
  
 Al termine della creazione della pianificazione, esaminare la data di inizio per verificare che corrisponda alla data corretta. Per altre informazioni, vedere la sezione "Pianificazione Start Date" nella [creare e collegare pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 [ **@active_end_date =** ] *active_end_date*  
 Data dalla quale è possibile arrestare l'esecuzione del processo. *active_end_date*viene **int**, il valore predefinito è **99991231**, che indica il 31 dicembre 9999. La data è nel formato AAAAMMGG.  
  
 [  **@active_start_time =** ] *active_start_time*  
 Il tempo compresa tra *active_start_date* e *active_end_date* per avviare l'esecuzione di un processo. *active_start_time*viene **int**, e il valore predefinito è 000000, che indica 12:00:00 A.M. nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
 [  **@active_end_time =** ] *active_end_time*  
 Il tempo compresa tra *active_start_date* e *active_end_date* per terminare l'esecuzione di un processo. *active_end_time*viene **int**, il valore predefinito è **235959**, a indicare 59: 11:59 P.M. nel formato a 24 ore e deve essere immesso nel formato HHMMSS.  
  
 [ **@owner_login_name**=] **'**_owner_login_name_**'**]  
 Nome dell'entità server proprietaria della pianificazione. *owner_login_name* viene **sysname**, con un valore predefinito è NULL, che indica che la pianificazione è di proprietà dell'autore.  
  
 [  **@automatic_post =**] *automatic_post*  
 Riservato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Tutti i processi che utilizzano la pianificazione, adottano immediatamente le nuove impostazioni. Cambiando la pianificazione, tuttavia, non vengono arrestati i processi attualmente in esecuzione.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** possono modificare una pianificazione di proprietà da un altro utente.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificato lo stato abilitato della pianificazione `NightlyJobs` impostandolo su `0` e impostando il proprietario su `terrid`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e collegare pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Pianificare un processo](../../ssms/agent/schedule-a-job.md)   
 [Creare una pianificazione](../../ssms/agent/create-a-schedule.md)   
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
