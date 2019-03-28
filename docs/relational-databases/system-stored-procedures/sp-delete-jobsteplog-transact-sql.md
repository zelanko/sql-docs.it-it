---
title: sp_delete_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3a3140c154f5d4eb224259001333747ce410e67
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533872"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove tutti i log dei passaggi di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent specificati con gli argomenti. Utilizzare questa stored procedure per gestire il **sysjobstepslogs** nella tabella di **msdb** database.  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] 'job_id'` ID del processo per il processo che contiene i log dei passaggi di processo da rimuovere. *job_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> **NOTA:** Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @step_id = ] step_id` Il numero di identificazione del passaggio del processo per cui è necessario eliminare i log dei passaggi di processo. Se omesso, vengono eliminati tutti i log dei passaggi di processo del processo, a meno che **@older_than** oppure **@larger_than** specificati. *step_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @step_name = ] 'step_name'` Il nome del passaggio del processo per cui è necessario eliminare i log dei passaggi di processo. *step_name* viene **sysname**, con un valore predefinito è NULL.  
  
> **NOTA:** Entrambi *step_id* oppure *step_name* può essere specificato, ma non è possibile specificarli entrambi.  
  
`[ @older_than = ] 'date'` Data e ora del log dei passaggi processo meno recente da conservare. Verranno rimossi tutti i log dei passaggi di processo antecedenti questa data e ora. *Data* viene **datetime**, con un valore predefinito è NULL. Entrambe **@older_than** e **@larger_than** può essere specificato.  
  
`[ @larger_than = ] 'size_in_bytes'` La dimensione in byte del log dei passaggi processo più grande si desidera mantenere. Vengono rimossi tutti i log dei passaggi di processo la cui dimensione è maggiore rispetto a quella indicata. Entrambe **@larger_than** e **@older_than** può essere specificato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **sp_delete_jobsteplog** è il **msdb** database.  
  
 Se nessun argomenti tranne **@job_id** oppure **@job_name** vengono specificati, vengono eliminati tutti i log dei passaggi di processo per il processo specificato.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** può eliminare un log dei passaggi di processo che appartiene a un altro utente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. Rimozione di tutti i log dei passaggi di processo da un processo  
 Nell'esempio seguente vengono rimossi tutti i log dei passaggi di processo del processo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. Rimozione del log dei passaggi di processo per un passaggio di processo specifico  
 Nell'esempio seguente viene rimosso il log relativo al passaggio 2 del processo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. Rimozione di tutti i log dei passaggi di processo in base alla data di creazione e alle dimensioni  
 Nell'esempio seguente tutti i log dei passaggi di processo antecedenti le ore 12.00 del 25 ottobre 2005 e di dimensioni maggiori di 100 MB vengono rimossi dal processo `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
