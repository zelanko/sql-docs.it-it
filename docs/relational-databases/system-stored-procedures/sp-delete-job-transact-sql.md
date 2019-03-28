---
title: sp_delete_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b5ccd47f2b702c998a9e9268db523da1bfceaec
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536683"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un processo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` È il numero di identificazione del processo da eliminare. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` È il nome del processo da eliminare. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name*deve essere specificato; non è possibile specificarli entrambi.  
  
`[ @originating_server = ] 'server'` Per uso interno.  
  
`[ @delete_history = ] delete_history` Specifica se eliminare la cronologia per il processo. *delete_history* viene **bit**, il valore predefinito è **1**. Quando *delete_history* viene **1**, la cronologia processo per il processo viene eliminata. Quando *delete_history* viene **0**, non viene eliminata la cronologia processo.  
  
 Si noti che quando viene eliminato un processo e la cronologia non viene eliminata, le informazioni cronologiche per il processo non verranno visualizzati nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cronologia processo di interfaccia utente grafica dell'agente, ma le informazioni continueranno comunque a risiedere nel **sysjobhistory**nella tabella di **msdb** database.  
  
`[ @delete_unused_schedule = ] delete_unused_schedule` Specifica se eliminare le pianificazioni associate a questo processo se non sono associate a nessun altro processo. *delete_unused_schedule* viene **bit**, il valore predefinito è **1**. Quando *delete_unused_schedule* viene **1**, le pianificazioni associate a questo processo vengono eliminate se nessun altro processo fanno riferimento alla pianificazione. Quando *delete_unused_schedule* viene **0**, le pianificazioni non vengono eliminate.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Il **@originating_server** argomento è riservato per uso interno.  
  
 Il **@delete_unused_schedule** argomento assicura la compatibilità con le versioni precedenti di SQL Server eliminando automaticamente le pianificazioni che non sono associate ad alcun processo. Si noti che per impostazione predefinita questo parametro assume una funzionalità compatibile con le versioni precedenti. Per mantenere le pianificazioni che non sono associate a un processo, è necessario fornire il valore **0** come la **@delete_unused_schedule** argomento.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
 Questa stored procedure non può eliminare i piani di manutenzione né i processi facenti parti dei piani di manutenzione. Per eliminare i piani di manutenzione, utilizzare invece [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_delete_job** per l'eliminazione di qualsiasi processo. Se un utente non è un membro del ruolo predefinito del server **sysadmin** , può eliminare solo i processi di sua proprietà.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il processo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
