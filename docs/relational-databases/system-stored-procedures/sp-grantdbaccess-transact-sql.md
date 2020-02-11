---
title: sp_grantdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 3b88badb8b1852617d9edd8acd31f2c19258cca7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304870"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un utente del database al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]In alternativa, usare [Create User](../../t-sql/statements/create-user-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login_ '`Nome del gruppo di Windows, account di accesso di Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o account di accesso di cui eseguire il mapping al nuovo utente del database. I nomi dei gruppi di Windows e degli account di accesso di Windows devono essere qualificati con un nome di dominio Windows nel formato *Domain*\\*login*; ad esempio, **London\JoeB**. Sull'account di accesso non può essere già stato eseguito il mapping a un utente nel database. *login* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]``Nome del nuovo utente del database. *name_in_db* è una variabile di output con tipo di dati **sysname**e il valore predefinito è null. Se non è specificato, viene usato l' *account di accesso* . Se viene specificato come variabile di output con valore null, ** \@name_in_db** viene impostato su *login*. *name_in_db* non deve esistere già nel database corrente.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_grantdbaccess** chiama Create User, che supporta opzioni aggiuntive. Per informazioni sulla creazione di utenti del database, vedere [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md). Per rimuovere un utente del database da un database, usare [drop user](../../t-sql/statements/drop-user-transact-sql.md).  
  
 Impossibile eseguire **sp_grantdbaccess** in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del database **db_owner** o al ruolo predefinito del database **db_accessadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `CREATE USER` per aggiungere un utente del database per l'account di accesso di Windows `Edmonds\LolanSo` al database corrente. Il nuovo utente è denominato `Lolan`. Si tratta del metodo ottimale per la creazione di un utente del database.  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREAZIONE di un utente &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
