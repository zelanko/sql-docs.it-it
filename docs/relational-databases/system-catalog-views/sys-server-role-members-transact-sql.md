---
title: Sys. server_role_members (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_role_members
- sys.server_role_members_TSQL
- server_role_members_TSQL
- sys.server_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_role_members catalog view
ms.assetid: efa20414-2c6b-45a2-a7a9-60110a24da18
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4107e6c1f675f7fae78ca384c082ef12c2fa309b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406458"
---
# <a name="sysserverrolemembers-transact-sql"></a>sys.server_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Restituisce una riga per ogni membro di ogni ruolo del server predefinito e definito dall'utente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|ID dell'entità server del ruolo.|  
|**member_principal_id**|**int**|ID dell'entità server del membro.|  
  
 Per aggiungere o rimuovere l'appartenenza al ruolo di server, usare il [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)istruzione.  
  
## <a name="permissions"></a>Permissions  
 Gli account di accesso possono visualizzare la propria appartenenza al ruolo di server e visualizzare gli oggetti principal_id dei membri dei ruoli predefiniti del server. Per visualizzare tutte le appartenenze al ruolo del server, è necessario il **VIEW DEFINITION ON SERVER ROLE** autorizzazioni o appartenenza al gruppo il **securityadmin** ruolo predefinito del server.  
  
 Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i nomi e gli ID dei ruoli e i relativi membri.  
  
```  
SELECT sys.server_role_members.role_principal_id, role.name AS RoleName,   
    sys.server_role_members.member_principal_id, member.name AS MemberName  
FROM sys.server_role_members  
JOIN sys.server_principals AS role  
    ON sys.server_role_members.role_principal_id = role.principal_id  
JOIN sys.server_principals AS member  
    ON sys.server_role_members.member_principal_id = member.principal_id;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Ruoli a livello di server](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
