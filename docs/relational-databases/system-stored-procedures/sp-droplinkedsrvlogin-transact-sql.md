---
title: sp_droplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: stevestein
ms.author: sstein
ms.openlocfilehash: ff6abaef6fc19a1bc646aab7ff30e4fcf6e13380
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097659"
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un mapping esistente tra un account di accesso nel server locale in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione e un account di accesso nel server collegato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @rmtsrvname = ] 'rmtsrvname'` È il nome di un server collegato che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene applicato il mapping di account di accesso. *rmtsrvname* viene **sysname**, non prevede alcun valore predefinito. *rmtsrvname* deve esistere già.  
  
`[ @locallogin = ] 'locallogin'` È il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso nel server locale che dispone di un mapping per il server collegato *rmtsrvname*. *locallogin* viene **sysname**, non prevede alcun valore predefinito. Un mapping per *locallogin* al *rmtsrvname* deve esistere già. Se NULL, il mapping predefinito creato tramite **sp_addlinkedserver**, che esegue il mapping di tutti gli account di accesso nel server locale per gli account di accesso nel server collegato, viene eliminato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Quando il mapping esistente per un account di accesso viene eliminato, utilizza il mapping predefinito creato dal server locale **sp_addlinkedserver** durante la connessione al server collegato per conto di tale account di accesso. Per modificare il mapping predefinito, usare **sp_addlinkedsrvlogin**.  
  
 Se viene eliminato anche il mapping predefinito, solo gli account di accesso in modo esplicito assegnato un mapping di account di accesso al server collegato, usando **sp_addlinkedsrvlogin**, può accedere al server collegato.  
  
 **la procedura sp_droplinkedsrvlogin** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY LOGIN nel server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>R. Rimozione del mapping di accesso per un utente esistente  
 Nell'esempio seguente viene rimosso il mapping per l'account di accesso `Mary` tra il server locale e il server collegato `Accounts`. L'account di accesso `Mary` utilizzerà pertanto il mapping predefinito degli account di accesso.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. Rimozione del mapping predefinito degli account di accesso  
 Nell'esempio seguente viene rimosso il mapping predefinito degli account di accesso creato tramite `sp_addlinkedserver` nel server locale `Accounts`.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
