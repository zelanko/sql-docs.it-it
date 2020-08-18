---
description: sys. pdw_health_components (Transact-SQL)
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
ms.openlocfilehash: 74b741d94d5e9a10c4b657cfbe70ad69f9cbbfa1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400767"
---
# <a name="syspdw_health_components-transact-sql"></a>sys. pdw_health_components (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le informazioni su tutti i componenti e i dispositivi presenti nel sistema. Che includono hardware, dispositivi di archiviazione e dispositivi di rete.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|Identificatore univoco di un componente o di un dispositivo.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|group_id|**Int**|Gruppo di componenti logici a cui appartiene il componente. Vedere [sys. pdw_health_components (data warehouse parallelo)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|component_name|**nvarchar(255)**|Nome del componente.|NOT NULL|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
