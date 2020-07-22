---
title: STEndPoint (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEndPoint (geography Data Type)
- STEndPoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndPoint method
ms.assetid: 8974cd07-8ec4-4126-8fc2-fdcf322ccedd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 475b5e99cd7628992e90a2921c0bd726f8f69560
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554406"
---
# <a name="stendpoint-geography-data-type"></a>STEndPoint (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce il punto di fine di un'istanza **geography**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STEndPoint ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
 Tipo OGC (Open Geospatial Consortium): **Point**  
  
## <a name="remarks"></a>Osservazioni  
 STEndPoint() equivale a [STPointN](../../t-sql/spatial-geography/stpointn-geography-data-type.md)`(x.STNumPoints``())`.  
  
 Se chiamato su un'istanza **geography** vuota, questo metodo restituisce Null.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `LineString` con `STGeomFromText()` e viene utilizzato `STEndPoint()` per recuperare il punto di fine di `LineString`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
