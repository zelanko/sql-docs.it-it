---
title: sp_stop_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eda439b53c72e41154d4891495470fc271028aee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004260"
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Richiede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent di arrestare l'esecuzione di un processo.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_name = ] 'job_name'` Il nome del processo da arrestare. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @job_id = ] job_id` Il numero di identificazione del processo da arrestare. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @originating_server = ] 'master_server'` Il nome del server master. Se specificato, vengono arrestati tutti i processi multiserver. *master_server* viene **nvarchar (128)**, con un valore predefinito è NULL. Specificare questo parametro solo quando si chiama **sp_stop_job** in un server di destinazione.  
  
> [!NOTE]  
>  È possibile specificare solo uno dei primi tre parametri.  
  
`[ @server_name = ] 'target_server'` Il nome del server di destinazione specifico in cui arrestare un processo multiserver. *target_server* viene **nvarchar (128)**, con un valore predefinito è NULL. Specificare questo parametro solo quando si chiama **sp_stop_job** in un server master per un processo multiserver.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **sp_stop_job** invia un segnale di arresto al database. Alcuni processi possono essere arrestate immediatamente e alcuni deve raggiungere un punto stabile (o un punto di ingresso per il percorso del codice) prima che questi possano smettere di. Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] con esecuzione prolungata, ad esempio BACKUP, RESTORE e alcuni comandi DBCC, possono richiedere un'elevata quantità di tempo per essere completate. Quando questi sono in esecuzione, potrebbe richiedere un po' di tempo prima che il processo viene annullato. L'arresto di un processo comporta la registrazione di una voce relativa all'annullamento nella cronologia processo.  
  
 Se un processo è in esecuzione un passaggio di tipo **CmdExec** oppure **PowerShell**, il processo in esecuzione (ad esempio, MyProgram.exe) deve essere terminato prematuramente. Tale interruzione può causare comportamenti imprevisti, ad esempio i file utilizzati dal processo potrebbero restare aperti. Di conseguenza **sp_stop_job** deve essere utilizzato solo in casi estremi, se il processo contiene passaggi di tipo **CmdExec** oppure **PowerShell**.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** e **SQLAgentReaderRole** possono arrestare solo i processi di cui sono proprietari. I membri del **SQLAgentOperatorRole** possono arrestare tutti i processi locali, inclusi quelli che sono proprietà di altri utenti. I membri del **sysadmin** possono arrestare tutti i processi locali e multiserver.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene arrestato un processo denominato `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
