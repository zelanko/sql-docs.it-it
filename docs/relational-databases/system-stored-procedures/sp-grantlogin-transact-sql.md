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
author: VanMSFT
ms.openlocfilehash: 3f605d17348c651ef0fbc58ebd52b422bdba1896
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728190"
---
# <a name="sp_grantlogin-transact-sql"></a>sp_grantlogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Crea un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]In alternativa, usare [Create Login](../../t-sql/statements/create-login-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_grantlogin [@loginame=] 'login'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'`Nome di un utente o di un gruppo di Windows. L'utente o il gruppo di Windows deve essere qualificato con un nome di dominio Windows *Domain*nel formato \\ *utente*dominio, ad esempio **London\JoeB**. *login* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_grantlogin** chiama Create login, che supporta opzioni aggiuntive. Per informazioni sulla creazione di account di accesso SQL Server, vedere [create login &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 Impossibile eseguire **sp_grantlogin** in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione ALTER ANY LOGIN nel server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `CREATE LOGIN` per creare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'utente di Windows `Corporate\BobJ.`. Questo è il metodo consigliato.  
  
```sql
CREATE LOGIN [Corporate\BobJ] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Crea account di accesso &#40;&#41;Transact-SQL](../../t-sql/statements/create-login-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
