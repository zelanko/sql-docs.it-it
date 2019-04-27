---
title: IHcolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5d05f2667b6f7196338b182f2b9cca1a84e7b6e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744176"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHcolumns** tabella di sistema contiene una riga per ogni colonna pubblicata. Questa tabella viene utilizzata per definire la modalità di rappresentazione quando pubblicato, i tipi di dati colonna dalla pubblicazione non SQL Server che esegue praticamente il mapping dei tipi di dati tra un sistemi di gestione database (DBMS) non SQL Server e SQL Server. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica una colonna pubblicata.|  
|**publishercolumn_id**|**int**|Associa i metadati della colonna archiviati in una colonna pubblicata la [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabella di sistema.|  
|**name**|**sysname**|Specifica il nome della colonna.|  
|**article_id**|**int**|Identifica l'articolo al quale appartiene la colonna.|  
|**column_ordinal**|**int**|Identifica la colonna in base all'ordine.|  
|**mapped_type**|**tinyint**|Tipo di dati della colonna di destinazione nel Sottoscrittore.|  
|**mapped_length**|**bigint**|Lunghezza della colonna nel Sottoscrittore.|  
|**mapped_prec**|**int**|Precisione della colonna nel Sottoscrittore.|  
|**mapped_scale**|**int**|Scala della colonna nel Sottoscrittore.|  
|**mapped_nullable**|**bit**|Indica se la colonna nel Sottoscrittore ammette valori NULL, dove **1** significa che i valori NULL vengono accettati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;System View&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
