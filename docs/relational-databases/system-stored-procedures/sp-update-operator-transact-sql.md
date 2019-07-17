---
title: sp_update_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a766ad74f42336612859c63cf42df654846ff96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084846"
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna le informazioni relative a un operatore (destinatario di notifiche) utilizzate in avvisi e processi.  
  
   ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @name=] '*nome*'  
 Nome dell'operatore da modificare. *nome* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ @new_name=] '*new_name*'  
 Nuovo nome dell'operatore. Il nome deve essere univoco. *new_name* viene **sysname**, con un valore predefinito è NULL.  
  
 [ @enabled=] *abilitata*  
 Numero che indica lo stato corrente dell'operatore (**1** se attualmente abilitato **0** in caso contrario). *abilitata* viene **tinyint**, con un valore predefinito è NULL. Gli operatori non abilitati non ricevono le notifiche di avviso.  
  
 [ @email_address=] '*email_address*'  
 Indirizzo di posta elettronica dell'operatore. Questa stringa viene passata direttamente al sistema di posta elettronica. *email_address* viene **nvarchar(100)** , con un valore predefinito è NULL.  
  
 [ @pager_address=] '*pager_number*'  
 Indirizzo del cercapersone dell'operatore. Questa stringa viene passata direttamente al sistema di posta elettronica. *pager_number* viene **nvarchar(100)** , con un valore predefinito è NULL.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 Indica l'ora dei giorni lavorativi da lunedì a venerdì oltre la quale è possibile inviare una notifica al cercapersone dell'operatore specificato. *weekday_pager_start_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 Indica l'ora dei giorni lavorativi da lunedì a venerdì oltre la quale non è possibile inviare una notifica al cercapersone dell'operatore specificato. *weekday_pager_end_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 Indica l'ora del sabato oltre la quale è possibile inviare una notifica sul cercapersone dell'operatore specificato. *saturday_pager_start_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 Indica l'ora del sabato oltre la quale non è possibile inviare una notifica sul cercapersone dell'operatore specificato. *saturday_pager_end_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 Indica l'ora della domenica oltre la quale è possibile inviare una notifica sul cercapersone dell'operatore specificato. *sunday_pager_start_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 Indica l'ora della domenica oltre la quale non è possibile inviare una notifica sul cercapersone dell'operatore specificato. *sunday_pager_end_time*viene **int**, con un valore predefinito è NULL e deve essere immesso nel formato HHMMSS per l'uso con un orologio di 24 ore.  
  
 [ @pager_days=] *pager_days*  
 Indica i giorni in cui l'operatore può essere rintracciato tramite cercapersone (in base all'ora di inizio e fine specificata). *pager_days*viene **tinyint**, con un valore predefinito è NULL e deve essere un valore compreso **0** tramite **127**. *pager_days* viene calcolato sommando i singoli valori dei giorni necessari. Ad esempio, da lunedì a venerdì viene **2**+**4**+**8**+**16** + **32** = **64**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Domenica|  
|**2**|Lunedì|  
|**4**|Martedì|  
|**8**|Mercoledì|  
|**16**|Giovedì|  
|**32**|Venerdì|  
|**64**|Sabato|  
  
 [ @netsend_address=] '*netsend_address*'  
 Indirizzo di rete dell'operatore a cui viene inviato il messaggio di rete. *netsend_address*viene **nvarchar(100)** , con un valore predefinito è NULL.  
  
 [ @category_name=] '*categoria*'  
 Nome della categoria di questo avviso. *categoria* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 La stored procedure sp_update_operator deve essere eseguita nel database msdb.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione per questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server sysadmin.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente lo stato dell'operatore viene impostato su abilitato. Vengono inoltre impostati i giorni in cui è possibile contattare l'operatore sul cercapersone, ovvero da lunedì a venerdì, dalle 8 alle 17.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
