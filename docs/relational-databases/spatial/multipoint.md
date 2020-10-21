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
ms.openlocfilehash: 2a64b2d0e640a2c16fc04491e9db307fca82633a
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006291"
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
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
  
  
