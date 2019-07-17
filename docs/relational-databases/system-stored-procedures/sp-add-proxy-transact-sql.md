---
title: sp_add_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4aa4120db7b45cb0b3a7d7a10bb53931b8300d9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088485"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge il proxy [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy da creare. Il *nome_proxy* viene **sysname**, con un valore predefinito è NULL. Quando la *nome_proxy* è NULL o una stringa vuota, il nome delle impostazioni predefinite del proxy per il *nome_utente* fornito.  
  
`[ @enabled = ] is_enabled` Specifica se il proxy è abilitato. Il *is_enabled* flag è **tinyint**, con un valore predefinito è 1. Quando *is_enabled* viene **0**, il proxy non è abilitato e non può essere utilizzato da un passaggio di processo.  
  
`[ @description = ] 'description'` Descrizione del proxy. La descrizione è **nvarchar(512)** , con un valore predefinito è NULL. La descrizione consente di documentare il proxy, ma non viene altrimenti utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questo argomento è pertanto facoltativo.  
  
`[ @credential_name = ] 'credential_name'` Il nome delle credenziali per il proxy. Il *credential_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *credential_name* oppure *credential_id* deve essere specificato.  
  
`[ @credential_id = ] credential_id` Il numero di identificazione delle credenziali per il proxy. Il *credential_id* viene **int**, con un valore predefinito è NULL. Entrambi *credential_name* oppure *credential_id* deve essere specificato.  
  
`[ @proxy_id = ] id OUTPUT` Il numero di identificazione proxy assegnato al proxy, se è stato creato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 Questa stored procedure deve essere eseguita **msdb** database.  
  
 Un proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gestisce la sicurezza per i passaggi di processo che implicano i sottosistemi diversi da [!INCLUDE[tsql](../../includes/tsql-md.md)]. Ogni proxy corrisponde a una credenziale di sicurezza Un proxy può avere accesso a qualsiasi numero di sottosistemi.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo di sicurezza predefinito può eseguire questa procedura.  
  
 I membri del **sysadmin** ruolo di sicurezza predefinito possa creare passaggi di processo che utilizzano qualsiasi proxy. Utilizzare la stored procedure [sp_grant_login_to_proxy &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) per concedere l'accesso altri account di accesso al proxy.  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene creato un proxy per le credenziali `CatalogApplicationCredential`. Nel codice si presuppone che le credenziali esistano già. Per altre informazioni sulle credenziali, vedere [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
