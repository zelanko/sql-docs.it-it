---
title: IHconstrainttypes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHconstrainttypes_TSQL
- IHconstrainttypes
dev_langs:
- TSQL
helpviewer_keywords:
- IHconstrainttypes system table
ms.assetid: 955d6fa9-0b31-4335-a3cd-e4c4d90ad308
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: efb9a64b6c6b875430cea7fcd5bb834f64bb413c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890318"
---
# <a name="ihconstrainttypes-transact-sql"></a>IHconstrainttypes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella di sistema **IHconstrainttypes** contiene una riga per ogni tipo di vincolo non SQL Server supportato per i publisher non SQL Server. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**type**|**nvarchar(255)**|Nome di un tipo di vincolo non SQL Server supportato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
