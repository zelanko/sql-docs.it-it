---
title: STDistance (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 2ae6354623f67003c56c99783e1916b71a80ea3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937051"
---
# <a name="stdistance-geography-data-type"></a>STDistance (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Restituisce la distanza più breve tra un punto in un'istanza **geography** e un punto in un'altra istanza **geography**.  
  
> [!NOTE]  
>  `STDistance()` restituisce la **LineString** più breve tra due tipi di geografia. È un'approssimazione della distanza geodetica. La deviazione di `STDistance()` dalla distanza geodetica esatta sui modelli di terra comuni non è superiore allo 0,25%. In tal modo si evitano confusioni sulle differenze minime tra lunghezza e distanza nei tipi geodetici.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STDistance ( other_geography )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geography*  
 Altra istanza **geography** da cui misurare la distanza rispetto all'istanza sulla quale viene chiamato STDistance(). Se *other_geography* è un set vuoto, STDistance() restituisce un valore Null.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **float**  
  
 Tipo CLR restituito: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 STDistance() restituisce sempre Null se gli identificatori SRID delle istanze **geography** non corrispondono.  
  
> [!NOTE]  
>  I metodi nel tipo di dati **geography** che calcolano un'area o una distanza restituiscono risultati diversi a seconda dell'identificatore SRID dell'istanza usato nel metodo.   Per altre informazioni sugli identificatori SRID, vedere [Spatial Reference Identifiers &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) (Identificatori SRID).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene trovata la distanza tra due istanze **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
