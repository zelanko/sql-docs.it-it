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
ms.openlocfilehash: 42a98fe7af16c4e8aab22d6ace02f359dfe02c54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096197"
---
# <a name="sp_help_maintenance_plan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sul piano di manutenzione specificato. Se non è stato specificato alcun piano, vengono restituite informazioni su tutti i piani di manutenzione.  
  
> **Nota:** Questa stored procedure viene utilizzata con i piani di manutenzione del database. Questa caratteristica è stata sostituita da piani di manutenzione che non utilizzano questa stored procedure. Utilizzare questa stored procedure per mantenere i piani di manutenzione del database nelle installazioni aggiornate da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @plan_id = ] 'plan\_id'`Specifica l'ID del piano di manutenzione. *plan_id* è di tipo **uniqueidentifier**. Il valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 nessuno  
  
## <a name="result-sets"></a>Set di risultati  
 Se *plan_id* viene specificato, **sp_help_maintenance_plan** restituirà tre tabelle: piano, database e processo.  
  
### <a name="plan-table"></a>Tabella relativa al piano  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID del piano di manutenzione.|  
|**plan_name**|**sysname**|Nome del piano di manutenzione.|  
|**date_created**|**datetime**|Data di creazione del piano di manutenzione.|  
|**proprietario**|**sysname**|Proprietario del piano di manutenzione.|  
|**max_history_rows**|**int**|Numero massimo di righe assegnate per la registrazione della cronologia del piano di manutenzione nella tabella di sistema.|  
|**remote_history_server**|**int**|Nome del server remoto in cui è possibile scrivere il report della cronologia.|  
|**max_remote_history_rows**|**int**|Numero massimo di righe assegnate nella tabella di sistema di un server remoto in cui è possibile scrivere il report della cronologia.|  
|**user_defined_1**|**int**|Il valore predefinito è NULL.|  
|**user_defined_2**|**nvarchar (100)**|Il valore predefinito è NULL.|  
|**user_defined_3**|**datetime**|Il valore predefinito è NULL.|  
|**user_defined_4**|**uniqueidentifier**|Il valore predefinito è NULL.|  
  
### <a name="database-table"></a>Tabella relativa ai database  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**database_name**|Nome di tutti i database associati al piano di manutenzione. *database_name* è di **tipo sysname**.|  
  
### <a name="job-table"></a>Tabella relativa ai processi  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**job_id**|ID di tutti i processi associati al piano di manutenzione. *job_id* è di tipo **uniqueidentifier**.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_maintenance_plan** si trova nel database **msdb** .  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono illustrate le informazioni relative al piano di manutenzione FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Stored procedure del piano di manutenzione del database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
