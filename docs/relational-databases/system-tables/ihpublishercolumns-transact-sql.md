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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1de331740a0c67642de314155bfdd4ee53ef8f3f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773795"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  La tabella di sistema **IHpublishercolumns** rappresenta i metadati archiviati nel server di pubblicazione. Contiene una riga per ogni colonna replicata da server di pubblicazione non SQL Server tramite il server di distribuzione corrente. Le informazioni sul tipo di dati in **IHpublishercolumns** sono specifiche del sistema di gestione di database (DBMS) non SQL Server da cui vengono pubblicati i dati. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica una colonna pubblicata.|  
|**table_id**|**int**|Identifica la tabella di origine da [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a cui appartiene la colonna.|  
|**publisher_id**|**smallint**|Identifica il server di pubblicazione non SQL Server da cui viene pubblicata la colonna.|  
|**nome**|**sysname**|Nome della colonna pubblicata.|  
|**column_ordinal**|**int**|Identifica la colonna in base all'ordine.|  
|**type**|**varchar(255)**|Tipo di dati della colonna di origine nel server di pubblicazione.|  
|**length**|**bigint**|Lunghezza della colonna di origine nel server di pubblicazione.|  
|**prec**|**int**|Precisione della colonna di origine nel server di pubblicazione.|  
|**scale**|**int**|Scala della colonna di origine nel server di pubblicazione.|  
|**IsNullable**|**bit**|Indica se la colonna accetta valori NULL, dove **1** indica che i valori null sono accettati.|  
|**iscaptured**|**bit**|Indica se esiste un trigger nella colonna. Il trigger potrebbe esistere anche se la colonna non è pubblicata in un articolo. Il valore **1** indica che il trigger esiste nella colonna.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste di replica &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;vista di sistema&#41; &#40;&#41;Transact-SQL](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;&#41;Transact-SQL](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
