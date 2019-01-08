---
title: IHpublisherconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 181cf4da50b315f67b124b7872be013eed3f4ef3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802193"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHpublisherconstraints** tabella di sistema contiene una riga per ogni vincolo replicato dal Server di pubblicazione non SQL usando il server di distribuzione corrente. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|Identificatore del vincolo pubblicato.|  
|**table_id**|**int**|Identifica la tabella dalla [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a cui appartiene il vincolo.|  
|**publisher_id**|**smallint**|Identifica la pubblicazione non SQL Server da cui la colonna viene pubblicata.|  
|**Name**|**sysname**|Nome del vincolo pubblicato.|  
|**Tipo**|**nvarchar(255)**|Tipo di vincolo supportato dal [IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md) tabella di sistema.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
