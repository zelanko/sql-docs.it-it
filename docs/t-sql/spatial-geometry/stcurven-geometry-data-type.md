---
title: STCurveN (tipo di dati geometry) | Microsoft Docs
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7905da990bf06b79641f19823f954abe201139ad
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555066"
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (tipo di dati geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Restituisce la curva specificata da un'istanza **geometry** e corrispondente a **LineString**, **CircularString**, **CompoundCurve** o **MultiLineString**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STCurveN ( curve_index )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *curve_index*  
 Espressione **int** compresa tra 1 e il numero di curve nell'istanza **geometry**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
## <a name="exceptions"></a>Eccezioni  
 Se *curve_index* < 1 viene generata un'eccezione `ArgumentOutOfRangeException`.  
  
## <a name="remarks"></a>Osservazioni  
 **NULL** viene restituito in uno dei casi seguenti:  
  
-   L'istanza **geometry** viene dichiarata, ma non ne viene creata un'istanza  
  
-   L'istanza **geometry** è vuota  
  
-   *curve_index* supera il numero di curve nell'istanza **geometry**  
  
-   L'istanza **geometry** è di tipo **Point**, **MultiPoint**, **Polygon**, **CurvePolygon** o **MultiPolygon**  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>R. Utilizzo di STCurves() in un'istanza CircularString  
 Nell'esempio seguente viene restituita la seconda curva in un'istanza `CircularString`:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Nell'esempio riportato in precedenza in questo argomento viene restituito:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. Utilizzo di STCurveN() in un'istanza CompoundCurve con un'istanza CircularString  
 Nell'esempio seguente viene restituita la seconda curva in un'istanza `CompoundCurve`:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Nell'esempio riportato in precedenza in questo argomento viene restituito:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. Utilizzo di STCurveN() in un'istanza CompoundCurve con tre istanze CircularString  
 Nell'esempio seguente viene utilizzata un'istanza `CompoundCurve` che combina tre istanze `CircularString` separate nella stessa sequenza di curve dell'esempio precedente:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Nell'esempio riportato in precedenza in questo argomento viene restituito:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 Si noti che i risultati sono gli stessi dei tre esempi precedenti. Indipendentemente dal formato WKT (well-known text) utilizzato per immettere la stessa sequenza di curve, i risultati restituiti da `STCurveN()` sono gli stessi quando viene utilizzata un'istanza `CompoundCurve`.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. Convalida del parametro prima della chiamata a STCurveN()  
 L'esempio seguente illustra come assicurarsi che `@n` sia valido prima di chiamare il metodo `STCurveN()`:  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [STNumCurves &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

