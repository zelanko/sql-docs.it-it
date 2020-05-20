---
title: sys. dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0efa4a5b5c8144807c27014a96b3fa90ed77971
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811756"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sulla coda di attesa relativa alle attività che sono in attesa di una risorsa. Per ulteriori informazioni sulle attività, vedere la [Guida all'architettura dei thread e delle attività](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
>  Per chiamare questo [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oggetto da o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , usare il nome **sys. dm_pdw_nodes_os_waiting_tasks**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary (8)**|Indirizzo dell'attività in attesa.|  
|**session_id**|**smallint**|ID della sessione associata all'attività.|  
|**exec_context_id**|**int**|ID del contesto di esecuzione associato all'attività.|  
|**wait_duration_ms**|**bigint**|Tempo totale di attesa per questo tipo di attesa, in millisecondi. Questa volta è incluso **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nome del tipo di attesa.|  
|**resource_address**|**varbinary (8)**|Indirizzo della risorsa attesa dall'attività.|  
|**blocking_task_address**|**varbinary (8)**|Attività che mantiene bloccata la risorsa.|  
|**blocking_session_id**|**smallint**|ID della sessione che sta bloccando la richiesta. Se questa colonna è NULL, la richiesta non è bloccata oppure non sono disponibili o identificabili informazioni di sessione per la sessione da cui è bloccata.<br /><br /> -2 = La risorsa di blocco appartiene a una transazione distribuita orfana.<br /><br /> -3 = La risorsa di blocco appartiene a una transazione di recupero posticipata.<br /><br /> -4 = Non è possibile determinare l'ID di sessione del proprietario del latch di blocco a causa di transizioni nello stato del latch interno.|  
|**blocking_exec_context_id**|**int**|ID del contesto di esecuzione dell'attività di blocco.|  
|**resource_description**|**nvarchar (3072)**|Descrizione della risorsa attualmente occupata. Per ulteriori informazioni, vedere l'elenco riportato di seguito.|  
|**pdw_node_id**|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="resource_description-column"></a>Colonna resource_description  
 La colonna resource_description dispone dei valori possibili seguenti.  
  
 **Proprietario risorsa pool di thread:**  
  
-   ID ThreadPool = \< indirizzo esadecimale dell'utilità di pianificazione>  
  
 **Proprietario risorsa query parallela:**  
  
-   ID exchangeEvent = {Port | Pipe} \< Hex-address> WaitType = \< Exchange-Wait-Type> NodeId = \< Exchange-node-ID>  
  
 **Tipo di attesa Exchange**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Proprietario risorsa di blocco:**  
  
-   \<type-specific-Description> ID = lock \< Lock-Hex-address> Mode = \< mode> associatedObjectId = \< Associated-obj-ID>  
  
     **\<type-specific-Description> può essere:**  
  
    -   Per DATABASE: databaselock subresource = \< databaselock-subresource> dbid = \< DB-ID>  
  
    -   Per FILE: filelock fileid = \< file-id> subresource = \< filelock-subresource> dbid = \< db-ID>  
  
    -   Per OBJECT: objectlock lockPartition = \< Lock-Partition-id> objid = \< obj-ID> subresource = \< objectlock-subresource> dbid = \< DB-ID>  
  
    -   Per la pagina: PageLock fileid = \< file-id> pageid = \< Page-ID> dbid = \< db-ID> subresource = \< pagelock-subresource>  
  
    -   Per Key: Key Lock hobtid = \< HoBT-id> dbid = \< DB-ID>  
  
    -   Per EXTENT: extentlock fileid = \< file-id> pageid = \< Page-ID> dbid = \< db-ID>  
  
    -   Per RID: ridlock fileid = \< file-id> pageid = \< Page-ID> dbid = \< db-ID>  
  
    -   Per l'applicazione: applicationlock hash = \< hash> databasePrincipalId = \< Role-ID> dbid = \< db-ID>  
  
    -   Per METADATA: metadatalock subresource = \< Metadata-subresource> ClassID = \< metadatalock-Description> dbid = \< db-ID>  
  
    -   Per HOBT: hobtlock hobtid = \< HoBT-id> subresource = \< HoBT-subresource> dbid = \< db-ID>  
  
    -   Per ALLOCATION_UNIT: allocunitlock hobtid = \< HoBT-id> subresource = \< Alloc-Unit-subresource> dbid = \< db-ID>  
  
     **\<la modalità> può essere:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Proprietario risorsa esterna:**  
  
-   External ExternalResource = \< wait-type>  
  
 **Proprietario risorsa generica:**  
  
-   Area di lavoro TransactionMutex TransactionInfo = \< ID area di lavoro>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Proprietario risorsa latch:**  
  
-   \<DB-ID>: \< file-id>: \< pagina nel file>  
  
-   \<> GUID  
  
-   \<> della classe latch ( \< Indirizzo latch>)  
  
## <a name="permissions"></a>Autorizzazioni

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   
 
## <a name="example"></a>Esempio
In questo esempio vengono identificate le sessioni bloccate. Eseguire la [!INCLUDE[tsql](../../includes/tsql-md.md)] query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Vedere anche  
[SQL Server viste a gestione dinamica relative al sistema operativo &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[Guida all'architettura di thread e attività](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
