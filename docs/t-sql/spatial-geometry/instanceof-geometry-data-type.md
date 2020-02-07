---
title: InstanceOf (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7eee6c8aa847a199f7b1547f61bbcd523039644f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68101238"
---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Metodo che verifica se l'istanza **geometry** corrisponde al tipo specificato. Restituisce 1 se l'istanza **geometry** corrisponde al tipo specificato. Questo metodo restituisce 1 anche se il tipo specificato è un predecessore del tipo di istanza. In caso contrario restituisce 0.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>Argomenti  
*geometry_type*  
Stringa **nvarchar(4000)** che specifica uno dei 15 tipi esposti nella gerarchia del tipo **geometry**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Osservazioni  
 L'input per il metodo deve essere uno dei tipi seguenti: **Geometry**, **Point**, **Curve**, **LineString**, **CircularString**, **CompoundCurve**, **Surface**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString** e **MultiPoint**. Questo metodo genera un'eccezione **ArgumentException** se per l'input viene usata qualsiasi altra stringa.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `MultiPoint` e viene utilizzato `InstanceOf()` per verificare se l'istanza è di tipo `GeometryCollection`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

