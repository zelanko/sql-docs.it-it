---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 6bc07f8770e6cd7d1fb1e4b4e6e40ca8b1c5256f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014197"
---
# <a name="linestring"></a>LineString
  
  `LineString` indica un oggetto unidimensionale che rappresenta una sequenza di punti e i segmenti lineari che li connettono.  
  
## <a name="linestring-instances"></a>Istanze LineString  
 Nella figura seguente vengono illustrati esempi di istanze `LineString`.  
  
 ![Esempi di istanze di geometria LineString](../../database-engine/media/linestring.gif "Esempi di istanze di geometria LineString")  
  
 Come indicato nell'illustrazione:  
  
-   La figura 1 rappresenta un'istanza `LineString` semplice non chiusa.  
  
-   La figura 2 rappresenta un'istanza `LineString` non semplice e non chiusa.  
  
-   La figura 3 rappresenta un'istanza `LineString` semplice chiusa che, di conseguenza, è un anello.  
  
-   La figura 4 rappresenta un'istanza `LineString` non semplice chiusa che, di conseguenza, non è un anello.  
  
### <a name="accepted-instances"></a>Istanze accettate  
 Le istanze `LineString` accettate possono essere di input in una variabile geometry, ma è possibile che non siano istanze `LineString` valide. Per poter essere accettata, un'istanza `LineString` deve soddisfare i criteri seguenti: L'istanza deve essere composta da almeno due punti distinti e deve essere vuota. Di seguito sono riportate le istanze LineString accettate.  
  
```  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
 In `@g3` viene illustrato che un'istanza `LineString` può essere accettata, ma non è valida.  
  
 L'istanza `LineString` seguente non viene accettata. Verrà generata un'eccezione `System.FormatException`.  
  
```  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
 Per poter essere valida, un'istanza `LineString` deve soddisfare i criteri seguenti.  
  
1.  L'istanza `LineString` deve essere accettata.  
  
2.  Se un'istanza `LineString` non è vuota, deve contenere almeno due punti distinti.  
  
3.  L'istanza `LineString` non può sovrapporti a un intervallo di due o più punti consecutivi.  
  
 Le istanze `LineString` seguenti sono valide.  
  
```  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
  
```  
  
 Le istanze `LineString` seguenti non sono valide.  
  
```  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
>  Il rilevamento delle sovrapposizioni di `LineString` è basato su calcoli a virgola mobile inesatti.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente illustra come creare un'istanza `geometry``LineString` con tre punti e un SRID di 0:  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
 Ogni punto nell'istanza `LineString` può contenere valori Z (innalzamento) e M (misura). In questo esempio vengono aggiunti i valori M all'istanza `LineString` creata nell'esempio precedente. M e Z possono essere valori Null.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
 Nell'esempio seguente viene illustrato come creare un'istanza `geometry LineString` con due punti uguali. Una chiamata a `IsValid` indica che l'istanza `LineString` non è valida e una chiamata a `MakeValid` convertirà l'istanza `LineString` in un `Point`.  
  
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
  
 Il frammento di codice precedente restituirà quando segue:  
  
```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [STLength &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints &#40;geometry Data Type&#41; (STNumPoints &#40;tipo di dati geometry&#41;)](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [Dati spaziali &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
