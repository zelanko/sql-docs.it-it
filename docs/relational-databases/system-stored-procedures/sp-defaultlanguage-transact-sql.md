---
title: sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: af2402ce4f1e49ee572a9d271497c2798d679070
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68120088"
---
# <a name="sp_defaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la lingua predefinita di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]In alternativa, usare [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'`Nome dell'account di accesso. *login* è di **tipo sysname**e non prevede alcun valore predefinito. l' *account di accesso* può [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] essere un account di accesso esistente o un utente o un gruppo di Windows.  
  
`[ @language = ] 'language'`Lingua predefinita dell'account di accesso. *Language* è di **tipo sysname**e il valore predefinito è null. la *lingua* deve essere una lingua valida nel server. Se la *lingua* non è specificata *, il linguaggio viene* impostato sulla lingua predefinita del server. la lingua predefinita è definita dalla variabile di configurazione **sp_configure** **lingua predefinita**. Se si modifica la lingua predefinita del server non viene modificata la lingua predefinita degli account di accesso esistenti.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_defaultlanguage** chiama ALTER LOGIN, che supporta opzioni aggiuntive. Per informazioni sulla modifica delle impostazioni predefinite degli account di accesso, vedere [ALTER login &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Per modificare la lingua della sessione corrente, eseguire l'istruzione SET LANGUAGE. Utilizzare la funzione@LANGUAGE @ per visualizzare l'impostazione della lingua corrente.  
  
 Se la lingua predefinita di un account di accesso viene eliminata dal server, l'account di accesso acquisisce la lingua predefinita del server. Impossibile eseguire **sp_defaultlanguage** in una transazione definita dall'utente.  
  
 Le informazioni sulle lingue installate nel server sono visibili nella vista del catalogo **sys. syslanguages** .  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione ALTER ANY LOGIN.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'istruzione `ALTER LOGIN` viene utilizzata per modificare la lingua predefinita dell'account di accesso `Fathima` e impostarla sull'arabo. Questo è il metodo preferito.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys. syslanguages &#40;&#41;Transact-SQL](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
