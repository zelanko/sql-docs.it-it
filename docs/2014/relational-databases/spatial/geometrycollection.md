---
title: GeometryCollection | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5aceabe5a263cfa53572be6f818ddc905f9742a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014226"
---
# <a name="geometrycollection"></a>GeometryCollection
  `GeometryCollection` è una raccolta di zero o più istanze `geometry` o `geography`. `GeometryCollection` può essere vuoto.  
  
## <a name="geometrycollection-instances"></a>Istanze GeometryCollection  
  
### <a name="accepted-instances"></a>Istanze accettate  
 Per poter essere accettata, un'istanza `GeometryCollection` deve essere un'istanza `GeometryCollection` vuota oppure tutte le istanze che comprendono l'istanza `GeometryCollection` devono essere istanze accettate. Nell'esempio seguente vengono illustrate le istanze accettate.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 Nell'esempio seguente viene generata un'eccezione `System.FormatException`, poiché l'istanza `LinesString` nell'istanza `GeometryCollection` non è accettata.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
 Un'istanza `GeometryCollection` è valida se tutte le istanze che comprendono l'istanza `GeometryCollection` sono valide. Nell'esempio seguente vengono indicate tre istanze `GeometryCollection` valide e un'istanza non valida.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` non è valida, poiché l'istanza `Polygon` nell'istanza `GeometryCollection` non è valida.  
  
 Per altre informazioni sulle istanze accettate e valide, vedere [Point](point.md), [MultiPoint](multipoint.md), [LineString](linestring.md), [MultiLineString](multilinestring.md), [Polygon](polygon.md)e [MultiPolygon](multipolygon.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza di un `geometry``GeometryCollection` con i valori Z in SRID 1 in cui sono incluse le istanze `Point` e `Polygon` .  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
