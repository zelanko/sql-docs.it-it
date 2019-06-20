---
title: sp_audit_write (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 450b1cdde9185edee5eac41f52d209e43a7ae22f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62996253"
---
# <a name="spauditwrite-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Aggiunge un evento di controllo definiti dall'utente per il **USER_DEFINED_AUDIT_GROUP**. Se **USER_DEFINED_AUDIT_GROUP** non è abilitato, **sp_audit_write** viene ignorato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>Argomenti  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 Un parametro definito dall'utente e registrato nella **user_defined_event_id** colonna del log di controllo. *@user_defined_event_id* è di tipo **smallint**.  
  
 `[ @succeeded = ] succeeded`  
 Parametro passato dall'utente per indicare se l'evento ha avuto esito positivo o meno. Viene visualizzato nella colonna del log di controllo indicante l'esito positivo. `@succeeded` viene **bit**.  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 Testo definito dall'utente e registrato nella nuova colonna user_defined_event_id del log di controllo. `@user_defined_information` viene **nvarchar (4000)** .  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
 Gli errori sono causati da parametri di input errati o da problemi di scrittura nel log di controllo di destinazione.  
  
## <a name="remarks"></a>Note  
 Quando la **USER_DEFINED_AUDIT_GROUP** viene aggiunto a una specifica del controllo server o una specifica del controllo del database, l'evento attivato da **sp_audit_write** verranno inclusi nel log di controllo.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **pubblica** ruolo predefinito del database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>A. Creazione di un evento di controllo definito dall'utente con testo informativo  
 Nell'esempio seguente viene creato un evento di controllo con ID 27, valore di esito positivo pari a 0 e testo informativo facoltativo incluso.  
  
```  
EXEC sp_audit_write @user_defined_event_id =  27 ,   
              @succeeded =  0   
            , @user_defined_information = N'Access to a monitored object.' ;  
```  
  
### <a name="b--creating-a-user-defined-audit-event-without-informational-text"></a>B.  Creazione di un evento di controllo definito dall'utente senza testo informativo  
 Nell'esempio seguente viene creato un evento di controllo con ID 27, valore di esito positivo pari a 0 e senza testo informativo o nomi di parametri facoltativi.  
  
```  
EXEC sp_audit_write 27, 0;  
  
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
  
  
