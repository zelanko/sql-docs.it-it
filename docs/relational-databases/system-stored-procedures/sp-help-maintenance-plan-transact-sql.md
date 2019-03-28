---
title: sp_help_maintenance_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f842060c6ca621fc52fa34f08838541dc65e993
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535633"
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sul piano di manutenzione specificato. Se non è stato specificato alcun piano, vengono restituite informazioni su tutti i piani di manutenzione.  
  
> **NOTA:** Questa stored procedure viene utilizzata con piani di manutenzione del database. Questa caratteristica è stata sostituita da piani di manutenzione che non utilizzano questa stored procedure. Utilizzare questa stored procedure per mantenere i piani di manutenzione del database nelle installazioni aggiornate da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @plan_id = ] 'plan\_id'` Specifica l'ID del piano di manutenzione. *plan_id* viene **UNIQUEIDENTIFIER**. Il valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
 Se *plan_id* omette **sp_help_maintenance_plan** restituirà tre tabelle: Piano, Database e processi.  
  
### <a name="plan-table"></a>Tabella relativa al piano  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID del piano di manutenzione.|  
|**plan_name**|**sysname**|Nome del piano di manutenzione.|  
|**date_created**|**datetime**|Data di creazione del piano di manutenzione.|  
|**owner**|**sysname**|Proprietario del piano di manutenzione.|  
|**max_history_rows**|**int**|Numero massimo di righe assegnate per la registrazione della cronologia del piano di manutenzione nella tabella di sistema.|  
|**remote_history_server**|**int**|Nome del server remoto in cui è possibile scrivere il report della cronologia.|  
|**max_remote_history_rows**|**int**|Numero massimo di righe assegnate nella tabella di sistema di un server remoto in cui è possibile scrivere il report della cronologia.|  
|**user_defined_1**|**int**|Il valore predefinito è NULL.|  
|**user_defined_2**|**nvarchar(100)**|Il valore predefinito è NULL.|  
|**user_defined_3**|**datetime**|Il valore predefinito è NULL.|  
|**user_defined_4**|**uniqueidentifier**|Il valore predefinito è NULL.|  
  
### <a name="database-table"></a>Tabella relativa ai database  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**database_name**|Nome di tutti i database associati al piano di manutenzione. *database_name* è di tipo **sysname**.|  
  
### <a name="job-table"></a>Tabella relativa ai processi  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**job_id**|ID di tutti i processi associati al piano di manutenzione. *job_id* viene **uniqueidentifier**.|  
  
## <a name="remarks"></a>Note  
 **sp_help_maintenance_plan** è il **msdb** database.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono illustrate le informazioni relative al piano di manutenzione FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Piano di manutenzione database Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
