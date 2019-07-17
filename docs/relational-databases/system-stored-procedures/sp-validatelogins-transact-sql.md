---
title: sp_validatelogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bd29100f8f7c54906b8aeafa98a7cf67f526db8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021061"
---
# <a name="spvalidatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli utenti e i gruppi di Windows di cui è stato eseguito il mapping a entità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non esistono più nell'ambiente Windows.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary(85)**|Identificatore di sicurezza (SID) di Windows dell'utente o gruppo di Windows.|  
|**Account di accesso NT**|**sysname**|Nome dell'utente o gruppo di Windows.|  
  
## <a name="remarks"></a>Note  
 Se l'entità a livello del server isolata (orfana) è proprietaria di un utente del database, tale utente deve essere rimosso prima di poter rimuovere l'entità server isolata (orfana). Per rimuovere un utente del database, usare [DROP USER](../../t-sql/statements/drop-user-transact-sql.md). Se l'entità a livello del server è proprietaria di entità a sicurezza diretta nel database, è necessario trasferire la proprietà delle entità a sicurezza diretta o rimuoverle. Per trasferire la proprietà dell'entità a protezione diretta database, utilizzare [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Per rimuovere i mapping per gli utenti di Windows e i gruppi che non esistono più, usare [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** oppure **securityadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzati gli utenti e i gruppi di Windows non più disponibili, ma per i quali esistono ancora autorizzazioni di accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
