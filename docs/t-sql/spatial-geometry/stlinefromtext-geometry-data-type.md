---
title: STLineFromText (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromText (geometry Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText (geometry Data Type)
ms.assetid: 430508ad-207b-4dee-a4d1-4ddf25e6b4a9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a0a912e4ab228617537e9c28e9a5cecc4a0278fe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "72278134"
---
# <a name="stlinefromtext-geometry-data-type"></a>STLineFromText (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce un'istanza **geometry** da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argomenti  
 *linestring_tagged_text*  
 Rappresentazione WKT dell'istanza **geometryLineString** da restituire. *linestring_tagged_text* è un'espressione **nvarchar(max)** .  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geometryLineString** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
 Tipo OGC: **LineString**  
  
## <a name="remarks"></a>Osservazioni  
Questo metodo genera un'eccezione **FormatException** se l'input non è formattato in modo corretto. La notazione WKT per geometria misurata tridimensionale in base alla specifica Simple Features per SQL versione 1.2.1. di Open Geospatial Consortium (OGC) non è supportata. Vedere gli esempi per la rappresentazione supportata dei valori Z (elevazione) e M (misura).
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti usano il metodo `STLineFromText()` per creare un'istanza `geometry`.

### <a name="example-1-two-dimension-geometry-wkt"></a>Esempio 1: WKT geometria bidimensionale
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100, 200 200)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="example-2-three-dimension-geometry-wkt"></a>Esempio 2: WKT geometria tridimensionale
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100, 200 200 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-3-two-dimension-measured-geometry-wkt"></a>Esempio 3: WKT geometria misurata bidimensionale
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 NULL 100, 200 200 NULL 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-4-three-dimension-measured-geometry-wkt"></a>Esempio 4: WKT geometria misurata tridimensionale
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100 100, 200 200 200 200)', 0);  
SELECT @g.ToString();  
``` 
## <a name="see-also"></a>Vedere anche  
 [Metodi di geometria statici OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

