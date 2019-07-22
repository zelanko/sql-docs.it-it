---
title: STSymDifference (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSymDifference (geography Data Type)
- STSymDifference_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geography Data Type)
ms.assetid: 82bbfa2c-a61b-4f41-9bf8-6f720f363bae
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f1e7824f864d7d764529fb6860496316bf00537d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120768"
---
# <a name="stsymdifference-geography-data-type"></a>STSymDifference (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce un oggetto che rappresenta tutti i punti che si trovano in un'istanza **geography** o un'altra istanza **geography**, ma non i punti che si trovano in entrambe le istanze.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STSymDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geography*  
 Altra istanza **geography** oltre all'istanza sulla quale viene richiamato STSymDistance().  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Questo metodo restituisce sempre Null se gli identificatori SRID delle istanze **geography** non corrispondono.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta le istanze spaziali di dimensioni maggiori di un emisfero. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il set di possibili risultati nel server è stato esteso alle istanze **FullGlobe**.  
  
 Il risultato può contenere segmenti di arco circolare solo se le istanze di input contengono segmenti di arco circolare.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygons"></a>A. Calcolo della differenza simmetrica di due poligoni  
 Nell'esempio seguente viene utilizzato `STSymDifference()` per calcolare la differenza simmetrica tra due istanze `Polygon`.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-with-fullglobe"></a>B. Calcolo della differenza simmetrica con FullGlobe  
 Nell'esempio seguente viene confrontata la differenza simmetrica di `Polygon` a `FullGlobe`.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STSymDifference('FULLGLOBE').ToString();
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
