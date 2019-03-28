---
title: xp_grantlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c6a6e31b4dc36e0f280dfb03d8eadf09a7d4ff7c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534863"
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un gruppo a un utente di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'` È il nome dell'utente di Windows o del gruppo da aggiungere. L'utente di Windows o il gruppo deve essere qualificato con un nome di dominio Windows nel formato *Domain*\\*utente*. *account di accesso* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @logintype = ] 'logintype'` Il livello di sicurezza dell'account di accesso viene concesso l'accesso. *LoginType* viene **varchar (5)**, con un valore predefinito è NULL. Solo **admin** può essere specificato. Se **admin** è specificato, *login* viene concesso l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e aggiunti come membro del **sysadmin** ruolo predefinito del server.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **xp_grantlogin** è ora un sistema di stored procedure anziché una stored procedure estesa. **xp_grantlogin** chiamate **sp_grantlogin** e **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **securityadmin** ruolo predefinito del server. Quando si modifica il *logintype*, richiede l'appartenenza al **sysadmin** ruolo predefinito del server.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure estese generali &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
