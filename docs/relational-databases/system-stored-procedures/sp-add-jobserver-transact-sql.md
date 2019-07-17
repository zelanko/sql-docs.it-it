---
title: sp_add_jobserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobserver
- sp_add_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobserver
ms.assetid: 485252cc-0081-490a-9bd1-cbbd68eea286
author: stevestein
ms.author: sstein
ms.openlocfilehash: fecd704d5f6b6f0384ecb17787bd8423852356ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078200"
---
# <a name="spaddjobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indirizza il processo specificato al server specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` Il numero di identificazione del processo. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @server_name = ] 'server'` Il nome del server a cui indirizzare il processo. *server* viene **nvarchar(30)** , con un valore predefinito di N' (Local) '. *server* può essere rappresentata **(locale)** per un server locale o il nome di un server di destinazione esistente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **@automatic_post** esiste **sp_add_jobserver**, ma non è elencato nella sezione argomenti. **@automatic_post** è riservato per uso interno.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_add_jobserver** per processi che implicano più server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-assigning-a-job-to-the-local-server"></a>R. Assegnazione di un processo al server locale  
 Nell'esempio seguente viene assegnato il processo `NightlyBackups` da eseguire nel server locale.  
  
> [!NOTE]  
>  In questo esempio si presuppone che il processo `NightlyBackups` esista già.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-assigning-a-job-to-run-on-a-different-server"></a>B. Assegnazione di un processo da eseguire su un server diverso  
 Nell'esempio seguente il processo multiserver `Weekly Sales Backups` viene assegnato al server `SEATTLE2`.  
  
> [!NOTE]  
>  In questo esempio si presuppone che il processo `Weekly Sales Backups` esista già e che `SEATTLE2` sia registrato come server di destinazione per l'istanza corrente.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
