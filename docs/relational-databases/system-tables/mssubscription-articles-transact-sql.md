---
title: MSsubscription_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_articles
- MSsubscription_articles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_articles system table
ms.assetid: dbc1737f-261e-4017-b9cd-703b9fc4ac78
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36d6c5db3f675c570237a436557bbe6827af09e2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758553"
---
# <a name="mssubscriptionarticles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsubscription_articles** tabella contiene informazioni relative agli articoli in una sottoscrizione in coda. Questa tabella viene popolata solo per i tipi di replica ad aggiornamento in coda e ad aggiornamento immediato sostituito dall'aggiornamento in coda in caso di errore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente che gestisce l'articolo.|  
|**artid**|**int**|L'ID dell'articolo dal **sysarticles** tabella.|  
|**article**|**sysname**|Il nome dell'articolo dal **sysarticles** tabella.|  
|**dest_table**|**sysname**|Il nome della tabella di destinazione dal **sysarticles** tabella.|  
|**Proprietario**|**sysname**|Proprietario della sottoscrizione.|  
|**cft_table**|**sysname**|Nome della tabella dei conflitti dell'articolo per il tipo di replica ad aggiornamento in coda.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
