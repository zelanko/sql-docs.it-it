---
title: DROP APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_APPLICATION_ROLE_TSQL
- DROP APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- dropping application roles
- deleting application roles
- removing application roles
- application roles [SQL Server], removing
- DROP APPLICATION ROLE statement
ms.assetid: 44121ee7-ef40-405d-b03b-f8ddb4e3c559
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 77bf5aad865c2c8a858c8a9c47fc5706d644cfb3
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361461"
---
# <a name="drop-application-role-transact-sql"></a>DROP APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Rimuove un ruolo applicazione dal database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP APPLICATION ROLE rolename  
```  
  
## <a name="arguments"></a>Argomenti  
 *rolename*  
 Specifica il nome del ruolo applicazione da eliminare.  
  
## <a name="remarks"></a>Remarks  
 Se il ruolo applicazione possiede un'entità a sicurezza diretta, tale ruolo non può essere rimosso. Prima di rimuovere un ruolo applicazione proprietario di entità a protezione diretta, è necessario innanzitutto trasferire la proprietà delle entità a protezione diretta oppure rimuoverle.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER ANY APPLICATION ROLE nel database.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il ruolo applicazione "weekly_ledger" viene rimosso dal database.  
  
```  
DROP APPLICATION ROLE weekly_ledger;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli applicazione](../../relational-databases/security/authentication-access/application-roles.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
