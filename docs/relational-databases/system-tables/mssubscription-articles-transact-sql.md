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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 30488b669265b66036b591191e8e528e1ef74b35
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757759"
---
# <a name="mssubscription_articles-transact-sql"></a>MSsubscription_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSsubscription_articles** contiene informazioni relative agli articoli di una sottoscrizione in coda. Questa tabella viene popolata solo per i tipi di replica ad aggiornamento in coda e ad aggiornamento immediato sostituito dall'aggiornamento in coda in caso di errore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente che gestisce l'articolo.|  
|**artid**|**int**|ID articolo della tabella **sysarticles** .|  
|**articolo**|**sysname**|Nome dell'articolo della tabella **sysarticles** .|  
|**dest_table**|**sysname**|Nome della tabella di destinazione dalla tabella **sysarticles** .|  
|**proprietario**|**sysname**|Proprietario della sottoscrizione.|  
|**cft_table**|**sysname**|Nome della tabella dei conflitti dell'articolo per il tipo di replica ad aggiornamento in coda.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
