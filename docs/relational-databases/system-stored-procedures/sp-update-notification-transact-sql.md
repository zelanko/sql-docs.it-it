---
title: sp_update_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cfa3aeda8e296cd1a85a0e8a098aaddac90954
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084858"
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna il metodo di notifica da adottare quando viene generato un avviso.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @alert_name = ] 'alert'` Il nome dell'avviso associato alla notifica. *avviso* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @operator_name = ] 'operator'` L'operatore che riceverà una notifica quando viene generato l'avviso. *operatore* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @notification_method = ] notification` Il metodo mediante il quale l'operatore riceve una notifica. *notifica*viene **tinyint**e non prevede alcun valore predefinito e può essere uno o più dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Posta elettronica|  
|**2**|Cercapersone|  
|**4**|**net send**|  
|**7**|Tutti i metodi|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_update_notification** deve essere eseguita la **msdb** database.  
  
 È possibile aggiornare una notifica per un operatore che non ha le informazioni necessarie sull'indirizzo utilizzando l'oggetto specificato *notification_method*. Gli eventuali errori che si verificano durante l'invio di un messaggio di posta elettronica o di una notifica su cercapersone vengono registrati nel log degli errori di Microsoft SQL Server Agent.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa stored procedure, gli utenti devono disporre i **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente modifica il metodo di notifica per notifiche inviate al `François Ajenstat`per l'avviso `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
