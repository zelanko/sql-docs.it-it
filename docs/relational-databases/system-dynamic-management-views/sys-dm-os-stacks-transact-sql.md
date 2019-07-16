---
title: sys.dm_os_stacks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c31bf39c4f133aa6f693614845cb54a5cf2bfc6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899762"
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Questa vista a gestione dinamica viene utilizzata internamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per:  
  
-   Tenere traccia dei dati di debug quali le allocazioni in sospeso.  
  
-   Utilizzare o convalidare la logica utilizzata dai componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dove il componente specifico presume che sia stata eseguita una determinata chiamata.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|Indirizzo univoco per l'allocazione di stack. Non ammette i valori Null.|  
|**frame_index**|**int**|Ogni riga rappresenta una funzione chiamata che, quando ordinato in ordine crescente in base all'indice di frame per un determinato **stack_address**, restituisce lo stack di chiamate completo. Non ammette i valori Null.|  
|**frame_address**|**varbinary(8)**|Indirizzo della chiamata di funzione. Non ammette i valori Null.|  
  
## <a name="remarks"></a>Note  
 **os_stacks** richiede che i simboli del server e altri componenti sia presente nel server per visualizzare le informazioni in modo corretto.  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] è richiesta l'autorizzazione `VIEW DATABASE STATE` per il database.   


## <a name="see-also"></a>Vedere anche  
  [Viste a gestione dinamica relative al sistema di operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
