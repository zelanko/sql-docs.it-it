---
title: sys. dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84be14f04a39f3697c6cf0bca87c5369cced2c48
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011610"
---
# <a name="sysdm_exec_background_job_queue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Restituisce una riga per ogni processo di Query Processor pianificato per l'esecuzione asincrona (in background).  
  
> **Nota!** Per chiamare questo **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** oggetto da o **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]** , usare il nome **sys. dm_pdw_nodes_exec_background_job_queue**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|Ora in cui il processo viene aggiunto alla coda.|  
|**job_id**|**int**|Identificatore di processo.|  
|**database_id**|**int**|Database in cui il processo viene eseguito.|  
|**object_id1**|**int**|Il valore dipende dal tipo di processo. Per altre informazioni, vedere la sezione Osservazioni.|  
|**object_id2**|**int**|Il valore dipende dal tipo di processo. Per altre informazioni, vedere la sezione Osservazioni.|  
|**object_id3**|**int**|Il valore dipende dal tipo di processo. Per altre informazioni, vedere la sezione Osservazioni.|  
|**object_id4**|**int**|Il valore dipende dal tipo di processo. Per altre informazioni, vedere la sezione Osservazioni.|  
|**error_code**|**int**|Codice di errore nel caso di reinserimento del processo a causa di un errore. È NULL in caso di processo sospeso, non prelevato o completato.|  
|**request_type**|**smallint**|Tipo di richiesta del processo.|  
|**retry_count**|**smallint**|Numero di volte che il processo è stato prelevato dalla coda e reinserito nella coda per mancanza di risorse o altri motivi.|  
|**in_progress**|**smallint**|Indica se è stata avviata l'esecuzione del processo.<br /><br /> 1 = avviato<br /><br /> 0 = Processo in attesa di avvio|  
|**session_id**|**smallint**|Identificatore di sessione.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   
  
## <a name="remarks"></a>Osservazioni  
 In questa vista vengono restituite solo le informazioni relative ai processi asincroni di aggiornamento delle statistiche. Per ulteriori informazioni sulle statistiche di aggiornamento asincrone, vedere [statistiche](../../relational-databases/statistics/statistics.md).  
  
 I valori di **object_id1** tramite **object_id4** dipendono dal tipo della richiesta di processo. Nella tabella seguente viene descritto il significato delle colonne per i diversi tipi di processo.  
  
|Tipo di richiesta|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|Aggiornamenti asincroni delle statistiche|ID di tabella o vista|ID delle statistiche|Non usato|Non usato|  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il numero di processi asincroni attivi nella coda in background per ogni database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Statistiche](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



