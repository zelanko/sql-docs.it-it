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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 356357df8d2c8a3202a5ff088ba2c277aa9fd73c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831123"
---
# <a name="sp_enum_sqlagent_subsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elenca i sottosistemi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>Argomenti  
 Nessuno  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**sottosistema**|**nvarchar(40)**|Nome del sottosistema.|  
|**Descrizione**|**nvarchar(512)**|Descrizione del sottosistema.|  
|**subsystem_dll**|**nvarchar (510)**|Modulo DLL contenente il sottosistema.|  
|**agent_exe**|**nvarchar (510)**|Modulo eseguibile utilizzato dal sottosistema.|  
|**start_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**event_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**stop_entry_point**|**nvarchar(30)**|Procedura richiamata da SQL Server Agent durante l'esecuzione del passaggio del processo.|  
|**max_worker_threads**|**int**|Numero massimo di thread avviati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per questo sottosistema.|  
|**subsystem_id**|**int**|Identificatore del sottosistema.|  
  
## <a name="remarks"></a>Osservazioni  
 Questa procedura elenca i sottosistemi disponibili nell'istanza.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
 Per informazioni dettagliate su **SQLAgentOperatorRole**, vedere [SQL Server Agent ruoli](../../ssms/agent/sql-server-agent-fixed-database-roles.md)predefiniti del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementare SQL Server Agent sicurezza](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
