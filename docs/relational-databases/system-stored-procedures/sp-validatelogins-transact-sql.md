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
ms.openlocfilehash: 8299e334ff3219c41a3a4adfcc29f238d0ed81b3
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891266"
---
# <a name="sp_validatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni sugli utenti e i gruppi di Windows di cui è stato eseguito il mapping a entità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non esistono più nell'ambiente Windows.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary (85)**|Identificatore di sicurezza (SID) di Windows dell'utente o gruppo di Windows.|  
|**NT Login**|**sysname**|Nome dell'utente o gruppo di Windows.|  
  
## <a name="remarks"></a>Osservazioni  
 Se l'entità a livello del server isolata (orfana) è proprietaria di un utente del database, tale utente deve essere rimosso prima di poter rimuovere l'entità server isolata (orfana). Per rimuovere un utente del database, utilizzare [drop user](../../t-sql/statements/drop-user-transact-sql.md). Se l'entità a livello del server è proprietaria di entità a sicurezza diretta nel database, è necessario trasferire la proprietà delle entità a sicurezza diretta o rimuoverle. Per trasferire la proprietà delle entità a protezione diretta del database, utilizzare [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Per rimuovere i mapping a utenti e gruppi di Windows che non esistono più, usare [Drop login](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o **securityadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzati gli utenti e i gruppi di Windows non più disponibili, ma per i quali esistono ancora autorizzazioni di accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure di sicurezza &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
