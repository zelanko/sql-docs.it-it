---
title: STNumGeometries (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geography Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries method
ms.assetid: 6ae7fac2-62f1-420f-9fc9-a09606be9605
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7b327c6f053e7a124462dc7d2243cdecb8799c84
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85702483"
---
# <a name="stnumgeometries-geography-data-type"></a>STNumGeometries (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce il numero di **geometrie** che costituiscono un'istanza **geography**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **int**  
  
 Tipo CLR restituito: **SqlInt32**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo restituisce 1 se l'istanza **geography** non è un'istanza **MultiPoint**, **MultiLineString**, **MultiPolygon** o **GeometryCollection** oppure 0 se l'istanza **geography** è vuota.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `MultiPoint` e viene usato `STNumGeometries()` per trovare il numero di **geometrie** contenute nell'istanza.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT((-122.360 47.656), (-122.343 47.656))', 4326);  
SELECT @g.STNumGeometries();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
