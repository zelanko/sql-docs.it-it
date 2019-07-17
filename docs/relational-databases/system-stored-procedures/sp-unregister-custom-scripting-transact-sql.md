---
title: sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe6bfe4c93ccabfaaec27739f7a1fd0e09348526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017905"
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure rimuove un'utente-stored procedure personalizzata definita oppure [!INCLUDE[tsql](../../includes/tsql-md.md)] file di script che è stata registrata eseguendo [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @type = ] 'type'` Si desidera rimuovere il tipo di stored procedure o script personalizzati. *tipo di* viene **varchar(16)** e non prevede alcun valore predefinito e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**insert**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione INSERT.|  
|**update**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione UPDATE.|  
|**delete**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione DELETE.|  
|**custom_script**|La stored procedure o lo script personalizzato registrato viene eseguito al termine del trigger DDL (Data Definition Language).|  
  
`[ @publication = ] 'publication'` Nome della pubblicazione per il quale viene rimossa la stored procedure o script personalizzati. *pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @article = ] 'article'` Nome dell'articolo per il quale viene rimossa la stored procedure o script personalizzati. *articolo* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_unregister_custom_scripting** viene utilizzata nella replica snapshot e transazionale.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database, o la **db_ddladmin** ruolo predefinito del database possono eseguire **sp _ unregister_custom_scripting**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
