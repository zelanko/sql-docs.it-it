---
title: Poligono | Microsoft Docs
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74e6c8cc19bac4c0428924effda87952642a37dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081657"
---
# <a name="polygon"></a>Polygon

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Un oggetto **Polygon** è una superficie bidimensionale archiviata come una sequenza di punti che definiscono un anello di delimitazione esterno e nessuno o più anelli interni.  
  
## <a name="polygon-instances"></a>Istanze Polygon  
 Un'istanza **Polygon** può essere formata da un anello che ha almeno tre punti distinti. Un'istanza **Polygon** può essere anche vuota.  
  
L'anello esterno e ogni anello interno di un oggetto **Polygon** ne definiscono il limite. Lo spazio all'interno degli anelli definisce l'interno dell'oggetto **Polygon**.  
  
La figura seguente mostra alcuni esempi di istanze **Polygon** .  
  
 ![Esempi di istanze di geometria Polygon](../../relational-databases/spatial/media/polygon.gif "Esempi di istanze di geometria Polygon")  
  
Come indicato nell'illustrazione:  
  
1.  La figura 1 è un'istanza **Polygon** il cui limite è definito da un anello esterno e due anelli interni.  
  
2.  La figura 2 è un'istanza **Polygon** il cui limite è definito da un anello esterno e due anelli interni. L'area negli anelli interni è parte dell'esterno dell'istanza **Polygon** .  
  
3.  La figura 3 è un'istanza **Polygon** valida perché i suoi anelli interni si intersecano in un solo punto tangente.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="accepted-instances"></a>Istanze accettate  
 Le istanze **Polygon** accettate sono istanze che possono essere archiviate in una variabile **geometry** o **geography** senza generare un'eccezione. Di seguito sono riportate le istanze **Polygon** accettate:  
  
-   Istanza **Polygon** vuota  
-   Istanza **Polygon** che ha un anello esterno accettabile e zero o più anelli interni accettabili  
  
I criteri seguenti sono necessari affinché un anello sia accettabile.  
  
-   L'istanza **LineString** deve essere accettata.  
-   L'istanza **LineString** deve avere almeno quattro punti.  
-   I punti iniziale e finale dell'istanza **LineString** devono corrispondere.  
  
L'esempio seguente illustra le istanze **Polygon** accettate.  
  
```sql  
DECLARE @g1 geometry = 'POLYGON EMPTY';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';  
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';  
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';  
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
```  
  
Come illustrato in `@g4` e `@g5` è possibile che **Polygon** accettata non sia un'istanza **Polygon** valida. `@g5` mostra anche che un'istanza Polygon, per essere accettata, deve contenere solo un anello con quattro punti qualsiasi.  
  
Negli esempi seguenti viene generata un'eccezione `System.FormatException` , poiché le istanze **Polygon** non vengono accettate.  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';  
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';  
```  
  
`@g1` non viene accettata perché l'istanza **LineString** per l'anello esterno non contiene un numero di punti sufficiente. `@g2` non viene accettata perché il punto iniziale dell'istanza **LineString** per l'anello esterno non corrisponde al punto finale. Nell'esempio seguente è presente un anello esterno accettabile, ma l'anello interno non è accettabile. Viene inoltre generata un'eccezione `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
 Gli anelli interni di un oggetto **Polygon** possono toccare se stessi e toccarsi tra di loro in ogni punto di tangenza, ma se gli anelli interni di un **Polygon** si incrociano, l'istanza non è valida.  
  
 Nell'esempio seguente vengono illustrate le istanze **Polygon** valide.  
  
```sql  
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g3` è valida perché i due anelli interni si toccano in un solo punto e non si incrociano. Nell'esempio seguente vengono illustrate le istanze `Polygon` non valide.  
  
```sql   
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';  
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';  
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';  
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';  
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';  
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();  
```  
  
 `@g1` non è valida perché l'anello interno tocca l'anello esterno in due punti. `@g2` non è valida perché il secondo anello interno si trova all'interno del primo anello interno. `@g3` non è valida perché i due anelli interni si toccano in più punti consecutivi. `@g4` non è valida perché gli interni dei due anelli interni si sovrappongono. `@g5` non è valida perché l'anello esterno non è il primo anello. `@g6` non è valida perché l'anello non presenta almeno tre punti distinti.  
  
## <a name="examples"></a>Esempi  
### <a name="example-a"></a>Esempio A.  
Nell'esempio seguente viene creata un'istanza di `geometry` `Polygon` semplice con un foro e SRID 10.
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STPolyFromText(
    'POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))',
    10);
```  
  

### <a name="example-b"></a>Esempio B.   
Un'istanza non valida può essere immessa e convertita in un'istanza `geometry` valida. Nell'esempio seguente di un `Polygon`, gli anelli interni ed esterni si sovrappongono e l'istanza non è valida.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse(
    'POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))'
    );  
```  
  
### <a name="example-c"></a>Esempio C.  
Nell'esempio seguente, l'istanza non valida è resa valida con `MakeValid()`.  
  
```sql  
SET @g = @g.MakeValid();  
SELECT @g.ToString();  
```  
  
L'istanza `geometry` restituita dall'esempio precedente è un `MultiPolygon`.  
  
```sql  
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)),
              ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```  
  
### <a name="example-d"></a>Esempio D.  
Questo è un altro esempio di conversione di un'istanza non valida in un'istanza geometry valida. Nell'esempio seguente l'istanza `Polygon` è stata creata utilizzando tre punti esattamente uguali:  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');  
SET @g = @g.MakeValid();  
SELECT @g.ToString()  
```  
  
L'istanza geometry restituita sopra è `Point(1 3)`.  Se l'istanza `Polygon` indicata è `POLYGON((1 3, 1 5, 1 3, 1 3))` , `MakeValid()` restituirà `LINESTRING(1 3, 1 5)`.  
  
## <a name="see-also"></a>Vedere anche  
 [STArea &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STExteriorRing &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)   
 [STNumInteriorRing &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)   
 [STInteriorRingN &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)   
 [STCentroid &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [MultiPolygon](../../relational-databases/spatial/multipolygon.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [STIsValid &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STIsValid &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
  
