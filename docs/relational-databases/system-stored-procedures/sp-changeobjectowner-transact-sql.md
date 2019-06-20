---
title: sp_changeobjectowner (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8980ab1f968bcc842fdd17a6095a9945fcc26b42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62997074"
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica il proprietario di un oggetto del database corrente.  
  
> [!IMPORTANT]
>  Questa stored procedure funziona solo con gli oggetti disponibili in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) oppure [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) invece. **sp_changeobjectowner** modifica lo schema sia il proprietario. Per mantenere la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa stored procedure modifica i proprietari degli oggetti solo quando sia il proprietario corrente che il nuovo proprietario possiedono schemi il cui nome corrisponde al relativo nome utente di database.  
> 
> [!IMPORTANT]
>  A questa stored procedure è stato aggiunto un nuovo requisito di autorizzazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @objname = ] 'object'` È il nome di una tabella esistente, vista, funzione definita dall'utente o stored procedure nel database corrente. *oggetto* è un **nvarchar(776)** , non prevede alcun valore predefinito. *oggetto* può essere qualificato con il proprietario dell'oggetto esistente, nel formato _existing_owner_ **.** _oggetto_ se lo schema e il relativo proprietario hanno lo stesso nome.  
  
`[ @newowner = ] 'owner_ '` È il nome dell'account di protezione che sarà il nuovo proprietario dell'oggetto. *proprietario* viene **sysname**, non prevede alcun valore predefinito. *proprietario* deve essere un utente valido del database, ruolo del server [!INCLUDE[msCoName](../../includes/msconame-md.md)] account di accesso di Windows, o il gruppo di Windows con accesso al database corrente. Se il nuovo proprietario è un utente di Windows o un gruppo di Windows per cui non esiste un'entità corrispondente a livello di database, verrà creato un utente di database.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_changeobjectowner** rimuove tutte le autorizzazioni esistenti dall'oggetto. È necessario riapplicare le autorizzazioni che si desidera mantenere dopo l'esecuzione **sp_changeobjectowner**. È pertanto consigliabile includere le autorizzazioni esistenti prima dell'esecuzione **sp_changeobjectowner**. Dopo avere modificato il proprietario dell'oggetto, è possibile eseguire lo script per riapplicare le autorizzazioni. È prima necessario modificare il proprietario dell'oggetto nello script.  
  
 Per modificare il proprietario di un'entità a sicurezza diretta, utilizzare ALTER AUTHORIZATION. Per modificare uno schema, utilizzare ALTER SCHEMA.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_owner** fisse, o appartenenza al ruolo di database in entrambi i **db_ddladmin** ruolo predefinito del database e il **db_securityadmin** ruolo predefinito del database, e anche dell'autorizzazione CONTROL per l'oggetto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificato il proprietario della tabella `authors` in `Corporate\GeorgeW`.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
