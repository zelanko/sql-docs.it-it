---
description: MSreplication_options (Transact-SQL)
title: MSreplication_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 44099921a382ca05f0e2e379b2df9d97e1c28f6e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460343"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSreplication_options** archivia i metadati utilizzati internamente dalla replica. Questa tabella è archiviata nel database **Master** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Solo per uso interno.|  
|**value**|**bit**|Solo per uso interno.|  
|**major_version**|**int**|Solo per uso interno.|  
|**minor_version**|**int**|Solo per uso interno.|  
|**Revisione**|**int**|Solo per uso interno.|  
|**install_failures**|**int**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
