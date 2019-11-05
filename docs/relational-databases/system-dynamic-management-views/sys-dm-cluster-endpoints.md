---
title: sys. dm _cluster_endpoints (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 05076a6b694ff5861c5a7862b1f8f913ddb67fd6
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536175"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm _cluster_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nome del servizio esposto esternamente in un cluster SQL Big Data. Identificatore univoco per l'endpoint. Chiave per questa visualizzazione. Non ammette i valori Null. |  
|description|`nvarchar(4000)`|Descrizione del servizio. Non ammette i valori Null. |
|endpoint|`sysname`|URL dell'endpoint o attributo di connessione. Non ammette i valori Null. |
|protocol_desc|`sysname`|Descrizione del protocollo dell'endpoint |

## <a name="permissions"></a>Autorizzazioni

Per [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è richiesta l'autorizzazione `VIEW SERVER STATE`.

## <a name="see-also"></a>Vedere anche

Che cosa sono [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)](.. /.. /big-data-cluster/big-data-cluster-overview.md)?
