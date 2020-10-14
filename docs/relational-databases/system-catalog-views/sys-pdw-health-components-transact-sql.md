---
description: sys.pdw_health_components (Transact-SQL)
title: sys.pdw_health_components (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 2b27f535bbe440e3ce09602b4c1098a33d3883f2
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034810"
---
# <a name="syspdw_health_components-transact-sql"></a>sys.pdw_health_components (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le informazioni su tutti i componenti e i dispositivi presenti nel sistema. Che includono hardware, dispositivi di archiviazione e dispositivi di rete.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificatore univoco di un componente o di un dispositivo.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|group_id|**Int**|Gruppo di componenti logici a cui appartiene il componente. Vedere [sys.pdw_health_components (data warehouse parallelo)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nome del componente.|NOT NULL|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
