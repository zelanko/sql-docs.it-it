---
title: sp_dbfixedrolepermission (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41c84c97027c8bfae82d3ac457c454f6a4d497e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724027"
---
# <a name="spdbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza le autorizzazioni di un ruolo predefinito del database. **sp_dbfixedrolepermission** restituisce informazioni corrette in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. L'output non riflette le modifiche alla gerarchia di autorizzazioni implementate in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per altre informazioni, vedere[le autorizzazioni &#40;motore di Database&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @rolename = ] 'role'` È il nome di un valore valido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ruolo predefinito del database. *ruolo* viene **sysname**, con un valore predefinito è NULL. Se *ruolo* non viene specificato, vengono visualizzate le autorizzazioni per tutti i ruoli predefiniti del database.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nome del ruolo predefinito del database|  
|**Autorizzazione**|**nvarchar(70)**|Le autorizzazioni associate **DbFixedRole**|  
  
## <a name="remarks"></a>Note  
 Per visualizzare un elenco dei ruoli predefiniti del database, eseguire **sp_helpdbfixedrole**. Nella tabella seguente vengono elencati i ruoli predefiniti del database.  
  
|Ruolo predefinito del database|Descrizione|  
|-------------------------|-----------------|  
|**db_owner**|Proprietari di database|  
|**db_accessadmin**|Amministratori dell'accesso ai database|  
|**db_securityadmin**|Amministratori della sicurezza dei database|  
|**db_ddladmin**|Amministratori del linguaggio DDL (Data Definition Language)|  
|**db_backupoperator**|Operatori di backup dei database|  
|**db_datareader**|Utenti con autorizzazioni di lettura per i database|  
|**db_datawriter**|Utenti con autorizzazioni di scrittura per i database|  
|**db_denydatareader**|Utenti senza autorizzazioni di lettura per i database|  
|**db_denydatawriter**|Utenti senza autorizzazioni di scrittura per i database|  
  
 I membri del **db_owner** ruolo predefinito del database dispone delle autorizzazioni di tutti gli altri ruoli predefiniti del database. Per visualizzare le autorizzazioni per i ruoli predefiniti del server, eseguire **sp_srvrolepermission**.  
  
 Il set di risultati include le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e altre attività speciali che possono essere eseguite dai membri del ruolo del database.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 Nella query seguente vengono restituite le autorizzazioni per tutti i ruoli predefiniti del database perché non ne è stato specificato uno.  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
