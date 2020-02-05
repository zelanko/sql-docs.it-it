---
title: STSymDifference (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ea26c364621910d6dd5148a5753bd6709d3e0f07
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066282"
---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Restituisce un oggetto che rappresenta tutti i punti che si trovano in un'istanza **geometry** o un'altra istanza **geometry**, ma non i punti che si trovano in entrambe le istanze.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geometry*  
 Altra istanza **geometry** oltre all'istanza sulla quale viene chiamato `STSymDistance()`.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo restituisce sempre Null se gli identificatori SRID delle istanze **geometry** non corrispondono. Il risultato può contenere segmenti di arco circolare solo se le istanze di input contengono segmenti di arco circolare.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>R. Calcolo della differenza simmetrica di due istanze Polygon  
 Nell'esempio seguente viene utilizzato `STSymDifference()` per calcolare la differenza simmetrica tra due istanze `Polygon`.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. Calcolo della differenza simmetrica tra un'istanza CurvePolygon e un'istanza Polygon  
 Nell'esempio seguente viene restituito `GeometryCollection` che rappresenta la differenza simmetrica tra `CurvePolygon` e `Polygon`.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. Utilizzo di STSymDifference() in un'istanza CurvePolygon con un'istanza Polygon inscritta  
 Nell'esempio seguente viene restituita un'istanza `CurvePolygon` con un anello `Polygon` interno che rappresenta la differenza simmetrica tra le due istanze confrontate.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
