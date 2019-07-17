---
title: xp_enumgroups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 885e29f8abbeb185017bc2472566e41596a56900
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116766"
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di gruppi locali di Microsoft Windows o di gruppi globali definiti nel dominio Windows specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **«** *nome_dominio* **»**  
 Nome del dominio Windows per cui si desidera ottenere un elenco di gruppi globali. *nome_dominio* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Gruppo**|**sysname**|Nome del gruppo di Windows.|  
|**comment**|**sysname**|Descrizione del gruppo di Windows fornita da Windows.|  
  
## <a name="remarks"></a>Note  
 Se *domain_name* è il nome del computer basato su Windows che un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in o nessun nome di dominio viene specificato, **xp_enumgroups** enumera i gruppi locali dal computer che è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **xp_enumgroups** non può essere utilizzato quando un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in Windows 98.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_owner** ruolo predefinito del database nel **master** database o l'appartenenza al **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono elencati i gruppi nel dominio `sales`.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Stored procedure estese generali &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
