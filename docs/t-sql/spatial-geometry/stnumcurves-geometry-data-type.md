---
description: STNumCurves (tipo di dati geometry)
title: STNumCurves (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fe3418284131577051e48f8300bd89df2abc0ec1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444963"
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Questo metodo restituisce il numero di curve di un'istanza **geometry** quando l'istanza è un tipo di dati spaziali unidimensionali. I tipi di dati spaziali unidimensionali includono **LineString**, **CircularString** e **CompoundCurve**. `STNumCurves`() funziona solo su tipi semplici; non funziona con raccolte **geometry** come **MultiLineString**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STNumCurves()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Osservazioni  
 Un'istanza **geometry** unidimensionale vuota restituisce 0. Viene restituito **NULL** quando l'istanza **geometry** non è un'istanza unidimensionale oppure è un'istanza non inizializzata.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>R. Utilizzo di STNumCurves() in un'istanza CircularString  
 Nell'esempio seguente viene illustrato come ottenere il numero di curve in un'istanza `CircularString`:  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. Utilizzo di STNumCurves() in un'istanza CompoundCurve  
 Nell'esempio seguente viene utilizzato `STNumCurves()` per restituire il numero di curve in un'istanza `CompoundCurve`.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dei tipi di dati spaziali](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

