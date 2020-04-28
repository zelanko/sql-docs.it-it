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
ms.openlocfilehash: 9a0549d247078634feadced301570e00746d5ba7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032718"
---
# <a name="sp_stop_job-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Richiede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent di arrestare l'esecuzione di un processo.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_name = ] 'job_name'`Nome del processo da arrestare. *job_name* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @job_id = ] job_id`Numero di identificazione del processo da arrestare. *job_id* è di tipo **uniqueidentifier**e il valore predefinito è null.  
  
`[ @originating_server = ] 'master_server'`Nome del server master. Se specificato, vengono arrestati tutti i processi multiserver. *master_server* è di **tipo nvarchar (128)** e il valore predefinito è null. Specificare questo parametro solo quando si chiama **sp_stop_job** in un server di destinazione.  
  
> [!NOTE]  
>  È possibile specificare solo uno dei primi tre parametri.  
  
`[ @server_name = ] 'target_server'`Nome del server di destinazione specifico in cui arrestare un processo multiserver. *target_server* è di **tipo nvarchar (128)** e il valore predefinito è null. Specificare questo parametro solo quando si chiama **sp_stop_job** in un server master per un processo multiserver.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 **sp_stop_job** Invia un segnale di arresto al database. Alcuni processi possono essere interrotti immediatamente e alcuni devono raggiungere un punto stabile (o un punto di ingresso al percorso del codice) prima di potersi arrestare. Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] con esecuzione prolungata, ad esempio BACKUP, RESTORE e alcuni comandi DBCC, possono richiedere un'elevata quantità di tempo per essere completate. Quando sono in esecuzione, l'operazione potrebbe richiedere alcuni minuti prima che il processo venga annullato. L'arresto di un processo comporta la registrazione di una voce relativa all'annullamento nella cronologia processo.  
  
 Se un processo è attualmente in esecuzione un passaggio di tipo **CmdExec** o **PowerShell**, il processo in esecuzione (ad esempio, programma. exe) viene forzato a terminare in modo anomalo. Tale interruzione può causare comportamenti imprevisti, ad esempio i file utilizzati dal processo potrebbero restare aperti. Di conseguenza, **sp_stop_job** deve essere usato solo in casi estremi se il processo contiene passaggi di tipo **CmdExec** o **PowerShell**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri di **SQLAgentUserRole** e **SQLAgentReaderRole** possono arrestare solo i processi di cui sono proprietari. I membri di **SQLAgentOperatorRole** possono arrestare tutti i processi locali, inclusi quelli di proprietà di altri utenti. I membri di **sysadmin** possono arrestare tutti i processi locali e multiserver.  
  
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
 [sp_delete_job &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
