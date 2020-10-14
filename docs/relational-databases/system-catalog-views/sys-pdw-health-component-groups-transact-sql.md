---
description: sys.pdw_health_component_groups (Transact-SQL)
title: sys.pdw_health_component_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8ac09a94a4821713bd1ef3cb2c852251d9b811c9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036783"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys.pdw_health_component_groups (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le informazioni sui raggruppamenti logici di componenti e dispositivi.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|Identificatore univoco per i componenti e i dispositivi.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|group_name|**nvarchar(255)**|Nome del gruppo logico per i componenti e i dispositivi.|NOT NULL|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
