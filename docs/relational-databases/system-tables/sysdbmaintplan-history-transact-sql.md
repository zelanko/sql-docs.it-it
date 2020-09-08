---
description: sysdbmaintplan_history (Transact-SQL)
title: sysdbmaintplan_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 473e98da465aa9952261ae3c57d77ab9b5d2629e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517736"
---
# <a name="sysdbmaintplan_history-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Questa tabella è archiviata nel database **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|Sequenza della cronologia relativa ai piani di manutenzione del database.|  
|**plan_id**|**uniqueidentifier**|ID del piano di manutenzione del database.|  
|**plan_name**|**sysname**|Nome del piano di manutenzione del database.|  
|**database_name**|**sysname**|Nome del database associato al piano di manutenzione del database.|  
|**server_name**|**sysname**|Nome di sistema.|  
|**activity**|**nvarchar(128)**|Attività eseguita dal piano di manutenzione del database, ad esempio Backup del log delle transazioni e così via.|  
|**succeeded**|**bit**|**0** = esito positivo **1** = esito negativo|  
|**end_time**|**datetime**|Ora in cui l'azione è stata completata.|  
|**duration**|**int**|Periodo di tempo richiesto per completare l'azione del piano di manutenzione del database.|  
|**start_time**|**datetime**|Ora in cui l'azione è iniziata.|  
|**error_number**|**int**|Numero di errore segnalato in caso di esito negativo.|  
|**message**|**nvarchar(512)**|Messaggio generato da **SQLMaint**.|  
  
  
