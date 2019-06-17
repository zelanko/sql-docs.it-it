---
title: LineString | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c340ec4e6b650784823869b8715579448229fb4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935203"
---
# <a name="linestring"></a>LineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **LineString** indica un oggetto unidimensionale che rappresenta una sequenza di punti e i segmenti lineari che li connettono.  
  
## <a name="linestring-instances"></a>Istanze LineString  
 Nella figura seguente vengono illustrati esempi di istanze **LineString** .  
  
 ![Esempi di istanze di geometria LineString](../../relational-databases/spatial/media/linestring.gif "Esempi di istanze di geometria LineString")  
  
Come indicato nell'illustrazione:  
  
-   La figura 1 rappresenta un'istanza **LineString** semplice non chiusa.  
  
-   La figura 2 rappresenta un'istanza **LineString** non semplice e non chiusa.  
  
-   La figura 3 rappresenta un'istanza **LineString** semplice chiusa che, di conseguenza, è un anello.  
  
-   La figura 4 rappresenta un'istanza **LineString** non semplice chiusa che, di conseguenza, non è un anello.  
  
### <a name="accepted-instances"></a>Istanze accettate  
Le istanze **LineString** accettate possono essere di input in una variabile geometry, ma è possibile che non siano istanze **LineString** valide. Per poter essere accettata, un'istanza **LineString** deve soddisfare i criteri seguenti. L'istanza deve essere composta da almeno due punti distinti e deve essere vuota. Di seguito sono riportate le istanze LineString accettate.  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
`@g3` indica che un'istanza **LineString** può essere accettata, ma non è valida.  
  
L'istanza **LineString** seguente non viene accettata. Verrà generata un'eccezione `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
Per poter essere valida, un'istanza **LineString** deve soddisfare i criteri seguenti.  
  
1.  L'istanza **LineString** deve essere accettata.  
2.  Se un'istanza **LineString** non è vuota, deve contenere almeno due punti distinti.  
3.  L'istanza **LineString** non può sovrapporsi a un intervallo di due o più punti consecutivi.  
  
Di seguito sono riportate le istanze **LineString** valide.  
  
```sql  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
Di seguito sono riportate le istanze **LineString** non valide.  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
> Il rilevamento delle sovrapposizioni di **LineString** è basato su calcoli a virgola mobile inesatti.  
  
## <a name="examples"></a>Esempi  
### <a name="example-a"></a>Esempio A.    
L'esempio seguente illustra come creare un'istanza `geometry``LineString` con tre punti e un SRID di 0:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
### <a name="example-b"></a>Esempio B.   
Ogni punto nell'istanza `LineString` può contenere valori Z (innalzamento) e M (misura). In questo esempio vengono aggiunti i valori M all'istanza `LineString` creata nell'esempio precedente. M e Z possono essere valori Null.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
### <a name="example-c"></a>Esempio C.   
Nell'esempio seguente viene illustrato come creare un'istanza `geometry LineString` con due punti uguali. Una chiamata a `IsValid` indica che l'istanza **LineString** non è valida e una chiamata a `MakeValid` convertirà l'istanza **LineString** in un'istanza **Point**.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);  
IF @g.STIsValid() = 1  
  BEGIN  
     SELECT @g.ToString() + ' is a valid LineString.';    
  END  
ELSE  
  BEGIN  
     SELECT @g.ToString() + ' is not a valid LineString.';  
     SET @g = @g.MakeValid();  
     SELECT @g.ToString() + ' is a valid Point.';    
  END  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [STLength &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints &#40;geometry Data Type&#41; (STNumPoints &#40;tipo di dati geometry&#41;)](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
