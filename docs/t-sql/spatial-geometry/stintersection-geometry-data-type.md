---
description: STIntersection (tipo di dati geometry)
title: STIntersection (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6365d94822d8d291951de3e59c7c71fbed487163
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479253"
---
# <a name="stintersection-geometry-data-type"></a>STIntersection (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un oggetto che rappresenta i punti in cui un'istanza **geometry** interseca un'altra istanza **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *other_geometry*  
 Altra istanza **geometry** da confrontare con l'istanza sulla quale viene chiamato `STIntersection()` per determinare il punto di intersezione.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Commenti  
 `STIntersection()` restituisce sempre Null se gli identificatori SRID delle istanze **geometry** non corrispondono. Il risultato può contenere segmenti di arco circolare solo se le istanze di input ne contengono.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>R. Utilizzo di STIntersection() in istanze Polygon  
 Nell'esempio seguente viene utilizzato `STIntersection()` per calcolare l'intersezione di due poligoni.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. Utilizzo di STIntersection() con istanze CurvePolygon  
 Nell'esempio seguente viene restituita un'istanza che contiene un segmento di arco circolare.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STIntersection(@g).ToString();
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

