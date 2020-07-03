---
title: MStracer_tokens (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0822c2de02de9ef0a420f0066d058fad200b4a88
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881468"
---
# <a name="mstracer_tokens-transact-sql"></a>MStracer_tokens (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Nella tabella **MStracer_tokens** viene mantenuto un record dei record del token di traccia inseriti in una pubblicazione. Questa tabella è archiviata nel database di distribuzione e viene utilizzata dalla replica per il monitoraggio delle prestazioni.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|Identifica un record di token di traccia.|  
|**publication_id**|**int**|Identifica la pubblicazione in cui il record di token di traccia è stato inserito.|  
|**publisher_commit**|**datetime**|Data e ora del commit del record di token di traccia nel server di pubblicazione.|  
|**distributor_commit**|**datetime**|Data e ora del commit del record di token di traccia nel server di distribuzione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
