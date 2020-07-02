---
title: sys. dm_tran_commit_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 863da6499e788b07576066a1890c4532f3a06456
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720377"
---
# <a name="change-tracking---sysdm_tran_commit_table"></a>Rilevamento modifiche-sys. dm_tran_commit_table
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Visualizza una riga per ogni transazione di cui viene eseguito il commit per una tabella rilevata mediante il rilevamento delle modifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La vista di gestione sys.dm_tran_commit_table, fornita per scopi di supporto, espone le informazioni correlate alla transazione archiviate tramite il rilevamento delle modifiche nella tabella di sistema sys.syscommittab. La tabella sys.syscommittab fornisce un efficiente mapping persistente da un ID di transazione specifico del database al numero di sequenza del file di log (LSN) del commit della transazione e al timestamp del commit. I dati archiviati nella tabella sys.syscommittab ed esposti in questa vista di gestione sono soggetti al processo di pulizia in base al periodo di memorizzazione specificato durante la configurazione del rilevamento delle modifiche.  
  
> [!NOTE]  
>  Per chiamare questo [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oggetto da o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , usare il nome **sys. dm_pdw_nodes_tran_commit_table**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|Numero a incremento progressivo costante che funge da timestamp specifico del database per ogni transazione di cui viene eseguito il commit.|  
|xdes_id|**bigint**|ID interno specifico del database per la transazione.|  
|commit_lbn|**bigint**|Numero del blocco del log contenente il record del log del commit per la transazione.|  
|commit_csn|**bigint**|Numero di sequenza del commit specifico dell'istanza per la transazione.|  
|commit_time|**smalldatetime**|Ora in cui è stato eseguito il commit della transazione.|  
|pdw_node_id|**int**|**Si applica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificatore del nodo su cui si trova questa distribuzione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQL](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Informazioni sul rilevamento delle modifiche &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


