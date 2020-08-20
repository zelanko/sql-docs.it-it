---
description: GeomFromGml (tipo di dati geometry)
title: GeomFromGml (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geometry Data Type)
ms.assetid: a3f2c84b-a49f-4ce3-ba25-b903fb0c99b4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5526d9e8fb788e06b1ed61b3e20236963319b844
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458961"
---
# <a name="geomfromgml-geometry-data-type"></a>GeomFromGml (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Costruisce un'istanza **geometry** data una rappresentazione nel subset [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di Geography Markup Language (GML).
  
Per ulteriori informazioni su Geography Markup Language, vedere le seguenti specifiche Open Geospatial Consortium:
  
[Specifiche OGC, Geography Markup Language](https://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *GML_input*  
 Input XML da cui GML restituirà un valore.  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geometry** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo genererà un'eccezione **FormatException** se l'input non è formattato in modo corretto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato il metodo `GeomFromGml()` per creare un'istanza `geometry`.  
  
```  
DECLARE @g geometry;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="https://www.opengis.net/gml"> <posList>100 100 20 180 180 180</posList> </LineString>';  
SET @g = geometry::GeomFromGml(@x, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di geometria statici estesi](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

