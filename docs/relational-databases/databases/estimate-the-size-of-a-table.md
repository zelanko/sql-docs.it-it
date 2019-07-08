---
title: Stimare le dimensioni di un tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8397cee022f51649c8a63efd853710184891a537
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585304"
---
# <a name="estimate-the-size-of-a-table"></a>Stima delle dimensioni di una tabella
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Per stimare la quantità di spazio necessario per archiviare dati in una tabella, è possibile utilizzare la procedura seguente:  
  
1.  Calcolare lo spazio necessario per l'heap o indice cluster seguendo le istruzioni in [Stima delle dimensioni di un heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md) o [Stima delle dimensioni di un indice cluster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcolare lo spazio necessario per ogni indice non cluster seguendo le istruzioni disponibili in [Stima delle dimensioni di un indice non cluster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Sommare i valori calcolati nei passaggi 1 e 2.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="see-also"></a>Vedere anche  
 [Stima delle dimensioni di un database](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Stima delle dimensioni di un heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Stima delle dimensioni di un indice cluster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Stima delle dimensioni di un indice non cluster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
