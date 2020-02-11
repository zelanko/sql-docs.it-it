---
title: Viste dell'agente di raccolta dati (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- data collector [SQL Server], views
ms.assetid: a005e885-7813-4c7e-b332-b01d9e9d4054
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9e412f796a5b04f980557b5a3131763811aa78da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68033175"
---
# <a name="data-collector-views-transact-sql"></a>Viste dell'agente di raccolta dati (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'agente di raccolta dati offre le viste seguenti per la visualizzazione di informazioni sulla propria configurazione, ad esempio le proprietà del tipo di agente di raccolta, i set di raccolta e gli elementi dei set di raccolta, nonché le statistiche di esecuzione ottenute quando un set di raccolta è in esecuzione. Queste viste, che si trovano nel database **msdb** , forniscono anche un livello di astrazione per le tabelle sottostanti. Tale astrazione consente di migliorare la sicurezza, impedendo l'accesso diretto alle tabelle e consentendo le modifiche alle tabelle senza influire sulle applicazioni associate.  
  
|||  
|-|-|  
|[syscollector_collection_items &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|[syscollector_collection_sets &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|  
|[syscollector_collector_types &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|[syscollector_config_store &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|  
|[syscollector_execution_log &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|[syscollector_execution_log_full &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|  
|[syscollector_execution_stats &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
