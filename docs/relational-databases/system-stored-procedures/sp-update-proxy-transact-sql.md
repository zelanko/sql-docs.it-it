---
title: sp_update_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29a95b506fbbfb5342410d8d393f0091dd98834b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534463"
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le proprietà di un proxy già esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id` Il numero di identificazione del proxy da modificare. Il *proxy_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy da modificare. Il *nome_proxy* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @credential_name = ] 'credential_name'` Il nome delle nuove credenziali per il proxy. Il *credential_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *credential_name* oppure *credential_id* può essere specificato.  
  
`[ @credential_id = ] credential_id` Il numero di identificazione delle nuove credenziali per il proxy. Il *credential_id* viene **int**, con un valore predefinito è NULL. Entrambi *credential_name* oppure *credential_id* può essere specificato.  
  
`[ @new_name = ] 'new_name'` Il nuovo nome del proxy. Il *new_name* viene **sysname**, con un valore predefinito è NULL. Quando specificato, la procedura modifica il nome del proxy per il *new_name*. Quando questo argomento è NULL, il nome del proxy rimane invariato.  
  
`[ @enabled = ] is_enabled` È fatto che il proxy è abilitato. Il *is_enabled* flag è **tinyint**, con un valore predefinito è NULL. Quando *is_enabled* viene **0**, il proxy non è abilitato e non può essere utilizzato da un passaggio di processo. Quando questo argomento è NULL, lo stato del proxy rimane invariato.  
  
`[ @description = ] 'description'` Nuova descrizione del proxy. Il *description* viene **nvarchar(512)**, con un valore predefinito è NULL. Quando questo argomento è NULL, la descrizione del proxy rimane invariata.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Entrambi **@proxy_name** oppure **@proxy_id** deve essere specificato. Se si specificano entrambi gli argomenti, devono riferirsi tutti e due allo stesso proxy per consentire la corretta esecuzione della stored procedure.  
  
 Entrambi **@credential_name** oppure **@credential_id** devono essere specificate per modificare le credenziali per il proxy. Se si specificano entrambi gli argomenti, devono riferirsi alle stesse credenziali per consentire la corretta esecuzione della stored procedure.  
  
 Questa procedura modifica il proxy, ma non modifica l'accesso al proxy. Per modificare l'accesso a un proxy, usare **sp_grant_login_to_proxy** e **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo di sicurezza predefinito può eseguire questa procedura.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene impostato il valore abilitato per il proxy `Catalog application proxy` su `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementazione di sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
