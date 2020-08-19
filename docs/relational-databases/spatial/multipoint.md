---
description: MultiPoint
title: MultiPoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f149e930c29be9a94ed6eee60efadd1a4f91d8d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88403298"
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
   Un **MultiPoint** è una raccolta di zero o più punti. Il limite di un'istanza **MultiPoint** è vuoto.  
  
## <a name="examples"></a>Esempi  

### <a name="example-a"></a>Esempio A.
Nell'esempio seguente è creata un'istanza `geometry MultiPoint` con SRID 23 e due punti: uno con le coordinate (2, 3), e l'altro con le coordinate (7, 8) e un valore Z di 9,5.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-b"></a>Esempio B. 
Nell'esempio seguente viene espressa l'istanza `MultiPoint` usando `STMPointFromText()`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-c"></a>Esempio C.
Nell'esempio seguente viene utilizzato il metodo `STGeometryN()` per recuperare una descrizione del primo punto nella raccolta.  
  
```sql  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Punto](../../relational-databases/spatial/point.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
