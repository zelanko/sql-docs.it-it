---
title: sp_grant_login_to_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: bdfeab5754a2397c01ace2bb9f822fa168eeef6b
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005861"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede a un'entità di sicurezza l'accesso a un proxy.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @login_name = ] 'login_name'` il nome dell'account di accesso a cui concedere l'accesso. *Login_name* è di **tipo nvarchar (256)** e il valore predefinito è null. È necessario specificare uno dei **\@login_name**, **\@fixed_server_role**o **\@msdb_role** oppure il stored procedure ha esito negativo.  
  
`[ @fixed_server_role = ] 'fixed_server_role'` il ruolo predefinito del server a cui concedere l'accesso. *Fixed_server_role* è di **tipo nvarchar (256)** e il valore predefinito è null. È necessario specificare uno dei **\@login_name**, **\@fixed_server_role**o **\@msdb_role** oppure il stored procedure ha esito negativo.  
  
`[ @msdb_role = ] 'msdb_role'` il ruolo del database nel database **msdb** al quale concedere l'accesso. *Msdb_role* è di **tipo nvarchar (256)** e il valore predefinito è null. È necessario specificare uno dei **\@login_name**, **\@fixed_server_role**o **\@msdb_role** oppure il stored procedure ha esito negativo.  
  
`[ @proxy_id = ] id` identificatore del proxy al quale concedere l'accesso. *ID* è di **tipo int**e il valore predefinito è null. È necessario specificare uno dei **\@proxy_id** o **\@proxy_name** oppure il stored procedure ha esito negativo.  
  
`[ @proxy_name = ] 'proxy_name'` il nome del proxy al quale concedere l'accesso. *Proxy_name* è di **tipo nvarchar (256)** e il valore predefinito è null. È necessario specificare uno dei **\@proxy_id** o **\@proxy_name** oppure il stored procedure ha esito negativo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_grant_login_to_proxy** deve essere eseguito dal database **msdb** .  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_grant_login_to_proxy**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene consentito all'account di accesso `adventure-works\terrid` di utilizzare il proxy `Catalog application proxy`.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
