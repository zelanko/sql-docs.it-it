---
title: STAsText (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 207341d09f153ed819d331960cf00dbb6c410bf3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85704953"
---
# <a name="stastext-geography-data-type"></a>STAsText (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza **geography**. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.  
  
 Questo metodo con tipo di dati **geography** supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **nvarchar(max)**  
  
 Tipo CLR restituito: **SqlChars**  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo OGC di un'istanza **geography** può essere determinato richiamando [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], il set di possibili risultati restituito nel server è stato esteso alle istanze **FullGlobe**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene usato `STAsText()` per creare un'istanza `LineString``geography` da (-122.360, 47.656) a (-122.343, 47.656) dal testo. e viene restituito il risultato in formato testo.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
