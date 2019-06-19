---
title: STCrosses (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7588d3a335785dd80a5b41cd17734b207852faae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65939044"
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Restituisce 1 se un'istanza **geometry** incrocia un'altra istanza **geometry**. In caso contrario, restituisce 0.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geometry*  
 Altra istanza **geometry** da confrontare con l'istanza sulla quale viene chiamato `STCrosses()`.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Due istanze **geometry** si incrociano se si verificano entrambe le condizioni seguenti:  
  
-   L'intersezione delle due istanze **geometry** restituisce una geometria le cui dimensioni sono minori delle dimensioni massime delle istanze **geometry** di origine.  
  
-   Il set di intersezione è interno a entrambe le istanze **geometry** di origine.  
  
 Questo metodo restituisce sempre Null se gli identificatori SRID delle istanze **geometry** non corrispondono.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato `STCrosses()` per verificare se due istanze `geometry` si incrociano.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

