---
title: sp_grantlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantlogin_TSQL
- sp_grantlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantlogin
ms.assetid: 0c873d99-c3bf-4eb1-948b-a46cb235ccd4
ms.author: vanto
manager: craigg
ms.openlocfilehash: def5041286ade754020a5c84e8d2ac91fc79afa3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535403"
---
# <a name="spgrantlogin-transact-sql"></a>sp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_grantlogin [@loginame=] 'login'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'` È il nome di un utente di Windows o un gruppo. L'utente di Windows o il gruppo deve essere qualificato con un nome di dominio Windows nel formato *Domain*\\*utente*, ad esempio **London\Joeb**. *account di accesso* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_grantlogin** chiama CREATE LOGIN, che supporta opzioni aggiuntive. Per informazioni sulla creazione di account di accesso di SQL Server, vedere [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **sp_grantlogin** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN nel server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `CREATE LOGIN` per creare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente di Windows `Corporate\BobJ.`. Questo è il metodo consigliato.  
  
```  
CREATE LOGIN [Corporate\BobJ] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
