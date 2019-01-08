---
title: sp_addremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e23684e04d8e49d1a6456185f94ad74b71b1604c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537923"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo ID di accesso remoto nel server locale. Ciò consente ai server remoti di connettersi ed eseguire chiamate di procedure remote.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilizzare i server collegati e le stored procedure per i server collegati in alternativa.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @remoteserver **=** ] **'**_remoteserver_**'**  
 Nome del server remoto a cui fa riferimento l'account di accesso remoto. *remoteserver* viene **sysname**, non prevede alcun valore predefinito. Se solo *remoteserver* è specificato, tutti gli utenti *remoteserver* vengono mappati a un account di accesso esistenti con lo stesso nome nel server locale. Il server deve essere noto al server locale. Viene aggiunto con sp_addserver. Quando gli utenti *remoteserver* connettersi al server locale in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire una stored procedure remota, si connettono come account di accesso locale corrispondente al proprio account di accesso in *remoteserver* . *remoteserver* è il server che avvia la chiamata di procedura remota.  
  
 [ @loginame **=** ] **'**_login_**'**  
 ID dell'account di accesso dell'utente nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* è di tipo **sysname** e il valore predefinito è NULL. *account di accesso*deve esistere già nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *account di accesso* è specificato, tutti gli utenti *remoteserver* viene eseguito il mapping a tale account di accesso locali specifici. Quando gli utenti *remoteserver* connettersi all'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire una stored procedure remota, si connettono come *login*.  
  
 [ @remotename **=** ] **'**_remote_name_**'**  
 ID dell'account di accesso dell'utente nel server remoto. *remote_name* viene **sysname**, con un valore predefinito è NULL. *remote_name* deve essere presente nel *remoteserver*. Se *remote_name* è specificato, l'utente specifico *remote_name* viene eseguito il mapping a *account di accesso* nel server locale. Quando *remote_name* sul *remoteserver* si connette all'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire una stored procedure remota, si connette come *login*. ID di accesso del *remote_name* può essere diverso dall'ID di accesso nel server remoto *login*.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Per eseguire query distribuite, utilizzare la procedura sp_addlinkedsrvlogin.  
  
 sp_addremotelogin non può essere utilizzata in una transazione definita dall'utente.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del sysadmin e securityadmin del server possono eseguire sp_addremotelogin.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-mapping-one-to-one"></a>A. Mapping uno-a-uno  
 Nell'esempio seguente viene eseguito il mapping dei nomi remoti ai nomi locali quando nel server remoto `ACCOUNTS` e in quello locale sono disponibili gli stessi account di accesso.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>b. Mapping molti-a-uno  
 Nell'esempio seguente viene creata una voce per mappare tutti gli utenti del server remoto `ACCOUNTS` all'ID di accesso locale `Albert`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. Utilizzo del mapping uno-a-uno esplicito  
 Nell'esempio seguente un account di accesso dell'utente remoto `Chris` nel server remoto `ACCOUNTS` viene mappato all'utente locale `salesmgr`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
