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
manager: craigg
ms.openlocfilehash: cb77f5d8bda6b05794499faa6e6e04d1fafa53ea
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534883"
---
# <a name="spgrantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un utente del database al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login_ '` È il nome del gruppo di Windows, account di accesso di Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso da associare al nuovo utente del database. I nomi dei gruppi di Windows e gli account di accesso di Windows devono essere qualificati con un nome di dominio Windows nel formato *Domain*\\*login*, ad esempio **LONDON\Joeb**. Sull'account di accesso non può essere già stato eseguito il mapping a un utente nel database. *account di accesso* è un **sysname**, non prevede alcun valore predefinito.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` È il nome per il nuovo utente del database. *name_in_db* è una variabile OUTPUT con un tipo di dati **sysname**e un valore predefinito è NULL. Se non specificato, *account di accesso* viene usato. Se specificato come variabile OUTPUT con un valore NULL, **@name_in_db** è impostata su *login*. *name_in_db* non deve esistere già nel database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_grantdbaccess** chiama CREATE USER, che supporta opzioni aggiuntive. Per informazioni sulla creazione di utenti del database, vedere [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md). Per rimuovere un utente del database da un database, usare [DROP USER](../../t-sql/statements/drop-user-transact-sql.md).  
  
 **sp_grantdbaccess** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_owner** ruolo predefinito del database o il **db_accessadmin** ruolo predefinito del database.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `CREATE USER` per aggiungere un utente del database per l'account di accesso di Windows `Edmonds\LolanSo` al database corrente. Il nuovo utente è denominato `Lolan`. Si tratta del metodo ottimale per la creazione di un utente del database.  
  
```  
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
