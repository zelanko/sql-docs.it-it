---
description: MStracer_history (Transact-SQL)
title: MStracer_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a3a8c4c03359209108ff839e2a5708ef2da248de
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545471"
---
# <a name="mstracer_history-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MStracer_history** mantiene un record di tutti i token di traccia ricevuti nel Sottoscrittore. Questa tabella è archiviata nel database di distribuzione e viene utilizzata dalla replica per il monitoraggio delle prestazioni.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|Identifica in modo univoco un token di traccia.|  
|**agent_id**|**int**|Identifica l'agente che ha gestito il record del token di traccia.|  
|**subscriber_commit**|**datetime**|Data e ora del commit del record del token di traccia nel Sottoscrittore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
