---
title: STArea (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 49919caaf30bb425e90b286cb3c8e7877067ae6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936239"
---
# <a name="starea-geography-data-type"></a>STArea (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce l'area della superficie totale di un'istanza **geography**. I risultati di STArea() sono costituiti dall'unità di misura al quadrato usata dall'identificatore di riferimento spaziale dell'istanza **geography**. Se, ad esempio, l'identificatore SRID dell'istanza è 4326, STArea() restituisce i risultati in metri quadrati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **float**  
  
Tipo CLR restituito: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
STArea() restituisce 0 se un'istanza **geography** contiene solo figure zero-dimensionali e unidimensionali oppure se è vuota.  
  
> [!NOTE]  
>  I metodi applicati al tipo di dati **geography** che producono valori misurabili restituiranno risultati diversi a seconda dell'identificatore SRID dell'istanza usato nel metodo. Per altre informazioni sugli identificatori SRID, vedere [Spatial Reference Identifiers &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) (Identificatori SRID).  
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene usato `STArea()` per creare un'istanza `Polygon geography` e viene calcolata l'area del poligono.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>Vedere anche  
[Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
