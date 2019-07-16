---
title: DM os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d23a0f8cbf3d0cb712cd0796256c1a6c7beb0ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899852"
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per contatore delle prestazioni gestito dal server. Per informazioni su ogni contatore delle prestazioni, vedere [usare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
> [!NOTE]  
>  Per chiamare questo elemento dal [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oppure [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], usare il nome **sys.dm_pdw_nodes_os_performance_counters**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Categoria di appartenenza del contatore.|  
|**counter_name**|**nchar(128)**|Nome del contatore. Per ottenere ulteriori informazioni su un contatore, si tratta del nome dell'argomento da selezionare dall'elenco dei contatori [usare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md). |  
|**instance_name**|**nchar(128)**|Nome dell'istanza specifica del contatore. Spesso include il nome del database.|  
|**cntr_value**|**bigint**|Valore corrente del contatore.<br /><br /> **Nota:** Per i contatori al secondo, questo valore è cumulativo. Il valore relativo alla frequenza deve essere calcolato tramite il campionamento del valore a intervalli di tempo discreti. La differenza tra due valori di campionamento successivi è uguale alla frequenza dell'intervallo di tempo utilizzato.|  
|**cntr_type**|**int**|Tipo di contatore definito dall'architettura di controllo delle prestazioni di Windows. Visualizzare [tipi di contatore delle prestazioni WMI](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-performance-counter-types) su documentazione o la documentazione di Windows Server per altre informazioni sui tipi di contatore delle prestazioni.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> L'identificatore per il nodo in questa distribuzione.|  
  
## <a name="remarks"></a>Note  
 Se l'istanza dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di visualizzare i contatori delle prestazioni del sistema operativo Windows, utilizzare la query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente per verificare se i contatori delle prestazioni sono stati disabilitati.  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 Se il valore restituito è di 0 righe, i contatori delle prestazioni sono stati disabilitati. È necessario quindi analizzare il log del programma di installazione e ricercare l'errore 3409 "Reinstallare sqlctr.ini e verificare che l'account di accesso dell'istanza disponga delle autorizzazioni di Registro di sistema appropriate".  Questo errore indica che i contatori delle prestazioni non sono stati abilitati. Gli errori immediatamente precedenti all'errore 3409 dovrebbero indicare la causa principale per l'errore relativo all'abilitazione dei contatori delle prestazioni. Per altre informazioni sui file di log di installazione, vedere [visualizzare e leggere i file Log di SQL Server Setup](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="permission"></a>Autorizzazioni

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] è richiesta l'autorizzazione `VIEW DATABASE STATE` per il database.   
 
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i valori dei contatori di prestazioni.  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


