---
title: sys. pdw_health_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83bea79a009e25d54f9d0ae589936de7fed7d94a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396036"
---
# <a name="syspdw_health_components-transact-sql"></a>sys. pdw_health_components (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le informazioni su tutti i componenti e i dispositivi presenti nel sistema. Che includono hardware, dispositivi di archiviazione e dispositivi di rete.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificatore univoco di un componente o di un dispositivo.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|group_id|**Int**|Gruppo di componenti logici a cui appartiene il componente. Vedere [sys. pdw_health_components (data warehouse parallelo)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nome del componente.|NOT NULL|  
  
## <a name="see-also"></a>Vedi anche  
 [Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
