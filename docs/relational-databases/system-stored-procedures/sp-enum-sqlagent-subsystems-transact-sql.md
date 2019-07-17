---
title: sp_enum_sqlagent_subsystems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 963cbcea93091eb48b8c73214ee3bc509f118e67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124668"
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elenca i sottosistemi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>Argomenti  
 Nessuna  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|Nome del sottosistema.|  
|**description**|**nvarchar(512)**|Descrizione del sottosistema.|  
|**subsystem_dll**|**nvarchar(510)**|Modulo DLL contenente il sottosistema.|  
|**agent_exe**|**nvarchar(510)**|Modulo eseguibile utilizzato dal sottosistema.|  
|**start_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**event_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**stop_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**max_worker_threads**|**int**|Numero massimo di thread avviati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per questo sottosistema.|  
|**subsystem_id**|**int**|Identificatore del sottosistema.|  
  
## <a name="remarks"></a>Note  
 Questa procedura elenca i sottosistemi disponibili nell'istanza.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
 Per informazioni dettagliate sui **SQLAgentOperatorRole**, vedere [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
