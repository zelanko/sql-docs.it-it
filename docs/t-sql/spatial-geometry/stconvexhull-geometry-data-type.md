---
description: STConvexHull (tipo di dati geometry)
title: STConvexHull (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STConvexHull (geometry Data Type)
- STConvexHull_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull (geometry Data Type)
ms.assetid: 60a520a6-1a7c-486b-8d91-34401edf6233
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: add89c5a1705344a661b6061dd7668429961ec14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472516"
---
# <a name="stconvexhull-geometry-data-type"></a>STConvexHull (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un oggetto che rappresenta la struttura convessa di un'istanza **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STConvexHull ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Osservazioni  
 `STConvexHull()` restituisce il più piccolo poligono convesso che contiene l'istanza **geometry** specificata. Le istanze **Point** o le istanze **LineString** collineari restituiranno un'istanza dello stesso tipo di quella di input.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato `STConvexHull()` per trovare la struttura convessa di un'istanza `Polygon``geometry` non convessa.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 1 1, 2 2, 2 0, 0 0))', 0);  
SELECT @g.STConvexHull().ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

