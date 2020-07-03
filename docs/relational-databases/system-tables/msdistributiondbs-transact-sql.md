---
title: MSdistributiondbs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fde8c78cb37b84ae897e2b12bba6049da8ddc4fa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889957"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSdistributiondbs** contiene una riga per ogni database di distribuzione definito nel server di distribuzione locale. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del database di distribuzione.|  
|**min_distretention**|**int**|Periodo di memorizzazione minimo, espresso in ore, che deve trascorrere prima dell'eliminazione delle transazioni.|  
|**max_distretention**|**int**|Periodo di memorizzazione massimo, espresso in ore, trascorso il quale le transazioni vengono eliminate.|  
|**history_retention**|**int**|Numero di ore di memorizzazione della cronologia.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
