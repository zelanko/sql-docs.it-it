---
title: sysmail_delete_log_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb2db3e60d416324a413bf9d6eb69f6125bc00b5
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588458"
---
# <a name="sysmaildeletelogsp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina eventi dal log di Posta elettronica database. È possibile eliminare tutti gli eventi nel log oppure solo quelli che soddisfano un particolare criterio relativo alla data o al tipo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@logged_before** =] **'**_logged_before_**'**  
 Elimina le voci anteriori alla data e ora specificate dal *logged_before* argomento. *logged_before* viene **datetime** con valore predefinito è NULL. che indica tutte le date.  
  
 [ **@event_type** =] **'**_event_type_**'**  
 Elimina le voci del tipo specificato come log di *event_type*. *event_type* viene **varchar(15)** non prevede alcun valore predefinito. Possibili valori sono **success**, **avviso**, **errore**, e **informativo**. NULL indica tutti i tipi di eventi.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Usare la **sysmail_delete_log_sp** stored procedure per eliminare definitivamente le voci dal log di posta elettronica Database. Un argomento facoltativo consente di eliminare solo i record meno recenti tramite l'impostazione di una data e un'ora. Gli eventi con una data anteriore a quella specificata nell'argomento verranno eliminati. Un argomento facoltativo consente di eliminare solo gli eventi di un determinato tipo, specificato come la **event_type** argomento.  
  
 L'eliminazione delle voci dal log di Posta elettronica database non comporta la rimozione dei messaggi di posta elettronica dalle tabelle di Posta elettronica database. Uso [sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) eliminare il messaggio di posta elettronica dalle tabelle di posta elettronica Database.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server può accedere a questa procedura.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-deleting-all-events"></a>A. Eliminazione di tutti gli eventi  
 Nell'esempio seguente vengono eliminati tutti gli eventi nel log di Posta elettronica database.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>b. Eliminazione degli eventi meno recenti  
 Nell'esempio seguente vengono eliminati gli eventi nel log di Posta elettronica database con una data anteriore al 9 ottobre 2005.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. Eliminazione di tutti gli eventi di un determinato tipo  
 Nell'esempio seguente vengono eliminati i messaggi di operazione riuscita nel log di Posta elettronica database.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [Creare un processo di SQL Server Agent per l'archiviazione di messaggi e log eventi di Posta elettronica database](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
