---
title: sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9fa56614c65dfc14982c62fb71ce117f8872805c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62668279"
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la lingua predefinita di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'` È il nome di account di accesso. *account di accesso* viene **sysname**, non prevede alcun valore predefinito. *account di accesso* può essere un oggetto esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o un utente di Windows o un gruppo.  
  
`[ @language = ] 'language'` È la lingua predefinita dell'account di accesso. *linguaggio* viene **sysname**, con un valore predefinito è NULL. *linguaggio* deve essere una lingua valida nel server. Se *language* non viene specificato, *language* è impostato per la lingua predefinita del server lingua predefinita è definita dal **sp_configure** variabile di configurazione **lingua predefinita**. Se si modifica la lingua predefinita del server non viene modificata la lingua predefinita degli account di accesso esistenti.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_defaultlanguage** chiama ALTER LOGIN, che supporta opzioni aggiuntive. Per informazioni su come modificare altre impostazioni predefinite di account di accesso, vedere [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Per modificare la lingua della sessione corrente, eseguire l'istruzione SET LANGUAGE. Uso di @@LANGUAGE funzione per visualizzare l'impostazione della lingua corrente.  
  
 Se la lingua predefinita di un account di accesso viene eliminata dal server, l'account di accesso acquisisce la lingua predefinita del server. **sp_defaultlanguage** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
 Le informazioni sulle lingue installate nel server sono visibili nel **Sys. syslanguages** vista del catalogo.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'istruzione `ALTER LOGIN` viene utilizzata per modificare la lingua predefinita dell'account di accesso `Fathima` e impostarla sull'arabo. Questo è il metodo consigliato.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
