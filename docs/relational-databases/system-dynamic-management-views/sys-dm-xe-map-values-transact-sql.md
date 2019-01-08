---
title: DM xe_map_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_map_values
- dm_xe_map_values
- dm_xe_map_values_TSQL
- sys.dm_xe_map_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_map_values dynamic management view
- xe
ms.assetid: c0c5dd7e-9cee-47e2-b65a-88194c00aa1f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d554a7269b8f10f8d2d44a48bc401e866f3dce8
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785772"
---
# <a name="sysdmxemapvalues-transact-sql"></a>sys.dm_xe_map_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un mapping di chiavi numeriche interne in un testo leggibile.  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar(256)**|Nome della mappa. nome è univoco nel sistema locale. Non ammette i valori Null.|  
|object_package_guid|**uniqueidentifier**|GUID del pacchetto che contiene la mappa. Non ammette i valori Null.|  
|map_key|**int**|Valore della chiave interna. Non ammette i valori Null.|  
|map_value|**nvarchar(3072)**|Descrizione del valore della chiave. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|Per|Relazione|  
|----------|--------|------------------|  
|dm_xe_map_values.object_package_guid<br /><br /> dm_xe_map_values.name|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|Molti-a-uno| 
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

