---
title: STAsBinary (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f2b110b4ee7abafc2c38ebc774d3d1673f0586c7
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552899"
---
# <a name="stasbinary-geography-data-type"></a>STAsBinary (tipo di dati geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce la rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza **geography**.  
  
 Questo metodo con tipo di dati **geography** supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STAsBinary ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **varbinary(max)**  
  
 Tipo CLR restituito: **SqlBytes**  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo OGC di un'istanza **geography** può essere determinato richiamando [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene usato `STAsBinary()` per creare un'istanza `LineString``geography` da (-122.360, 47.656) a (-122.343, 47.656) dal testo. e viene restituito il risultato in formato WKB.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
