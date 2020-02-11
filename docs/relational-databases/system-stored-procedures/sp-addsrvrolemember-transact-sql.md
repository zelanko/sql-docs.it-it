---
title: sp_addsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c927bdff462922d1846188366fbb92ce0d3663c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022422"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un account di accesso come membro di un ruolo predefinito del server.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]In alternativa, utilizzare [ALTER Server Role](../../t-sql/statements/alter-server-role-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @loginame **=** ] **'**_login_**'**  
 Nome dell'account di accesso aggiunto al ruolo predefinito del server. *login* è di **tipo sysname**e non prevede alcun valore predefinito. *login* può essere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso di o un account di accesso di Windows. Gli account di Windows che non dispongono ancora dell'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ricevono automaticamente l'autorizzazione di accesso.  
  
 [ @rolename **=** ] **'**_Role_**'**  
 Nome del ruolo predefinito del server a cui verrà aggiunto l'account di accesso. *Role* è di **tipo sysname**e il valore predefinito è null. deve essere uno dei valori seguenti:  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 Se si aggiunge un account di accesso a un ruolo predefinito del server, tale account eredita le autorizzazioni associate al ruolo.  
  
 L'appartenenza ai ruoli dell'account di accesso sae del ruolo public non può essere modificata.  
  
 Utilizzare sp_addrolemember  per aggiungere un membro a un ruolo predefinito del database o definito dall'utente.  
  
 La stored procedure sp_addsrvrolemember non può essere eseguita in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo a cui viene aggiunto il nuovo membro.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'account di accesso di Windows `Corporate\HelenS` viene aggiunto al ruolo predefinito del server `sysadmin`.  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funzioni di sicurezza &#40;&#41;Transact-SQL](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREAZIONE del ruolo del SERVER &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
