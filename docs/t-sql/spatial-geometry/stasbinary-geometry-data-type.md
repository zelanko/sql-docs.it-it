---
title: STAsBinary (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary (geometry Data Type)
ms.assetid: 65353777-e3e6-461c-9504-ea4d83312692
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: aa0bc1c078e476fbf888f632f583179c6066e1e8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748806"
---
# <a name="stasbinary-geometry-data-type"></a>STAsBinary (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce la rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza di geometria.  
 
## <a name="syntax"></a>Sintassi  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **varbinary(max)**  
  
 Tipo CLR restituito: **SqlBytes**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza di geometria `LineString` da (0,0) a (2,3) dal testo. `STAsBinary()` restituisce il risultato in WKB.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
