---
title: STUnion (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUnion (geometry Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion (geometry Data Type)
ms.assetid: 5b168118-137d-402f-9173-fee3f365a89c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 868b344a18494e4b92cd3ee5944cb80ad15ab845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066223"
---
# <a name="stunion-geometry-data-type"></a>STUnion (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Restituisce un oggetto che rappresenta l'unione di un'istanza **geometry** con un'altra istanza **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STUnion ( other_geometry )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geometry*  
 Altra istanza **geometry** per formare un'unione con l'istanza sulla quale viene chiamato `STUnion()`.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Questo metodo restituisce sempre Null se gli identificatori SRID delle istanze **geometry** non corrispondono. Il risultato può contenere segmenti di arco circolare solo se le istanze di input contengono segmenti di arco circolare.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-computing-the-union-of-two-polygon-instances"></a>A. Calcolo dell'unione di due istanze Polygon  
 Nell'esempio seguente viene utilizzato `STUnion()` per calcolare l'unione di due istanze `Polygon`.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-computing-the-union-of-a-polygon-instance-with-a-curvepolygon-instance"></a>B. Calcolo dell'unione di un'istanza Polygon e un'istanza CurvePolygon  
 Nell'esempio seguente viene restituita un'istanza `GeometryCollection` che contiene un segmento di arco circolare.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON((5 -1, 5 -3, 7 -3, 7 -1, 5 -1))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
 `STUnion()` restituisce un risultato che contiene un segmento di arco circolare perché l'istanza che ha richiamato `STUnion()` contiene un segmento di arco circolare.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

