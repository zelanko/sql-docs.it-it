---
title: sysmail_delete_mailitems_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 23ecda5fd8d91f20133eb2295d38dc9d9ace66f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069097"
---
# <a name="sysmaildeletemailitemssp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina definitivamente messaggi di posta elettronica dalle tabelle interne di Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @sent_before = ] 'sent_before'` Elimina messaggi di posta elettronica anteriori alla data e ora specificate il *sent_before* argomento. *sent_before* viene **datetime** con valore predefinito è NULL. che indica tutte le date.  
  
`[ @sent_status = ] 'sent_status'` Elimina messaggi di posta elettronica del tipo specificato da *sent_status*. *sent_status* viene **varchar (8)** non prevede alcun valore predefinito. Possibili valori sono **inviato**, **unsent**, **ritentare**, e **non è stato possibile**. NULL indica tutti gli stati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 I messaggi di posta elettronica database e dei relativi allegati sono archiviati nel **msdb** database. I messaggi devono essere eliminati periodicamente per evitare **msdb** dall'aumento delle dimensioni maggiori del previsto e per assicurare la conformità con il programma di conservazione dei documenti di organizzazioni. Usare la **sysmail_delete_mailitems_sp** stored procedure per eliminare definitivamente messaggi di posta elettronica dalle tabelle di posta elettronica Database. Un argomento facoltativo consente di eliminare solo i messaggi di posta elettronica meno recenti tramite l'impostazione di una data e un'ora. I messaggi di posta elettronica con una data anteriore a quella specificata nell'argomento verranno eliminati. Un altro argomento facoltativo consente di eliminare solo i messaggi di posta elettronica di un determinato tipo, specificato come la **sent_status** argomento. È necessario fornire un argomento di tipo **@sent_before** oppure **@sent_status** . Per eliminare tutti i messaggi, usare  **@sent_before GETDATE () =** .  
  
 L'eliminazione di un messaggio di posta elettronica comporta la rimozione degli allegati correlati a tale messaggio, L'eliminazione di posta elettronica non elimina le voci corrispondenti nella **sysmail_event_log**. Uso [sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) eliminare elementi dal log.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure viene concessa per l'esecuzione di ai membri disattivare la **sysadmin** ruolo predefinito del server e **DatabaseMailUserRole**. I membri del **sysadmin** ruolo predefinito del server possono eseguire questa procedura per eliminare messaggi di posta elettronica inviati da tutti gli utenti. I membri del **DatabaseMailUserRole** possono eliminare solo i messaggi di posta elettronica inviati da tale utente.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-deleting-all-e-mails"></a>R. Eliminazione di tutti i messaggi di posta elettronica  
 Nell'esempio seguente vengono eliminati tutti i messaggi di posta elettronica nel sistema di Posta elettronica database.  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>B. Eliminazione dei messaggi di posta elettronica meno recenti  
 Nell'esempio seguente vengono eliminati i messaggi di posta elettronica nel log di Posta elettronica database con una data anteriore a `October 9, 2005`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>C. Eliminazione di tutti i messaggi di posta elettronica di un determinato tipo  
 Nell'esempio seguente vengono eliminati dal log di Posta elettronica database tutti i messaggi di posta elettronica che non è stato possibile inviare.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [Creare un processo di SQL Server Agent per l'archiviazione di messaggi e log eventi di Posta elettronica database](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
