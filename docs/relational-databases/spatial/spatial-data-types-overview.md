---
title: Panoramica dei tipi di dati spaziali | Microsoft Docs
ms.date: 11/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2abe169f1666a1ce44b96130a52ef8edbc5a788e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048518"
---
# <a name="spatial-data-types-overview"></a>Panoramica dei tipi di dati spaziali
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
Esistono due tipi di dati spaziali. Il tipo di dati **geometry** supporta dati planari o euclidei (terra piatta). Il tipo di dati **geometry** è conforme a Open Geospatial Consortium (OGC) Simple Features for SQL Specification versione 1.1.0 e a SQL MM (standard ISO).
Inoltre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta il tipo di dati **geography** , che archivia dati ellissoidali (terra rotonda), ad esempio coordinate di latitudine e longitudine GPS.

##  <a name="objects"></a> Oggetti dati spaziali  
I tipi di dati **geometry** e **geography** supportano sedici oggetti dati spaziali o tipi di istanza. Solo per undici di questi tipi di istanza, tuttavia, è possibile *creare istanze*. È possibile creare e usare queste istanze (o crearne un'istanza) in un database. Queste istanze derivano determinate proprietà dai relativi tipi di dati padre che consentono di distinguerle come **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** o come più istanze di **geometry** o **geography** in un oggetto **GeometryCollection**. Il tipo**Geography** dispone di un tipo di istanza aggiuntivo, **FullGlobe**.  

Nella figura seguente viene illustrata la gerarchia **geometry** sulla quale si basano i tipi di dati **geometry** e **geography** . I tipi di **geometry** e **geography** di cui è possibile creare istanze sono indicati in blu.  

![geom_hierarchy](../../relational-databases/spatial/media/geom-hierarchy.gif) 

Come indicato nella figura, i dieci tipi di cui è possibile creare istanze dei tipi di dati **geometry** e **geography** sono **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**e **GeometryCollection**. Vi è un tipo aggiuntivo di cui è possibile creare istanze per il tipo di dati geography, ovvero **FullGlobe**. I tipi **geometry** e **geography** sono in grado di riconoscere un'istanza specifica purché si tratti di un'istanza con formato corretto, anche se non definita in modo esplicito. Ad esempio, se si definisce un'istanza **Point** usando in modo esplicito il metodo STPointFromText(), **geometry** e **geography** riconoscono l'istanza come **Point**, purché il formato dell'input del metodo sia corretto. Se si definisce la stessa istanza utilizzando il metodo `STGeomFromText()` , entrambi i tipi di dati **geometry** e **geography** riconoscono l'istanza come **Point**.  

I sottotipi per i tipi geometry e geography sono divisi in tipi semplici e di raccolta.  Alcuni metodi come `STNumCurves()` possono essere utilizzati solo con tipi semplici.  

I tipi semplici includono:  
-   [Point](../../relational-databases/spatial/point.md)  
-   [LineString](../../relational-databases/spatial/linestring.md)  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
-   [Poligono](../../relational-databases/spatial/polygon.md)  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  

I tipi di raccolta includono:  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  

##  <a name="differences"></a> Differenze tra i tipi di dati geometry e geography  
I due tipi di dati spaziali si comportano spesso in modo simile, ma esistono alcune differenze fondamentali nel modo in cui i dati vengono archiviati e modificati.  

### <a name="how-connecting-edges-are-defined"></a>Definizione dei bordi di collegamento  
I dati di definizione per i tipi **LineString** e **Polygon** sono solo vertici.  Il bordo di collegamento tra due vertici in un tipo geometry è una linea retta.  Tuttavia, il bordo di collegamento tra due vertici in un tipo geografico è un corto arco di grande ellissi tra i due vertici.  Una grande ellisse è l'intersezione dell'ellissoide con un piano attraverso il centro e un arco di grande ellisse è un segmento di arco sulla grande ellisse.  

### <a name="how-circular-arc-segments-are-defined"></a>Definizione di segmenti di arco circolare  
I segmenti di arco circolare per i tipi geometry vengono definiti sul piano delle coordinate cartesiane XY (i valori Z vengono ignorati). I segmenti di arco circolare per i tipi geography vengono definiti da segmenti di curva su una sfera di riferimento. Qualsiasi parallelo sulla sfera di riferimento può essere definito da due archi circolari complementari in cui i punti per entrambi gli archi hanno un angolo di latitudine costante.  

### <a name="measurements-in-spatial-data-types"></a>Misurazioni nei tipi di dati spaziali  
Nel sistema planare, o terra piatta, le misurazioni delle distanze e delle aree vengono fornite nella stessa unità di misurazione delle coordinate. Usando il tipo di dati **geometry** , la distanza tra (2, 2) e (5, 6) è 5 unità, indipendentemente dalle unità usate.  

Nel sistema ellissoidale, o terra rotonda, le coordinate sono fornite in gradi di latitudine e longitudine. Tuttavia, le lunghezze e le aree sono misurate generalmente in metri e metri quadrati, sebbene la misurazione possa dipendere dall'identificatore di riferimento spaziale (SRID) dell'istanza **geography** . L'unità di misurazione più comune per il tipo di dati **geography** è il metro.  

### <a name="orientation-of-spatial-data"></a>Orientamento dei dati spaziali  
Nel sistema planare l'orientamento dell'anello di un poligono non è un fattore di particolare rilevanza. Ad esempio, un poligono descritto da ((0, 0), (10, 0), (0, 20), (0, 0)) è identico al poligono descritto da ((0, 0), (0, 20), (10, 0), (0, 0)). OGC Simple Features for SQL Specification non indica un ordinamento dell'anello e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non impone tale ordinamento.  

In un sistema ellissoidale, un poligono non ha significato, o è ambiguo, senza un orientamento. Ad esempio, un anello intorno all'equatore descrive l'emisfero nord o sud? Se si utilizza il tipo di dati **geography** per archiviare l'istanza spaziale, è necessario specificare l'orientamento dell'anello e descrivere accuratamente la posizione dell'istanza. L'interno del poligono in un sistema ellissoidale è definito dal lato sinistro della regola.  

Quando il livello di compatibilità è uguale o minore di 100 in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , al tipo di dati **geography** si applicano le restrizioni seguenti:  
-   Ogni istanza **geography** deve adattarsi all'interno di un singolo emisfero. Non è possibile archiviare oggetti spaziali con dimensioni maggiori di un emisfero.  
-   Qualsiasi istanza **geography** di una rappresentazione Well-Known Text (WKT) o Well-Known Binary (WKB) OCG che produca un oggetto più grande di un emisfero genera **ArgumentException**.  
-   I metodi del tipo di dati **geography** che richiedono l'input di due istanze **geography** , ad esempio STIntersection(), STUnion(), STDifference() e STSymDifference(), restituiranno Null se i risultati dei metodi non si adattano a un singolo emisfero. Anche STBuffer() restituirà Null se l'output supera un singolo emisfero.  

In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] **FullGlobe** è un tipo speciale di Polygon che copre l'intero globo. **FullGlobe** dispone di un'area, ma non ha bordi o vertici.  

### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>Anelli interni ed esterni non rilevanti nel tipo di dati `geography`  
In OGC Simple Features for SQL Specification vengono trattati anelli esterni e interni, ma questa distinzione non è significativa per il tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** . È possibile scegliere qualsiasi anello di un poligono come anello esterno.  

Per ulteriori informazioni sulle specifiche OGC, vedere quanto riportato di seguito:  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](https://go.microsoft.com/fwlink/?LinkId=93627)  
-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options](https://go.microsoft.com/fwlink/?LinkId=93628) (Specifiche OGC, accesso semplificato alle caratteristiche Parte 2 - Opzioni SQL)  

##  <a name="circular"></a> Segmenti di arco circolare  
Tre tipi di cui è possibile creare istanze possono accettare segmenti di arco circolare: **CircularString**, **CompoundCurve** e **CurvePolygon**.  Un segmento di arco circolare è definito da tre punti in un piano bidimensionale. Il terzo punto non può corrispondere al primo punto.  

Nelle figure A e B vengono illustrati segmenti di arco circolare tipici. Si noti come ognuno dei tre punti giace sul perimetro di un cerchio.  

Nelle figure C e D viene illustrato come un segmento di linea possa essere definito segmento di arco circolare.  Si noti che sono ancora necessari tre punti per definire il segmento di arco circolare, diversamente da un segmento di linea regolare, che può essere definito solo da due punti.  
I metodi che operano sui tipi di segmento di arco circolare utilizzano segmenti di linea retta per simulare l'arco circolare. Il numero di segmenti di linea utilizzati per simulare l'arco dipenderanno dalla lunghezza e dalla curvatura dell'arco. Benché sia possibile archiviare i valori Z per ognuno dei tipi di segmento di arco circolare, i metodi non utilizzeranno i valori Z nei calcoli.  

> [!NOTE]  
> Se si specificano valori Z per segmenti di arco circolare, tali valori devono essere gli stessi per tutti i punti nel segmento di arco circolare perché questo venga accettato per l'input. Ad esempio, `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` è ammesso, mentre `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` non lo è.  

### <a name="linestring-and-circularstring-comparison"></a>Confronto tra LineString e CircularString  
Questo esempio illustra come archiviare triangoli isosceli identici usando un'istanza **LineString** e un'istanza **CircularString**:  

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```  

Si noti che un'istanza **CircularString** richiede sette punti per definire il triangolo, mentre un'istanza **LineString** richiede solo quattro punti. Il motivo è che un'istanza **CircularString** archivia segmenti di arco circolare e non segmenti di linea. Di conseguenza, i lati del triangolo archiviati nell'istanza **CircularString** sono ABC, CDE ed EFA, mentre i lati del triangolo archiviati nell'istanza **LineString** sono AC, CE ed EA.  

Si consideri l'esempio descritto di seguito.  

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LS LengthCS Length
5.65685...6.28318...
```

Le istanze **CircularString** usano un numero minore di punti per archiviare i limiti delle curve con maggiore precisione delle istanze **LineString**. Le istanze**CircularString** sono ideali per l'archiviazione di limiti circolari come un raggio cercato di venti miglia da un punto specifico. Le istanze**LineString** sono ideali per l'archiviazione di limiti lineari come un blocco urbano quadrato.  

### <a name="linestring-and-compoundcurve-comparison"></a>Confronto tra LineString e CompoundCurve  
Negli esempi di codice seguenti viene illustrato come archiviare la stessa figura utilizzando istanze **LineString** e **CompoundCurve** :

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

Negli esempi precedenti un'istanza **LineString** o un'istanza **CompoundCurve** potrebbe archiviare la figura.  Nell'esempio seguente viene utilizzata un'istanza **CompoundCurve** per archiviare una sezione di un grafico a torta:  

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  

Un'istanza **CompoundCurve** consente di archiviare direttamente il segmento di arco circolare (2 2, 1 3, 0 2), mentre con un'istanza **LineString** è necessario convertire la curva in diversi segmenti di linea più piccoli.  

### <a name="circularstring-and-compoundcurve-comparison"></a>Confronto tra CircularString e CompoundCurve  
Nell'esempio di codice seguente viene illustrata l'archiviazione di una sezione di un grafico a torta in un'istanza **CircularString** :  

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

Per archiviare la sezione del grafico a torta utilizzando un'istanza **CircularString** , è necessario utilizzare tre punti per ogni segmento di linea.  Se un punto intermedio non è noto, deve essere calcolato oppure è necessario raddoppiare l'endpoint del segmento di linea, come illustrato nel frammento di codice seguente:  

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

Le istanze**CompoundCurve** consentono componenti sia **LineString** sia **CircularString** , in modo che solo due punti nei segmenti di linea della sezione del grafico a torta debbano essere noti.  In questo esempio di codice viene illustrato come utilizzare un'istanza **CompoundCurve** per archiviare la stessa figura:  
```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Confronto tra Polygon e CurvePolygon  
Le istanze**CurvePolygon** possono utilizzare istanze **CircularString** e **CompoundCurve** instances when defining their exterior e interior rings.  Le istanze **Polygon** non possono usare i tipi di segmento di arco circolare: **CircularString** e **CompoundCurve**.  

## <a name="see-also"></a>Vedere anche  
- [Dati spaziali (SQL Server)](https://msdn.microsoft.com/library/bb933790.aspx) 
- [Guida di riferimento ai metodi per il tipo di dati geometry](https://msdn.microsoft.com/library/bb933973.aspx) 
- [Guida di riferimento ai metodi per il tipo di dati geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)   
- [STNumCurves &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
- [STNumCurves &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)   
- [STGeomFromText &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)   
- [STGeomFromText &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
