---
title: IHpublishercolumnindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6dfe2075f983d59b0ef4edecf242a5faadc5821
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990281"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHpublishercolumnindexes** tabella di sistema esegue il mapping di colonne di una pubblicazione non SQL Server nel [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) agli indici della tabella di sistema di [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)tabella di sistema. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica la colonna dalla [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) con l'indice associato.|  
|**publisherindex_id**|**int**|Identifica un indice dal [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) tabella associata alla colonna.|  
|**indid**|**int**|Indica la posizione della colonna nella tabella pubblicata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
