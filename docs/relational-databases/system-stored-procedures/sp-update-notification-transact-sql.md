---
description: sp_update_notification (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32ddc8e2afae79b458d39f577d75176ba6f9dec1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473525"
---
# <a name="sp_update_notification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Aggiorna il metodo di notifica da adottare quando viene generato un avviso.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @alert_name = ] 'alert'` Nome dell'avviso associato alla notifica. *Alert* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @operator_name = ] 'operator'` Operatore che riceverà una notifica quando viene generato l'avviso. *operator* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @notification_method = ] notification` Metodo con cui l'operatore riceve una notifica. la *notifica*è di **tinyint**e non prevede alcun valore predefinito. i possibili valori sono i seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**1**|Posta elettronica|  
|**2**|Cercapersone|  
|**4**|**net send**|  
|**7**|Tutti i metodi|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_update_notification** deve essere eseguito dal database **msdb** .  
  
 È possibile aggiornare una notifica per un operatore che non ha le informazioni di indirizzo necessarie usando il *notification_method*specificato. Gli eventuali errori che si verificano durante l'invio di un messaggio di posta elettronica o di una notifica su cercapersone vengono registrati nel log degli errori di Microsoft SQL Server Agent.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire questa stored procedure, è necessario che agli utenti venga concesso il ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificato il metodo di notifica per le notifiche inviate a `François Ajenstat` per l'avviso `Test Alert` .  
  
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
 [sp_add_notification &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
