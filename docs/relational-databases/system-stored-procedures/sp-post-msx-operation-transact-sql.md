---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 93e9c574346ad57a6947645552616cd8db46fe85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056376"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inserisce operazioni (righe) nella **sysdownloadlist** tabella di sistema per i server di destinazione scaricare ed eseguire.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @operation = ] 'operation'` Il tipo di operazione per l'operazione da richiedere. *operazione*viene **varchar(64)** , non prevede alcun valore predefinito. Operazioni valide dipendono *object_type*.  
  
|Tipo oggetto|Operazione|  
|-----------------|---------------|  
|**JOB**|INSERT<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**SERVER**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**PIANIFICAZIONE**|INSERT<br /><br /> UPDATE<br /><br /> DELETE|  
  
`[ @object_type = ] 'object'` Il tipo di oggetto per cui si desidera richiedere un'operazione. I tipi validi sono **processo**, **SERVER**, e **pianificazione**. *oggetto* viene **varchar(64)** , il valore predefinito è **processo**.  
  
`[ @job_id = ] job_id` Il numero di identificazione del processo a cui viene applicata l'operazione. *job_id* viene **uniqueidentifier**, non prevede alcun valore predefinito. **0x00** indica tutti i processi. Se *oggetti* viene **SERVER**, quindi *job_id*non è obbligatorio.  
  
`[ @specific_target_server = ] 'target_server'` Il nome del server di destinazione per il quale si applica l'operazione specificata. Se *job_id* è specificato, ma *target_server* viene omesso, le operazioni vengono richieste per tutti i server del processo del processo. *target_server* viene **nvarchar(30)** , con un valore predefinito è NULL.  
  
`[ @value = ] value` L'intervallo di polling in secondi. *value* è **int**e il valore predefinito è NULL. Specificare questo parametro solo se *operazione* viene **SET-POLL**.  
  
`[ @schedule_uid = ] schedule_uid` Identificatore univoco per la pianificazione a cui si applica l'operazione. *valore schedule_uid* viene **uniqueidentifier**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **SP_POST_MSX_OPERATION** deve essere eseguita la **msdb** database.  
  
 **SP_POST_MSX_OPERATION** può sempre essere chiamato in modo sicuro perché determina innanzitutto se il server corrente è un agente multiserver di Microsoft SQL Server e, in questo caso, se *oggetto*è un processo multiserver.  
  
 Dopo un'operazione è stata registrata, viene visualizzato nei **sysdownloadlist** tabella. Dopo la creazione e l'inserimento di un processo, è necessario comunicare ai server di destinazione (TSX) tutte le successive modifiche apportate al processo. A tale scopo è possibile utilizzare l'elenco di download.  
  
 È consigliabile gestire l'elenco di download in SQL Server Management Studio. Per altre informazioni, vedere [visualizzare o modificare processi](../../ssms/agent/view-or-modify-jobs.md).  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa stored procedure, gli utenti devono disporre i **sysadmin** ruolo predefinito del server.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
