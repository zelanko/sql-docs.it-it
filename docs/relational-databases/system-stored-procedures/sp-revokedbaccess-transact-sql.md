---
title: sp_revokedbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 41d2c1aa64bc3d7913cadbb5e54e9895af55e554
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750485"
---
# <a name="sp_revokedbaccess-transact-sql"></a>sp_revokedbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Rimuove un utente di database dal database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]In alternativa, usare [drop user](../../t-sql/statements/drop-user-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name_in_db = ] 'name'`Nome dell'utente del database da rimuovere. *Name* è di **tipo sysname** e non prevede alcun valore predefinito. *Name* può essere il nome di un account di accesso del server, di un account di accesso di Windows o di un gruppo di Windows e deve esistere nel database corrente. Se si specifica un account di accesso o un gruppo di Windows, specificare il nome con cui è noto nel database.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 Quando si rimuove l'utente di database, vengono rimossi anche le autorizzazioni e gli alias che dipendono dall'utente.  
  
 **sp_revokedbaccess** possibile rimuovere solo gli utenti del database dal database corrente. Prima di rimuovere un utente di database proprietario di oggetti nel database corrente è necessario trasferire la proprietà degli oggetti o rimuoverli dal database. Per altre informazioni, vedere [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Impossibile eseguire **sp_revokedbaccess** in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione ALTER ANY USER per il database.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'utente di database sul quale è stato eseguito il mapping a `Edmonds\LolanSo` viene rimosso dal database corrente.  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
