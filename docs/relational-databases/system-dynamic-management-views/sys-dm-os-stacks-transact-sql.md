---
title: sys. dm_os_stacks (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2db6fb4245b98abe36ec4b2813fe6fbc366e7046
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824534"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Questa vista a gestione dinamica viene utilizzata internamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per:  
  
-   Tenere traccia dei dati di debug quali le allocazioni in sospeso.  
  
-   Utilizzare o convalidare la logica utilizzata dai componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dove il componente specifico presume che sia stata eseguita una determinata chiamata.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary (8)**|Indirizzo univoco per l'allocazione di stack. Non ammette i valori Null.|  
|**frame_index**|**int**|Ogni riga rappresenta una chiamata di funzione che, se ordinata in ordine crescente in base all'indice del frame per una particolare **stack_address**, restituisce lo stack di chiamate completo. Non ammette i valori Null.|  
|**frame_address**|**varbinary (8)**|Indirizzo della chiamata di funzione. Non ammette i valori Null.|  
  
## <a name="remarks"></a>Commenti  
 **sys. dm_os_stacks** richiede che i simboli del server e di altri componenti siano presenti nel server per visualizzare correttamente le informazioni.  
  
## <a name="permissions"></a>Autorizzazioni

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   


## <a name="see-also"></a>Vedere anche  
  [SQL Server viste a gestione dinamica relative al sistema operativo &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
