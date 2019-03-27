---
title: sp_altermessage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df2bab593e0e945e854e310a394abbc93f75efa4
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493123"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica lo stato dei messaggi di sistema o definiti dall'utente in un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Messaggi definiti dall'utente possono essere visualizzati utilizzando il **Sys. Messages** vista del catalogo.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@message_id =** ] *message_number*  
 È il numero di errore del messaggio da modificare dal **Sys. Messages**. *message_number* viene **int** non prevede alcun valore predefinito.  
  
`[ @parameter = ] 'write\_to\_log_'` Viene usato con **@parameter_value** a indicare che il messaggio deve essere scritto il [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows. *write_to_log* viene **sysname** non prevede alcun valore predefinito. *write_to_log* deve essere impostato su WITH_LOG o NULL. Se *write_to_log* è impostato su WITH_LOG o NULL e il valore per **@parameter_value** viene **true**, il messaggio viene scritto nel registro applicazioni di Windows. Se *write_to_log* è impostato su WITH_LOG o NULL e il valore di **@parameter_value** viene **false**, il messaggio viene scritto nel registro applicazioni di Windows, ma potrebbe essere scritta in base al modo in cui è stato generato l'errore. Se *write_to_log* è specificato, il valore per **@parameter_value** deve anche essere specificato.  
  
> [!NOTE]  
>  Se un messaggio viene scritto nel registro applicazioni di Windows, viene registrato inoltre nel file di log degli errori di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
`[ @parameter_value = ]'value_'` Viene usato con **@parameter** per indicare che l'errore è necessario scrivere il [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows. *valore* viene **varchar (5)**, non prevede alcun valore predefinito. Se **true**, l'errore viene sempre scritto nel registro applicazioni di Windows. Se **false**, l'errore viene scritto nel registro applicazioni di Windows, ma può essere scritta in base al modo in cui è stato generato l'errore. Se *valore* omette *write_to_log* per **@parameter** deve anche essere specificato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 L'effetto della **sp_altermessage** con il WITH_LOG è analogo a quello del parametro RAISERROR WITH LOG, con la differenza che opzione **sp_altermessage** cambia il comportamento della registrazione di un messaggio esistente. I messaggi modificati con l'opzione WITH_LOG vengono sempre scritti nel registro applicazioni di Windows, indipendentemente dalla modalità con cui sono stati generati. Gli errori vengono infatti scritti nel registro applicazioni di Windows anche se RAISERROR viene eseguito senza l'opzione WITH_LOG.  
  
 I messaggi di sistema possono essere modificati utilizzando **sp_altermessage**.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **serveradmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene registrato il messaggio `55001` esistente nel registro applicazioni di Windows.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
