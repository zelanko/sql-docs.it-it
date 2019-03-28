---
title: sp_delete_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 194395728e60f31c689293191be2cedca4d549f3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528913"
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove il server specificato dall'elenco dei server di destinazione disponibili.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server_name = ] 'server'` Il nome del server da rimuovere come server di destinazione disponibile. *server* viene **nvarchar(30)**, non prevede alcun valore predefinito.  
  
`[ @clear_downloadlist = ] clear_downloadlist` Specifica se cancellare l'elenco di download per il server di destinazione. *clear_downloadlist* è di tipo **bit**, il valore predefinito è **1**. Quando *clear_downloadlist* viene **1**, la procedura cancella l'elenco di download per il server prima di eliminare il server. Quando *clear_downloadlist* viene **0**, l'elenco di download non viene cancellata.  
  
`[ @post_defection = ] post_defection` Specifica se inviare un'istruzione di esclusione al server di destinazione. *post_defection* è di tipo **bit**, con un valore predefinito è 1. Quando *post_defection* viene **1**, la procedura invia un'istruzione di esclusione al server di destinazione prima di eliminare il server. Quando *post_defection* viene **0**, la procedura non invia un'istruzione di esclusione al server di destinazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Normalmente per eliminare un server di destinazione consiste nel chiamare **sp_msx_defect** nel server di destinazione. Uso **sp_delete_targetserver** solo quando è necessaria un'esclusione in modo manuale.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa stored procedure, gli utenti devono disporre i **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il server `LONDON1` viene rimosso dall'elenco dei server di processo disponibili.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_help_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
