---
title: dbo.syssubsystems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d685f5e8837feebffeeeade95697f4f3bfea4c81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470501"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene informazioni su tutti i sottosistemi proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent disponibili. Il **syssubsystems** tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|ID del sottosistema.|  
|**subsystem**|**nvarchar(40)**|Nome del sottosistema.|  
|**description_id**|**int**|ID della riga nel messaggio il **Sys. Messages** vista del catalogo che contiene la descrizione del sottosistema.|  
|**subsystem_dll**|**nvarchar(255)**|Posizione del file dll del sottosistema.|  
|**agent_exe**|**nvarchar(255)**|Percorso completo del file eseguibile che utilizza il sottosistema.|  
|**start_entry_point**|**nvarchar(30)**|Funzione richiamata quando il sottosistema viene inizializzato.|  
|**event_entry_point**|**nvarchar(30)**|Funzione richiamata quando viene eseguito un passaggio del sottosistema.|  
|**stop_entry_point**|**nvarchar(30)**|Funzione richiamata quando l'esecuzione di un sottosistema viene interrotta.|  
|**max_worker_threads**|**int**|Numero massimo di passaggi simultanei per un sottosistema specifico.|  
  
## <a name="remarks"></a>Note  
 Solo i membri del **sysadmin** ruolo predefinito del server può accedere a questa tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [Sys. Messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
