---
title: IHpublishercolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f965bb76f13c01531ba5007d82de9e42c8138f05
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802493"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHpublishercolumns** tabella di sistema rappresenta i metadati archiviati nel server di pubblicazione. Questa tabella contiene una riga per ogni colonna replicata da Server di pubblicazione non SQL usando il server di distribuzione corrente. Le informazioni nel tipo di dati **IHpublishercolumns** è specifico per il sistema non SQL Server di gestione database (DBMS) da cui i dati vengono pubblicati. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica una colonna pubblicata.|  
|**table_id**|**int**|Identifica la tabella di origine [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a cui appartiene la colonna.|  
|**publisher_id**|**smallint**|Identifica la pubblicazione non SQL Server da cui la colonna viene pubblicata.|  
|**name**|**sysname**|Nome della colonna pubblicata.|  
|**column_ordinal**|**int**|Identifica la colonna in base all'ordine.|  
|**type**|**varchar(255)**|Tipo di dati della colonna di origine nel server di pubblicazione.|  
|**length**|**bigint**|Lunghezza della colonna di origine nel server di pubblicazione.|  
|**Prec**|**int**|Precisione della colonna di origine nel server di pubblicazione.|  
|**scala**|**int**|Scala della colonna di origine nel server di pubblicazione.|  
|**IsNullable**|**bit**|Indica se la colonna accetta valori NULL, dove **1** significa che i valori NULL vengono accettati.|  
|**iscaptured**|**bit**|Indica se esiste un trigger nella colonna. Il trigger potrebbe esistere anche se la colonna non è pubblicata in un articolo. Un valore pari **1** significa che il trigger esiste nella colonna.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;vista di sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
