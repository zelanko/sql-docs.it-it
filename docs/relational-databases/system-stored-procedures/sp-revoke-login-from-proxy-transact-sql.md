---
description: sp_revoke_login_from_proxy (Transact-SQL)
title: sp_revoke_login_from_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 39857bce8c0fc50c1773709d70e7e477b669b282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473852"
---
# <a name="sp_revoke_login_from_proxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove l'accesso a un proxy per un'entità di sicurezza.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'` Nome dell'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso, del ruolo del server o del ruolo del database **msdb** per il quale rimuovere l'accesso. il *nome* è di **tipo nvarchar (256)** e non prevede alcun valore predefinito.  
  
`[ @proxy_id = ] id` ID del proxy per il quale rimuovere l'accesso. È necessario specificare *ID* o *proxy_name* , ma non è possibile specificarli entrambi. *ID* è di **tipo int**e il valore predefinito è null.  
  
`[ @proxy_name = ] 'proxy_name'` Nome del proxy per il quale rimuovere l'accesso. È necessario specificare *ID* o *proxy_name* , ma non è possibile specificarli entrambi. Il *proxy_name* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 L'esecuzione dei processi di proprietà dell'account di accesso che fanno riferimento al proxy corrente avranno esito negativo.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire questa stored procedure, è necessario che gli utenti siano membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente all'account di accesso `terrid` viene revocato l'accesso al proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di SQL Server Agent &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
