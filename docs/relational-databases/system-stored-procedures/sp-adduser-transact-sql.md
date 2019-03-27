---
title: sp_adduser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 46b1548f1eb587aa62c0d0427661d97d97bf3cc7
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492939"
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo utente al database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @loginame = ] 'login'` È il nome del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o Windows. *account di accesso* è un **sysname**, non prevede alcun valore predefinito. *account di accesso* deve essere un oggetto esistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o Windows.  
  
`[ @name_in_db = ] 'user'` È il nome per il nuovo utente del database. *utente* è un **sysname**, con un valore predefinito è NULL. Se *utente* non viene specificato, per impostazione predefinita il nome del nuovo utente del database di *login* nome. Che specifica *utente* assegna a un nome al nuovo utente del database diverso dal nome dell'account di accesso a livello di server.  
  
`[ @grpname = ] 'role'` È il ruolo del database di cui il nuovo utente diventa membro. *ruolo* viene **sysname**, con un valore predefinito è NULL. *ruolo* deve essere un ruolo di database valido nel database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_adduser** creerà inoltre uno schema con il nome dell'utente.  
  
 Dopo avere aggiunto un utente, utilizzare le istruzioni GRANT, DENY e REVOKE per definire le autorizzazioni per controllare le attività che l'utente può svolgere.  
  
 Uso **Sys. server_principals** per visualizzare un elenco di nomi di account di accesso valido.  
  
 Uso **sp_helprole** per visualizzare un elenco di nomi di ruolo validi. Se si specifica un ruolo, l'utente ottiene automaticamente le autorizzazioni definite per tale ruolo. Se non viene specificato un ruolo, l'utente ha le autorizzazioni concesse per impostazione predefinita **pubblica** ruolo. Per aggiungere un utente a un ruolo, un valore per il *nome utente* devono essere specificati. (*nomeutente* può essere identico *login_id*.)  
  
 Utente **guest** già esiste in ogni database. Aggiunta dell'utente **guest** abiliterà questo utente, se è stata precedentemente disabilitata. Per impostazione predefinita, utente **guest** è disabilitato nei nuovi database.  
  
 **sp_adduser** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
 Non è possibile aggiungere un **guest** utente perché un **guest** utente esiste già all'interno di ogni database. Per abilitare la **guest** utente, concedere **guest** dell'autorizzazione CONNECT come illustrato:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 È necessario essere il proprietario del database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-adding-a-database-user"></a>A. Aggiunta di un utente del database  
 Nell'esempio seguente l'utente del database `Vidur` viene aggiunto al ruolo esistente `Recruiting` nel database corrente utilizzando l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistente `Vidur`.  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>b. Aggiunta di un utente del database con lo stesso ID di accesso  
 Nell'esempio seguente l'utente `Arvind` viene aggiunto al database corrente per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Arvind`. L'utente a cui appartiene il valore predefinito **pubblica** ruolo.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Aggiunta di un utente del database con un nome diverso dall'account di accesso a livello di server  
 Nell'esempio seguente l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `BjornR` viene aggiunto al database corrente che include il nome utente `Bjorn`, quindi l'utente del database `Bjorn` viene aggiunto al ruolo del database `Production`.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
