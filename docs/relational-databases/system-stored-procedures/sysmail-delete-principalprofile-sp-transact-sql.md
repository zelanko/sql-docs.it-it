---
title: sysmail_delete_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae63fabdca36e70daa6da28daa136a5dfcec8e1f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527783"
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove l'autorizzazione per un utente o ruolo del database per l'utilizzo di un profilo di Posta elettronica database pubblico o privato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @principal_id = ] principal_id` È l'ID dell'utente del database o del ruolo nel **msdb** database per l'associazione da eliminare. *principal_id* viene **int**, con un valore predefinito è NULL. Per rendere un profilo pubblico in profilo privato, fornire l'ID dell'entità **0** o il nome dell'entità **'public'**. Entrambi *principal_id* oppure *principal_name* deve essere specificato.  
  
`[ @principal_name = ] 'principal_name'` È il nome dell'utente del database o del ruolo nel **msdb** database per l'associazione da eliminare. *principal_name* viene **sysname**, con un valore predefinito è NULL. Per rendere un profilo pubblico in profilo privato, fornire l'ID dell'entità **0** o il nome dell'entità **'public'**. Entrambi *principal_id* oppure *principal_name* deve essere specificato.  
  
`[ @profile_id = ] profile_id` È l'ID del profilo per l'associazione da eliminare. *profile_id* viene **int**, con un valore predefinito è NULL. Entrambi *profile_id* oppure *profile_name* deve essere specificato.  
  
`[ @profile_name = ] 'profile_name'` È il nome del profilo per l'associazione da eliminare. *profile_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *profile_id* oppure *profile_name* deve essere specificato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Per trasformare un profilo pubblico in profilo privato, immettere **'public'** per il nome dell'entità oppure **0** per l'id dell'entità.  
  
 Prestare attenzione quando si rimuovono le autorizzazioni per il profilo privato predefinito di un utente o per il profilo pubblico predefinito. Quando non è disponibile alcun profilo predefinito **sp_send_dbmail** richiede il nome di un profilo come argomento. Rimozione di un profilo predefinito potrebbe pertanto provocare chiamate a **sp_send_dbmail** esito negativo. Per altre informazioni, vedere [sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).  
  
 La stored procedure **sysmail_delete_principalprofile_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente illustra l'eliminazione dell'associazione tra il profilo **AdventureWorks Administrator** e l'account di accesso **ApplicationUser** nel **msdb** database.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Oggetti di configurazione di posta elettronica database](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
