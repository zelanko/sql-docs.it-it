---
description: sys.login_token (Transact-SQL)
title: sys. login_token (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 339964a859d5e95d88853781a8b2b43f341f23be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377807"
---
# <a name="syslogin_token-transact-sql"></a>sys.login_token (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga per ogni entità server appartenente al token dell'account di accesso.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|ID dell'entità. Questo valore è univoco all'interno del server.|  
|**sid**|**varbinary (85)**|ID di sicurezza dell'entità. Se si tratta di un'entità di Windows, **SID** = SID di Windows. Se viene eseguito il mapping dell'account di accesso a un certificato, **SID** = GUID del certificato.|  
|**nome**|**nvarchar(128)**|Nome dell'entità. Questo valore è univoco all'interno del server.|  
|**type**|**nvarchar(128)**|Descrizione del tipo dell'entità. Viene eseguito il mapping di tutti i tipi a **SID**. I possibili valori sono i seguenti:<br /><br /> SQL LOGIN<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> LOGIN MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**utilizzo**|**nvarchar(128)**|Specifica che l'entità partecipa alla valutazione di autorizzazioni GRANT or DENY o funge da autenticatore.<br /><br /> I valori validi sono i seguenti:<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>Vedere anche  
 [sys. user_token &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
