---
title: STMPolyFromText (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPolyFromText (geography Data Type)
- STMPolyFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromText method
ms.assetid: 15356c0f-5144-418d-aa96-3e7ea5fecea3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5c60f2395b34d580c4782de5d3cfda40eb39cf35
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85702842"
---
# <a name="stmpolyfromtext-geography-data-type"></a>STMPolyFromText (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un'istanza **geography** da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium), integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
STMPolyFromText ( 'multipolygon_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argomenti  
 *multipolygon_tagged_text*  
 Rappresentazione WKT dell'istanza **geographyMultiPolygon** da restituire. *multipolygon_tagged_text* è un'espressione **nvarchar(max)** .  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geographyMultiPolygon** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **Sql Geography**  
  
 Tipo OGC: **MultiPolygon**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo genera un'eccezione **FormatException** se l'input non è formattato in modo corretto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato il metodo `STMPolyFromText()` per creare un'istanza `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STMPolyFromText('MULTIPOLYGON(((-122.358 47.653, -122.348 47.649, -122.358 47.658, -122.358 47.653)), ((-122.341 47.656, -122.341 47.661, -122.351 47.661, -122.341 47.656)))', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
