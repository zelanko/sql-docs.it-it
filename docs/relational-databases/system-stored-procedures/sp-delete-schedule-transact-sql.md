---
title: sp_delete_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ec2fe4ba5ad90d044a9407be04acc850ae16b73
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591495"
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina una pianificazione.  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@schedule_id=** ] *schedule_id*  
 Numero di identificazione della pianificazione che si desidera eliminare. *schedule_id* viene **int**, con un valore predefinito è NULL.  
  
> **NOTA:** Entrambi *schedule_id* oppure *schedule_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
 [  **@schedule_name=** ] **'**_schedule_name_**'**  
 Nome della pianificazione che si desidera eliminare. *schedule_name* viene **sysname**, con un valore predefinito è NULL.  
  
> **NOTA:** Entrambi *schedule_id* oppure *schedule_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
 [ **@force_delete** =] *force_delete*  
 Specifica se la stored procedure avrà esito negativo se la pianificazione è associata a un processo. *Force_delete* è di tipo bit e il valore predefinito **0**. Quando *force_delete* viene **0**, la stored procedure ha esito negativo se la pianificazione è associata a un processo. Quando *force_delete* viene **1**, la pianificazione verrà eliminata indipendentemente dal fatto che la pianificazione è associata a un processo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Per impostazione predefinita, una pianificazione non può essere eliminata se è associata a un processo. Per eliminare una pianificazione collegata a un processo, specificare il valore **1** per *force_delete*. L'eliminazione di una pianificazione non comporta l'arresto dei processi in esecuzione.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Notare che il proprietario del processo può collegare un processo a una pianificazione e può scollegare un processo da una pianificazione senza dovere essere anche il proprietario della pianificazione. Tuttavia, non è possibile eliminare una pianificazione se lo scollegamento la lascia senza processi, a meno che il chiamante sia il proprietario della pianificazione.  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** ruolo può eliminare una pianificazione del processo che appartiene a un altro utente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-deleting-a-schedule"></a>A. Eliminazione di una pianificazione  
 Nell'esempio seguente viene eliminata la pianificazione `NightlyJobs`. Se è associata a un processo qualsiasi, la pianificazione non verrà eliminata.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>b. Eliminazione di una pianificazione associata a un processo  
 Nell'esempio seguente viene eliminata la pianificazione `RunOnce` anche se è associata a un processo.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di processi](../../ssms/agent/implement-jobs.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
