---
title: IHpublishercolumnconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7f6c4b609159d34c1159a248c8ea9a9eacc24d18
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813525"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella di sistema **IHpublishercolumnconstraints** esegue il mapping delle colonne di una pubblicazione non SQL Server nella tabella di sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) ai vincoli nella tabella di sistema [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) . Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica la colonna da [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) con un vincolo associato.|  
|**publisherconstraint_id**|**int**|Identifica un vincolo da [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) associato alla colonna.|  
|**indid**|**int**|Indica la posizione della colonna nella tabella pubblicata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
