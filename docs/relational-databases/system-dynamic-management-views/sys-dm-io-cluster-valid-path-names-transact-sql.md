---
description: sys.dm_io_cluster_valid_path_names (Transact-SQL)
title: sys. dm_io_cluster_valid_path_names (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs:
- TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0f81bd26a6ec2a43e9f063466bfa77c793ac4d8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419655"
---
# <a name="sysdm_io_cluster_valid_path_names-transact-sql"></a>sys.dm_io_cluster_valid_path_names (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni su tutti i dischi condivisi validi, inclusi i volumi condivisi cluster, per un'istanza del cluster di failover di SQL Server. Se l'istanza non è in cluster, viene restituito un set di righe vuoto.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**path_name**|**Nvarchar (512)**|Punto di montaggio del volume o percorso dell'unità che può essere utilizzato come directory radice per i file di log e di database. Non ammette i valori Null.|  
|**cluster_owner_node**|**Nvarchar (64)**|Proprietario corrente dell'unità. Per i volumi condivisi cluster il proprietario è il nodo che ospita il server di metadati. Non ammette i valori Null.|  
|**is_cluster_shared_volume**|**Po'**|Restituisce 1 se l'unità in cui si trova questo percorso è un volume condiviso cluster; in caso contrario, restituisce 0.|  
  
## <a name="remarks"></a>Osservazioni  
 Un'istanza del cluster di failover di SQL Server deve utilizzare l'archiviazione condivisa tra tutti i nodi dell'istanza del cluster di failover per l'archiviazione dei file di dati e di log. I dischi inclusi in questa vista sono quelli presenti nel gruppo di risorse del cluster associato all'istanza e sono gli unici dischi che possono essere utilizzati per l'archiviazione dei file di dati o di log.  
  
> [!NOTE]  
>  Questa vista sostituirà [sys. dm_io_cluster_shared_drives &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md) in una versione futura.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'utente deve disporre dell'autorizzazione VIEW SERVER STATE per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata la vista sys.dm_io_cluster_valid_path_names per determinare le unità condivise in un'istanza del server di cluster:  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys. dm_os_cluster_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys. dm_io_cluster_shared_drives &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

