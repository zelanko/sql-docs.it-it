---
title: CurvePolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ddd07c68d5549ed4cfc7cc3f421168ad968dadda
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014245"
---
# <a name="curvepolygon"></a>CurvePolygon
  Un'istanza `CurvePolygon` è una superficie topologicamente chiusa definita da un anello di delimitazione esterno e nessuno o più anelli interni  
  
> [!IMPORTANT]  
>  Per una descrizione dettagliata ed esempi delle funzionalità spaziali introdotte in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], tra cui la `CurvePolygon` sottotipo, scaricare il white paper [nuove funzionalità spaziali in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 I criteri seguenti vengono definiti attributi di un `CurvePolygon` istanza:  
  
-   Il limite dell'istanza `CurvePolygon` viene definito dall'anello esterno e da tutti gli anelli interni.  
  
-   L'interno dell'istanza `CurvePolygon` è lo spazio tra l'anello esterno e tutti gli anelli interni.  
  
 Un'istanza `CurvePolygon` differisce da un'istanza `Polygon` per il fatto che un'istanza `CurvePolygon` può contenere i segmenti di arco circolare seguenti: `CircularString` e `CompoundCurve`.  
  
## <a name="compoundcurve-instances"></a>Istanze CompoundCurve  
 Nell'illustrazione seguente vengono illustrate figure `CurvePolygon` valide:  
  
### <a name="accepted-instances"></a>Istanze accettate  
 Per poter essere accettata, un'istanza `CurvePolygon` deve essere vuota o contenere solo anelli di arco circolare accettati. Un anello di arco circolare accettato soddisfa i requisiti seguenti.  
  
1.  È un'istanza `LineString`, `CircularString` o `CompoundCurve` accettata. Per altre informazioni sulle istanze accettate, vedere [LineString](linestring.md), [CircularString](circularstring.md)e [CompoundCurve](compoundcurve.md).  
  
2.  Dispone almeno di quattro punti.  
  
3.  I punti iniziale e finale condividono le stesse coordinate X e Y.  
  
    > [!NOTE]  
    >  I valori Z e ; vengono ignorati.  
  
 Nell'esempio seguente vengono illustrate le istanze `CurvePolygon` accettate.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` viene accettata anche se i punti iniziale e finale hanno valori Z diversi perché i valori Z vengono ignorati. `@g5` viene accettata anche se l'istanza del tipo `geography` non è valida.  
  
 Gli esempi seguenti generano `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` non viene accettata perché i punti iniziale e finale non hanno lo stesso valore Y. `@g2` non viene accettata perché l'anello non dispone di un numero di punti sufficiente.  
  
### <a name="valid-instances"></a>Istanze valide  
 Perché un'istanza `CurvePolygon` sia valida, è necessario che l'anello interno e quello esterno soddisfino i criteri seguenti:  
  
1.  Possono toccarsi solo in corrispondenza di singoli punti tangenti.  
  
2.  Non possono incrociarsi.  
  
3.  Ogni anello deve contenere almeno quattro punti.  
  
4.  Ogni anello deve essere un tipo di curva accettabile.  
  
 Le istanze `CurvePolygon` devono inoltre soddisfare criteri specifici a seconda di se sono di un tipo di dati `geometry` o `geography`.  
  
#### <a name="geometry-data-type"></a>Tipo di dati geometry  
 Un'istanza **geometryCurvePolygon** valida deve avere gli attributi seguenti:  
  
1.  Tutti gli anelli interni devono essere contenuti nell'anello esterno.  
  
2.  Può disporre di più anelli interni, ma un anello interno non può contenere un altro anello interno.  
  
3.  Nessun anello può incrociare se stesso o un altro anello.  
  
4.  Gli anelli possono toccarsi solo in corrispondenza di singoli punti tangenti (il numero di punti dove gli anelli si toccano deve essere limitato).  
  
5.  L'interno del poligono deve essere connesso.  
  
 L'esempio seguente illustra un'istanza **geometryCurvePolygon** valida.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 Le istanze CurvePolygon dispongono delle stesse regole di validità delle istanze Polygon, ad eccezione del fatto che le istanze CurvePolygon possono accettare i nuovi tipi di segmento di arco circolare. Per altri esempi di istanze valide o non valide, vedere [Polygon](polygon.md).  
  
#### <a name="geography-data-type"></a>Tipo di dati geography  
 Un'istanza **geographyCurvePolygon** valida deve avere gli attributi seguenti:  
  
1.  L'interno del poligono viene connesso utilizzando il lato sinistro della regola.  
  
2.  Nessun anello può incrociare se stesso o un altro anello.  
  
3.  Gli anelli possono toccarsi solo in corrispondenza di singoli punti tangenti (il numero di punti dove gli anelli si toccano deve essere limitato).  
  
4.  L'interno del poligono deve essere connesso.  
  
 Nell'esempio seguente viene illustrata un'istanza CurvePolygon geography valida.  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. Creazione di un'istanza Geometry con un'istanza CurvePolygon vuota  
 In questo esempio viene illustrato come creare un'istanza `CurvePolygon` vuota:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. Dichiarazione e creazione di un'istanza Geometry utilizzando un'istanza CurvePolygon nella stessa istruzione  
 In questo frammento di codice viene illustrato come dichiarare e inizializzare un'istanza geometry con un'istanza `CurvePolygon` nella stessa istruzione:  
  
```sql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. Creazione di un'istanza Geography con un'istanza CurvePolygon  
 Nel frammento di codice seguente viene illustrato come dichiarare e inizializzare un'istanza `geography` con un'istanza `CurvePolygon`:  
  
```sql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. Archiviazione di un'istanza CurvePolygon con un solo anello di delimitazione esterno  
 In questo esempio viene illustrato come archiviare un cerchio semplice in un'istanza `CurvePolygon` (per definire il cerchio viene utilizzato solo un anello di delimitazione esterno):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. Archiviazione di un'istanza CurvePolygon contenente anelli interni  
 In questo esempio viene creato un anello in un'istanza `CurvePolygon` (per definire l'anello vengono utilizzati sia un anello di delimitazione esterno che un anello interno):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 In questo esempio viene illustrata sia un'istanza `CurvePolygon` valida che un'istanza non valida in caso di utilizzo di anelli interni:  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 Sia per @g1 che per @g2 viene usato lo stesso anello di delimitazione esterno: un cerchio con un raggio di 5 ed entrambi usano un quadrato per un anello interno.  Tuttavia, l'istanza @g1 è valida, mentre l'istanza @g2 non lo è.  @g2 è non valida perché l'anello interno divide lo spazio interno delimitato dall'anello esterno in quattro aree separate.  Nel disegno seguente viene illustrata questa condizione:  
  
## <a name="see-also"></a>Vedere anche  
 [Polygon](polygon.md)   
 [CircularString](circularstring.md)   
 [CompoundCurve](compoundcurve.md)   
 [Guida di riferimento ai metodi per il tipo di dati geometry](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [Guida di riferimento ai metodi per il tipo di dati geography](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [Panoramica dei tipi di dati spaziali](spatial-data-types-overview.md)  
  
  
