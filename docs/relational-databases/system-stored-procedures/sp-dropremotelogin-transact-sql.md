---
title: sp_dropremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
author: VanMSFT
manager: jroth
ms.openlocfilehash: 820ebc7e2bd79d0c321e327a2e5713151f3e24f3
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822474"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un account di accesso remoto di cui è stato eseguito il mapping a un account di accesso locale utilizzato per eseguire stored procedure remote nel server locale in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilizzare i server collegati e le stored procedure per i server collegati in alternativa.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @remoteserver = ] 'remoteserver'` È il nome del server remoto eseguito il mapping all'account di accesso remoto che deve essere rimossa. *remoteserver* viene **sysname**, non prevede alcun valore predefinito. *remoteserver* deve esistere già.  
  
`[ @loginame = ] 'login'` È il nome di account di accesso facoltativo nel server locale in cui è associato al server remoto. *login* è di tipo **sysname** e il valore predefinito è NULL. *account di accesso* deve già esistere se specificato.  
  
`[ @remotename = ] 'remote_name'` Nome facoltativo dell'account di accesso remoto viene mappato a *account di accesso* durante l'accesso dal server remoto. *remote_name* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Se solo *remoteserver* viene specificato, vengono rimossi tutti gli account di accesso remoto per il server remoto dal server locale. Se *account di accesso* è anche gli account di accesso specificato in tutte le modalità remota dal *remoteserver* mappate a questo specifico account di accesso locale vengono rimosse dal server locale. Se *remote_name* viene specificato anche, solo l'account di accesso remoto per l'utente remoto da *remoteserver* viene rimosso dal server locale.  
  
 Per aggiungere utenti al server locale, usare **sp_addlogin**. Per rimuovere utenti dal server locale, usare **sp_droplogin**.  
  
 Gli account di accesso remoti sono necessari solo in caso di utilizzo di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 e versioni successive utilizzano invece account di accesso dei server collegati. Uso **sp_addlinkedsrvlogin** e **sp_droplinkedsrvlogin** per aggiungere e rimuovere gli accessi server collegato.  
  
 **sp_dropremotelogin** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** oppure **securityadmin** ruoli predefiniti del server.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. Eliminazione di tutti gli account di accesso remoti per un server remoto  
 Nell'esempio seguente viene rimossa la voce relativa al server remoto `ACCOUNTS`, con la conseguente rimozione di tutti i mapping tra gli account di accesso nel server locale e gli account di accesso remoti nel server remoto.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. Eliminazione di un mapping tra account di accesso  
 Nell'esempio seguente viene rimossa la voce per il mapping degli account di accesso remoti tra il server remoto `ACCOUNTS` e l'account di accesso locale `Albert`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. Eliminazione di un utente remoto  
 Nell'esempio seguente viene rimosso l'account di accesso remoto `Chris` del server remoto `ACCOUNTS` sul quale è stato eseguito il mapping all'account di accesso locale `salesmgr`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
