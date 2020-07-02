---
title: sys. sp_cdc_help_jobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 77595c353522dc2db3452b51f3a0395346c85619
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768631"
---
# <a name="syssp_cdc_help_jobs-transact-sql"></a>sys.sp_cdc_help_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni su tutti i processi di pulizia dell'acquisizione dei dati delle modifiche o di acquisizione nel database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ID del processo.|  
|**job_type**|**nvarchar (20)**|Tipo di processo.|  
|**maxtrans**|**int**|Numero massimo di transazioni da elaborare in ogni ciclo di analisi.<br /><br /> **maxtrans** è valido solo per i processi di acquisizione.|  
|**maxscans**|**int**|Numero massimo di cicli di analisi da eseguire per estrarre tutte le righe dal log.<br /><br /> **maxscans** è valido solo per i processi di acquisizione.|  
|**continuo**|**bit**|Flag che indica se l'esecuzione del processo di acquisizione deve essere continua (1) o come singola occorrenza (0). Per ulteriori informazioni, vedere [sys. sp_cdc_add_job &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).<br /><br /> **Continuous** è valido solo per i processi di acquisizione.|  
|**PollingInterval**|**bigint**|Numero di secondi tra cicli di analisi del log.<br /><br /> **pollingInterval** è valido solo per i processi di acquisizione.|  
|**conservazione**|**bigint**|Numero di minuti per i quali vengono conservate le righe delle modifiche nelle tabelle delle modifiche.<br /><br /> la **conservazione** è valida solo per i processi di pulizia.|  
|**threshold**|**bigint**|Numero massimo di voci che possono essere eliminate utilizzando un'unica istruzione nel processo di pulizia.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del database **db_owner** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sui processi di acquisizione e di pulizia definiti per il database `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [dbo. cdc_jobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
