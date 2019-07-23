---
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b91242524f3edada4de8112558a01f09fb3310cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927221"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica l'utente associato a un'associazione al servizio remoto oppure modifica le impostazioni dell'accesso anonimo per l'associazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *binding_name*  
 Nome dell'associazione al servizio remoto da modificare. Non è possibile specificare i nomi del server, del database e dello schema.  
  
 WITH USER = \<*user_name>*  
 Specifica l'utente di database che dispone del certificato associato al servizio remoto per questa associazione. La chiave pubblica di questo certificato viene utilizzata per la crittografia e l'autenticazione dei messaggi scambiati con il servizio remoto.  
  
 ANONYMOUS  
 Specifica se viene utilizzato l'accesso anonimo durante la comunicazione con il servizio remoto. Se ANONYMOUS = ON, viene utilizzato l'accesso anonimo e le credenziali utente locale non vengono trasferite al servizio remoto. Se ANONYMOUS = OFF, le credenziali utente vengono trasferite. Se questa clausola viene omessa, il valore predefinito è OFF.  
  
## <a name="remarks"></a>Remarks  
 La chiave pubblica nel certificato associato a *user_name* viene usata per autenticare i messaggi inviati al servizio remoto e crittografare una chiave di sessione che verrà quindi usata per crittografare la conversazione. Il certificato per *user_name* deve corrispondere al certificato per un account utente nel database che ospita il servizio remoto.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione per la modifica dell'associazione al servizio remoto viene concessa per impostazione predefinita al proprietario dell'associazione al servizio remoto, ai membri del ruolo predefinito del database **db_owner** e ai membri del ruolo predefinito del server **sysadmin**.  
  
 L'utente che esegue l'istruzione ALTER REMOTE SERVICE BINDING deve disporre dell'autorizzazione di rappresentazione per l'utente specificato nell'istruzione.  
  
 Per modificare l'autorizzazione per un'associazione a un servizio remoto, utilizzare l'istruzione ALTER AUTHORIZATION.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene modificata l'associazione al servizio remoto `APBinding` in modo da crittografare i messaggi con i certificati dell'account `SecurityAccount`.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
