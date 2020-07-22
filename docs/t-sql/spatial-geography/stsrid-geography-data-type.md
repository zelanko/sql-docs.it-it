---
title: STSrid (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 57c580706f5a8a7c9fec02ca7675b6733cd9dddf
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555359"
---
# <a name="stsrid-geography-data-type"></a>STSrid (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **STSrid** è un Integer che rappresenta l'identificatore SRID dell'istanza.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STSrid  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo CLR: **SqlInt32**  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà può essere modificata.  
  
## <a name="examples"></a>Esempi  
 Nel primo esempio viene creata un'istanza `geography` con il valore dell'identificatore SRID uguale a 4326 (WGS84) e viene utilizzato `STSrid` per confermare l'identificatore SRID.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 Nel secondo esempio viene utilizzato `STSrid` per impostare il valore dell'identificatore SRID dell'istanza su 4267 (NAD27), quindi viene confermato il valore SRID modificato.  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [Identificatori SRID &#40;Spatial Reference Identifier&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
