---
title: sys. dm_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8eeeaaf59934d6c3307641b6c93f110ab5738f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982536"
---
# <a name="sysdm_os_threads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce un elenco di tutti i thread del sistema operativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Per chiamare questo oggetto [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] da [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]o, usare il nome **sys. dm_pdw_nodes_os_threads**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary (8)**|Indirizzo di memoria (chiave primaria) del thread.|  
|started_by_sqlservr|**bit**|Indica l'initiator del thread.<br /><br /> 1 = Il thread è stato avviato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Il thread è stato avviato da un altro componente, ad esempio una stored procedure estesa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**int**|ID del thread assegnato dal sistema operativo.|  
|status|**int**|Flag di stato interno.|  
|instruction_address|**varbinary (8)**|Indirizzo dell'istruzione attualmente in esecuzione.|  
|creation_time|**datetime**|Ora di creazione del thread.|  
|kernel_time|**bigint**|Quantità di tempo del kernel utilizzato dal thread.|  
|usermode_time|**bigint**|Quantità di tempo utente utilizzato dal thread.|  
|stack_base_address|**varbinary (8)**|Indirizzo di memoria dell'indirizzo dello stack più alto per il thread.|  
|stack_end_address|**varbinary (8)**|Indirizzo di memoria dell'indirizzo dello stack più basso per il thread.|  
|stack_bytes_committed|**int**|Numero di byte di cui è stato eseguito il commit nello stack.|  
|stack_bytes_used|**int**|Numero di byte attivamente utilizzati nel thread.|  
|affinity|**bigint**|Maschera della CPU nella quale il thread è in esecuzione. Dipende dal valore configurato dall'istruzione **ALTER Server Configuration set process Affinity** . Potrebbe essere diverso dall'utilità di pianificazione in caso di affinità soft.|  
|Priorità|**int**|Valore di priorità del thread.|  
|Impostazioni locali|**int**|Identificatore delle impostazioni locali (LCID) nella cache per il thread.|  
|token|**varbinary (8)**|Handle del token di rappresentazione nella cache per il thread.|  
|is_impersonating|**int**|Indica se il thread utilizza la rappresentazione Win32.<br /><br /> 1 = Il thread utilizza credenziali di sicurezza diverse da quelle predefinite del processo. Ciò indica che il thread rappresenta un'entità diversa da quella che ha creato il processo.|  
|is_waiting_on_loader_lock|**int**|Stato del sistema operativo indicante se il thread è in attesa di un blocco del caricatore.|  
|fiber_data|**varbinary (8)**|Fiber Win32 corrente in esecuzione nel thread. È applicabile solo in caso di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il lightweight pooling.|  
|thread_handle|**varbinary (8)**|Solo per uso interno.|  
|event_handle|**varbinary (8)**|Solo per uso interno.|  
|scheduler_address|**varbinary (8)**|Indirizzo di memoria dell'utilità di pianificazione associata al thread. Per ulteriori informazioni, vedere [sys. dm_os_schedulers &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary (8)**|Indirizzo di memoria del thread di lavoro associato al thread. Per ulteriori informazioni, vedere [sys. dm_os_workers &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary (8)**|Indirizzo del contesto interno del fiber. È applicabile solo in caso di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il lightweight pooling.|  
|self_address|**varbinary (8)**|Puntatore di consistenza interno.|  
|processor_group|**smallint**|**Si applica a**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e versioni successive.<br /><br /> ID del gruppo di processori.|  
|pdw_node_id|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="permissions"></a>Autorizzazioni

In [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]è richiesta `VIEW SERVER STATE` l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   

## <a name="notes-on-linux-version"></a>Note sulla versione di Linux

Poiché il motore SQL funziona in Linux, alcune di queste informazioni non corrispondono ai dati di diagnostica di Linux. Ad esempio, `os_thread_id` non corrisponde al risultato di strumenti quali `ps``top` o procfs (/proc/`pid`).  A causa del livello di astrazione della piattaforma (SQLPAL), un livello tra SQL Server componenti e il sistema operativo.

## <a name="examples"></a>Esempi  
 All'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono avviati dei thread a cui vengono associati thread di lavoro. Componenti esterni, ad esempio una stored procedure estesa, possono tuttavia avviare thread nel processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di controllo su questi thread. sys. dm_os_threads è in grado di fornire informazioni sui thread non autorizzati che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzano risorse nel processo.  
  
 La query seguente consente di individuare i thread di lavoro che eseguono thread non avviati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], con il tempo utilizzato per l'esecuzione.  
  
> [!NOTE]
>  A scopo di brevità, nell'istruzione `*` della query seguente viene utilizzato un asterisco (`SELECT`). È consigliabile evitare di utilizzare l'asterisco (*), in particolare per viste del catalogo, viste a gestione dinamica e funzioni di sistema con valori di tabella. Gli aggiornamenti e le versioni [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] future di possono aggiungere colonne e modificare l'ordine delle colonne in queste viste e funzioni. Queste modifiche potrebbero causare malfunzionamenti nelle applicazioni che prevedono un ordine e un numero di colonne specifici.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Vedere anche  
  [sys. dm_os_workers &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [SQL Server viste a gestione dinamica relative al sistema operativo &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


