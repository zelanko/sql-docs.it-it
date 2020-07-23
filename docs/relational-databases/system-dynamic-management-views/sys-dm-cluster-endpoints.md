---
title: sys. dm_cluster_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe06d6b7c00fe60c44b19468f9ef0cc814d25e5d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913236"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm_cluster_endpoints (Transact-SQL)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome del servizio esposto esternamente in un cluster SQL Big Data. Identificatore univoco per l'endpoint. Chiave per questa visualizzazione. Non ammette i valori Null. |  
|description|`nvarchar(4000)`|Descrizione del servizio Non ammette i valori Null. |
|endpoint|`sysname`|URL dell'endpoint o attributo di connessione. Non ammette i valori Null. |
|protocol_desc|`sysname`|Descrizione del protocollo dell'endpoint |

## <a name="permissions"></a>Autorizzazioni

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.

## <a name="see-also"></a>Vedere anche

[Che cosa [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] sono ](../../big-data-cluster/big-data-cluster-overview.md)?
