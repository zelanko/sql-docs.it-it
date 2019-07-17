---
title: sp_addrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1711ec3941a5fced5ef9e0c32808d6153b673e2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030924"
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuovo ruolo di database nel database corrente.  
  
> [!IMPORTANT]
>  **sp_addrole** è inclusa per compatibilità con le versioni precedenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e potrebbero non essere supportate nelle versioni future. Uso [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @rolename = ] 'role'` È il nome del nuovo ruolo del database. *ruolo* è un **sysname**, non prevede alcun valore predefinito. *ruolo* deve essere un identificatore (ID) valido e non deve esistere già nel database corrente.  
  
`[ @ownername = ] 'owner'` È il proprietario del nuovo ruolo del database. *proprietario* è un **sysname**, con un valore predefinito dell'utente corrente in esecuzione. *proprietario* deve essere un utente del database o ruolo del database nel database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 I nomi dei ruoli di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono includere da 1 a 128 caratteri. Sono consentiti simboli, numeri e lettere. I nomi dei ruoli predefiniti del database non possono: contenere un carattere di barra rovesciata (\\), essere NULL o una stringa vuota ( **'** ).  
  
 Dopo aver aggiunto un ruolo del database, utilizzare [sp_addrolemember &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) per aggiungere entità al ruolo. Quando si utilizza l'istruzione GRANT, DENY o REVOKE per applicare autorizzazioni al ruolo, i membri corrispondenti ereditano tali autorizzazioni come se fossero state assegnate direttamente ai relativi account.  
  
> [!NOTE]  
>  Non è possibile creare nuovi ruoli di server. I ruoli possono essere creati solo a livello di database.  
  
 **sp_addrole** non può essere utilizzata in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CREATE ROLE per il database. Per la creazione di uno schema, è richiesta l'autorizzazione CREATE SCHEMA per il database. Se *proprietario* è specificato come un utente o gruppo, è richiesta l'autorizzazione IMPERSONATE in tale utente o gruppo. Se *proprietario* è specificato come un ruolo, richiede l'autorizzazione ALTER per tale ruolo o in un membro di tale ruolo. Se owner è specificato come ruolo di applicazione, è richiesta l'autorizzazione ALTER per quel ruolo di applicazione.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene aggiunto un nuovo ruolo `Managers` al database corrente.  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
