---
title: dbo. sysjobsteps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d98b1ccc4dc8da3ba9d494a78bfea3727102da07
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827320"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene informazioni relative a tutti i passaggi di un processo da eseguire tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ID del processo.|  
|**step_id**|**int**|ID del passaggio del processo.|  
|**step_name**|**sysname**|Nome del passaggio del processo.|  
|**sottosistema**|**nvarchar(40)**|Nome del sottosistema utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per eseguire il passaggio del processo|  
|**comando**|**nvarchar(max)**|Comando che deve essere eseguito dal **sottosistema**.|  
|**flags**|**int**|Riservato.|  
|**additional_parameters**|**ntext**|Riservato.|  
|**cmdexec_success_code**|**int**|Valore a livello di errore restituito dai passaggi del sottosistema **CmdExec** per indicare l'esito positivo.|  
|**on_success_action**|**tinyint**|Azione da eseguire quando un passaggio viene eseguito correttamente.|  
|**on_success_step_id**|**int**|ID del passaggio successivo da eseguire quando un passaggio viene eseguito correttamente.|  
|**on_fail_action**|**tinyint**|Azione da eseguire quando un passaggio non viene eseguito correttamente.|  
|**on_fail_step_id**|**int**|ID del passaggio successivo da eseguire quando un passaggio non viene eseguito correttamente.|  
|**Server**|**sysname**|Riservato.|  
|**database_name**|**sysname**|Nome del database in cui viene eseguito il **comando** se **sottosistema** è TSQL.|  
|**database_user_name**|**sysname**|Nome dell'utente del database di cui viene utilizzato l'account quando si esegue il passaggio.|  
|**retry_attempts**|**int**|Numero di tentativi in caso di esecuzione errata del passaggio.|  
|**retry_interval**|**int**|Periodo di attesa tra un tentativo e il successivo.|  
|**os_run_priority**|**int**|Riservato.|  
|**output_file_name**|**nvarchar(200)**|Nome del file in cui viene salvato l'output del passaggio quando il **sottosistema** è TSQL, PowerShell o **CmdExec**_._|  
|**last_run_outcome**|**int**|Risultato dell'esecuzione precedente del passaggio del processo.<br /><br /> **0** = non riuscito<br /><br /> **1** = operazione completata<br /><br /> **2** = nuovo tentativo<br /><br /> **3** = annullato<br /><br /> **5** = sconosciuto|  
|**last_run_duration**|**int**|Durata (hhmmss) dell'ultima esecuzione del passaggio.|  
|**last_run_retries**|**int**|Numero di tentativi durante l'ultima esecuzione del passaggio del processo.|  
|**last_run_date**|**int**|Data (yyyymmdd) di inizio dell'ultima esecuzione del passaggio.|  
|**last_run_time**|**int**|Ora (hhmmss) di inizio dell'ultima esecuzione del passaggio.|  
|**proxy_id**|**int**|Proxy per il passaggio del processo.|  
|**step_uid**|**uniqueidentifier**|Identificatore per il passaggio del processo.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Agent tabelle &#40;&#41;Transact-SQL](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
