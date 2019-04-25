---
title: dbo.sysjobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797fb6183863bb0249bd0cda6024d0e95914e82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470849"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene informazioni sull'esecuzione di processi pianificati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa tabella è archiviata nel **msdb** database.  
  
> **NOTA:** I dati vengono aggiornati solo dopo il completamento di jobstep.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Identificatore univoco della riga.|  
|**job_id**|**uniqueidentifier**|ID del processo.|  
|**step_id**|**int**|ID del passaggio del processo.|  
|**step_name**|**sysname**|Nome del passaggio.|  
|**sql_message_id**|**int**|ID di un messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito se l'esecuzione del processo ha esito negativo.|  
|**sql_severity**|**int**|Gravità di qualsiasi errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**message**|**nvarchar(4000)**|Eventuale testo di un messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**run_status**|**int**|Stato di esecuzione del processo:<br /><br /> **0** = non è riuscita<br /><br /> **1** = Succeeded<br /><br /> **2** = Retry<br /><br /> **3** = annullato<br /><br /> **4** = in corso|  
|**run_date**|**int**|Data di avvio dell'esecuzione del processo o del passaggio. Per una cronologia dei processi o dei passaggi in corso, rappresenta la data/ora di scrittura della cronologia.|  
|**run_time**|**int**|Ora di inizio dell'esecuzione del processo o del passaggio.|  
|**run_duration**|**int**|Tempo trascorso per l'esecuzione del processo o passaggio **HHMMSS** formato.|  
|**operator_id_emailed**|**int**|ID dell'operatore che ha ricevuto una notifica tramite posta elettronica al termine dell'esecuzione del processo.|  
|**operator_id_netsent**|**int**|ID dell'operatore che ha ricevuto un messaggio al termine dell'esecuzione del processo.|  
|**operator_id_paged**|**int**|ID dell'operatore che ha ricevuto una notifica tramite cercapersone al termine dell'esecuzione del processo.|  
|**retries_attempted**|**int**|Numero di tentativi di esecuzione del processo o del passaggio.|  
|**server**|**sysname**|Nome del server in cui è stato eseguito il processo.|  
  
  ## <a name="example"></a>Esempio
 Quanto segue [!INCLUDE[tsql](../../includes/tsql-md.md)] query convertirà il **fase di esecuzione** e **Durata esecuzione** colonne in un formato più intuitivo.  Eseguire lo script in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
