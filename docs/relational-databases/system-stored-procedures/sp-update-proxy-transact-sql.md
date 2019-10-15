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
ms.openlocfilehash: ec6c40abd080c86722565762fab3b4f9d30bd0c0
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305313"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
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
`[ @proxy_id = ] id` il numero di identificazione del proxy da modificare. *Proxy_id* è di **tipo int**e il valore predefinito è null.  
  
`[ @proxy_name = ] 'proxy_name'` il nome del proxy da modificare. *Proxy_name* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @credential_name = ] 'credential_name'` il nome delle nuove credenziali per il proxy. *Credential_name* è di **tipo sysname**e il valore predefinito è null. È possibile specificare *credential_name* o *credential_id* .  
  
`[ @credential_id = ] credential_id` il numero di identificazione delle nuove credenziali per il proxy. *Credential_id* è di **tipo int**e il valore predefinito è null. È possibile specificare *credential_name* o *credential_id* .  
  
`[ @new_name = ] 'new_name'` il nuovo nome del proxy. *New_name* è di **tipo sysname**e il valore predefinito è null. Quando viene specificato, la procedura modifica il nome del proxy in *new_name*. Quando questo argomento è NULL, il nome del proxy rimane invariato.  
  
`[ @enabled = ] is_enabled` indica se il proxy è abilitato. Il flag *is_enabled* è di **tinyint**e il valore predefinito è null. Quando *is_enabled* è **0**, il proxy non è abilitato e non può essere utilizzato da un passaggio di processo. Quando questo argomento è NULL, lo stato del proxy rimane invariato.  
  
`[ @description = ] 'description'` la nuova descrizione del proxy. La *Descrizione* è di **tipo nvarchar (512)** e il valore predefinito è null. Quando questo argomento è NULL, la descrizione del proxy rimane invariata.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 È necessario specificare **\@proxy_name** o **\@proxy_id** . Se si specificano entrambi gli argomenti, devono riferirsi tutti e due allo stesso proxy per consentire la corretta esecuzione della stored procedure.  
  
 È necessario specificare **\@credential_name** o **\@credential_id** per modificare le credenziali per il proxy. Se si specificano entrambi gli argomenti, devono riferirsi alle stesse credenziali per consentire la corretta esecuzione della stored procedure.  
  
 Questa procedura modifica il proxy, ma non modifica l'accesso al proxy. Per modificare l'accesso a un proxy, usare **sp_grant_login_to_proxy** e **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Permissions  
 Questa procedura può essere eseguita solo dai membri del ruolo di sicurezza predefinito **sysadmin** .  
  
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
 [Stored procedure &#40;SQL Server Agent Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementare SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)@no__t di sicurezza-1  
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
