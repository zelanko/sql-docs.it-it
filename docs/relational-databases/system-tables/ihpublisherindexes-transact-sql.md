---
title: IHpublisherindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a24126ef3226878b4d07a056573f3b60e94495c3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802513"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHpublisherindexes** tabella di sistema contiene una riga per ogni indice replicato dal Server di pubblicazione non SQL usando il server di distribuzione corrente. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|Identificatore dell'indice pubblicato.|  
|**table_id**|**int**|Identifica la tabella dalla [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a cui appartiene l'indice.|  
|**publisher_id**|**smallint**|Identifica la pubblicazione non SQL Server da cui l'indice viene pubblicato.|  
|**name**|**sysname**|Nome dell'indice pubblicato.|  
|**type**|**nvarchar(255)**|Un tipo di indice supportati dal [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) tabella di sistema.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
