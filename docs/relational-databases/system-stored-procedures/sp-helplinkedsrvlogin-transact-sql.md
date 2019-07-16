---
title: sp_helplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1728b3e5d4cd3189a8d9a01a8b72ecedaf7cb6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122456"
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui mapping degli account di accesso definiti per un determinato server collegato utilizzato per query distribuite e stored procedure remote.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @rmtsrvname = ] 'rmtsrvname'` È il nome del server collegato che viene applicato il mapping dell'account di accesso. *rmtsrvname* viene **sysname**, con un valore predefinito è NULL. NULL indica che vengono restituiti i mapping degli account di accesso definiti per tutti i server collegati nel computer locale in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione.  
  
`[ @locallogin = ] 'locallogin'` È il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso nel server locale che dispone di un mapping per il server collegato *rmtsrvname*. *locallogin* viene **sysname**, con un valore predefinito è NULL. NULL indica che tutti i mapping definiti nella *rmtsrvname* vengono restituiti. Se non è NULL, un mapping per *locallogin* al *rmtsrvname* deve esistere già. *locallogin* può essere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso o un utente di Windows. È necessario che l'utente di Windows disponga dell'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ottenuto tramite concessione diretta o in base all'appartenenza a un gruppo di Windows che dispone dell'accesso.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Server collegato**|**sysname**|Nome del server collegato.|  
|**Account di accesso locale**|**sysname**|Account di accesso locale a cui fa riferimento il mapping.|  
|**Il mapping automatico**|**smallint**|0 = **account di accesso locale** viene eseguito il mapping al **Login remoto** durante la connessione al **Server collegato**.<br /><br /> 1 = **account di accesso locale** viene eseguito il mapping allo stesso account di accesso e password quando ci si connette a **Server collegato**.|  
|**Account di accesso remoto**|**sysname**|Nome account di accesso nel **LinkedServer** a cui viene eseguito il mapping **LocalLogin** quando **IsSelfMapping** è 0. Se **IsSelfMapping** è 1, **RemoteLogin** è NULL.|  
  
## <a name="remarks"></a>Note  
 Prima di eliminare i mapping di account di accesso, usare **sp_helplinkedsrvlogin** per determinare i server collegati coinvolti.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni non vengono controllate.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>R. Visualizzazione dei mapping degli account di accesso per tutti i server collegati  
 Nell'esempio seguente vengono visualizzati i mapping degli account di accesso per tutti i server collegati definiti nel computer locale in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione.  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B. Visualizzazione di tutti i mapping degli account di accesso per un server collegato  
 Nell'esempio seguente vengono visualizzati tutti i mapping degli account di accesso definiti a livello locale per il server collegato `Sales`.  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C. Visualizzazione di tutti i mapping per un account di accesso locale  
 Nell'esempio seguente vengono visualizzati tutti i mapping definiti a livello locale per l'account di accesso `Mary`.  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
