---
title: sp_detach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: stevestein
ms.author: sstein
ms.openlocfilehash: aed989cc09922b7b480a7dd7b3ca6820d6b77ab2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936749"
---
# <a name="spdetachschedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un'associazione tra una pianificazione e un processo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` Numero di identificazione del processo da cui eliminare la pianificazione. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo da cui eliminare la pianificazione. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @schedule_id = ] schedule_id` Il numero di identificazione della pianificazione della pianificazione da eliminare dal processo. *schedule_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @schedule_name = ] 'schedule_name'` Il nome della pianificazione da eliminare dal processo. *schedule_name* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *schedule_id* oppure *schedule_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` Specifica se eliminare le pianificazioni dei processi. *delete_unused_schedule* viene **bit**, il valore predefinito è **0**, a indicare che verranno mantenute tutte le pianificazioni, anche se vi fa riferimento alcun processo. Se impostato su **1**, pianificazioni di processi non utilizzate vengono eliminate se vi fa riferimento alcun processo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Notare che il proprietario del processo può collegare un processo a una pianificazione e può scollegare un processo da una pianificazione senza dovere essere anche il proprietario della pianificazione. Tuttavia, non è possibile eliminare una pianificazione se lo scollegamento la lascia senza processi, a meno che il chiamante sia il proprietario della pianificazione.  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono eseguite verifiche per determinare se l'utente è proprietario della pianificazione. Solo i membri del **sysadmin** ruolo predefinito del server possono scollegare le pianificazioni da processi di proprietà da un altro utente.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene rimossa un'associazione tra una pianificazione `'NightlyJobs'` e un processo `'BackupDatabase'`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
