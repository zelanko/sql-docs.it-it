---
title: Panoramica dei tipi di dati spaziali | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 9ae74640557f7906ed237341d147926eb3296614
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014051"
---
# <a name="spatial-data-types-overview"></a>Panoramica dei tipi di dati spaziali
  Esistono due tipi di dati spaziali. Il tipo di dati `geometry` supporta dati planari o euclidei (terra piatta). Il tipo di dati `geometry` è conforme a Open Geospatial Consortium (OGC) Simple Features for SQL Specification versione 1.1.0 e a SQL MM (standard ISO).  
  
 Inoltre, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta il tipo di dati `geography`, che archivia dati ellissoidali (terra rotonda), ad esempio coordinate di latitudine e longitudine GPS.  
  
> [!IMPORTANT]  
>  Per una descrizione dettagliata e alcuni esempi delle funzionalità spaziali introdotte in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], tra cui i miglioramenti apportati ai tipi di dati spaziali, scaricare il white paper [Nuove funzionalità spaziali di SQL Server, nome in codice "Denali"](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
##  <a name="objects"></a> Oggetti dati spaziali  
 I tipi di dati `geometry` e `geography` supportano sedici oggetti dati spaziali o tipi di istanza. Solo per undici di questi tipi di istanza, tuttavia, è possibile *creare istanze*. È possibile creare e usare queste istanze (o crearne un'istanza) in un database. Queste istanze derivano determinate proprietà dai relativi tipi di dati padre che distinguono come `Points`, **LineStrings, CircularStrings**, `CompoundCurves`, `Polygons`, `CurvePolygons` o come più `geometry`oppure `geography` le istanze in un `GeometryCollection`. Il tipo `Geography` dispone di un tipo di istanza aggiuntivo, `FullGlobe`.  
  
 Nella figura seguente viene illustrata la gerarchia `geometry` sulla quale si basano i tipi di dati `geometry` e `geography`. I tipi di istanziabile `geometry` e `geography` sono indicati in blu.  
  
 ![Gerarchia del tipo di geometria](../../database-engine/media/geom-hierarchy.gif "gerarchia del tipo di geometria")  
  
 Come indicato nella figura, i dieci tipi istanziabili del `geometry` e `geography` sono tipi di dati `Point`, `MultiPoint`, `LineString`, `CircularString`, `MultiLineString`, `CompoundCurve`, `Polygon`, `CurvePolygon`, `MultiPolygon`, e `GeometryCollection`. Vi è un tipo aggiuntivo di cui è possibile creare istanze per il tipo di dati geography, ovvero `FullGlobe`. Il `geometry` e `geography` tipi possono riconoscere un'istanza specifica purché si tratta di un'istanza con formato corretto, anche se l'istanza non è definito in modo esplicito. Ad esempio, se si definisce una `Point` in modo esplicito usando il metodo stpointfromtext (), dell'istanza `geometry` e `geography` riconoscono l'istanza come un `Point`, purché l'input del metodo sia ben formato. Se si definisce la stessa istanza utilizzando il metodo `STGeomFromText()`, entrambi i tipi di dati `geometry` e `geography` riconoscono l'istanza come `Point`.  
  
 I sottotipi per i tipi geometry e geography sono divisi in tipi semplici e di raccolta.  Alcuni metodi come `STNumCurves()` possono essere utilizzati solo con tipi semplici.  
  
 I tipi semplici includono:  
  
-   [Point](../spatial/point.md)  
  
-   [LineString](../spatial/linestring.md)  
  
-   [CircularString](../spatial/circularstring.md)  
  
-   [CompoundCurve](../spatial/compoundcurve.md)  
  
-   [Poligono](../spatial/polygon.md)  
  
-   [CurvePolygon](../spatial/curvepolygon.md)  
  
 I tipi di raccolta includono:  
  
-   [MultiPoint](../spatial/multipoint.md)  
  
-   [MultiLineString](../spatial/multilinestring.md)  
  
-   [MultiPolygon](../spatial/multipolygon.md)  
  
-   [GeometryCollection](../spatial/geometrycollection.md)  
  
  
##  <a name="differences"></a> Differenze tra i tipi di dati geometry e geography  
 I due tipi di dati spaziali si comportano spesso in modo simile, ma esistono alcune differenze fondamentali nel modo in cui i dati vengono archiviati e modificati.  
  
### <a name="how-connecting-edges-are-defined"></a>Definizione dei bordi di collegamento  
 I dati di definizione per i tipi `LineString` e `Polygon` sono solo vertici.  Il bordo di collegamento tra due vertici in un tipo geometry è una linea retta.  Tuttavia, il bordo di collegamento tra due vertici in un tipo geografico è un corto arco di grande ellissi tra i due vertici.  Una grande ellisse è l'intersezione dell'ellissoide con un piano attraverso il centro e un arco di grande ellisse è un segmento di arco sulla grande ellisse.  
  
### <a name="how-circular-arc-segments-are-defined"></a>Definizione di segmenti di arco circolare  
 I segmenti di arco circolare per i tipi geometry vengono definiti sul piano delle coordinate cartesiane XY (i valori Z vengono ignorati). I segmenti di arco circolare per i tipi geography vengono definiti da segmenti di curva su una sfera di riferimento. Qualsiasi parallelo sulla sfera di riferimento può essere definito da due archi circolari complementari in cui i punti per entrambi gli archi hanno un angolo di latitudine costante.  
  
### <a name="measurements-in-spatial-data-types"></a>Misurazioni nei tipi di dati spaziali  
 Nel sistema planare, o terra piatta, le misurazioni delle distanze e delle aree vengono fornite nella stessa unità di misurazione delle coordinate. Utilizzando il tipo di dati `geometry`, la distanza tra (2, 2) e (5, 6) è 5 unità, indipendentemente dalle unità utilizzate.  
  
 Nel sistema ellissoidale, o terra rotonda, le coordinate sono fornite in gradi di latitudine e longitudine. Tuttavia, le lunghezze e le aree sono misurate generalmente in metri e metri quadrati, sebbene la misurazione possa dipendere dall'identificatore di riferimento spaziale (SRID) dell'istanza `geography`. L'unità di misurazione più comune per il tipo di dati `geography` è il metro.  
  
### <a name="orientation-of-spatial-data"></a>Orientamento dei dati spaziali  
 Nel sistema planare l'orientamento dell'anello di un poligono non è un fattore di particolare rilevanza. Ad esempio, un poligono descritto da ((0, 0), (10, 0), (0, 20), (0, 0)) è identico al poligono descritto da ((0, 0), (0, 20), (10, 0), (0, 0)). OGC Simple Features for SQL Specification non indica un ordinamento dell'anello e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non impone tale ordinamento.  
  
 In un sistema ellissoidale, un poligono non ha significato, o è ambiguo, senza un orientamento. Ad esempio, un anello intorno all'equatore descrive l'emisfero nord o sud? Se si utilizza il tipo di dati `geography` per archiviare l'istanza spaziale, è necessario specificare l'orientamento dell'anello e descrivere accuratamente la posizione dell'istanza. L'interno del poligono in un sistema ellissoidale è definito dal lato sinistro della regola.  
  
 Quando il livello di compatibilità è 100 o minore di nel [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] il `geography` tipo di dati presenta le restrizioni seguenti:  
  
-   Ogni istanza `geography` deve adattarsi all'interno di un singolo emisfero. Non è possibile archiviare oggetti spaziali con dimensioni maggiori di un emisfero.  
  
-   Qualsiasi istanza `geography` di una rappresentazione Well-Known Text (WKT) o Well-Known Binary (WKB) OCG che produca un oggetto più grande di un emisfero genera una `ArgumentException`.  
  
-   Il `geography` metodi che richiedono l'input di due tipi di dati `geography` istanze, ad esempio stintersection (), stunion (), stdifference () e stsymdifference (), restituiranno null se i risultati dei metodi non rientrano in un singolo emisfero. Anche STBuffer() restituirà Null se l'output supera un singolo emisfero.  
  
 In [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]`FullGlobe` è un tipo speciale di Polygon che copre l'intero globo. `FullGlobe` dispone di un'area, ma non ha bordi o vertici.  
  
### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>Anelli interni ed esterni non rilevanti nel tipo di dati geography  
 OGC Simple Features for SQL Specification vengono trattati anelli esterni e interni, ma questa distinzione non ha molto senso il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `geography` del tipo di dati; qualsiasi anello di un poligono può essere considerato l'anello esterno.  
  
 Per ulteriori informazioni sulle specifiche OGC, vedere quanto riportato di seguito:  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](https://go.microsoft.com/fwlink/?LinkId=93627)  
  
-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options](https://go.microsoft.com/fwlink/?LinkId=93628) (Specifiche OGC, accesso semplificato alle caratteristiche Parte 2 - Opzioni SQL)  
  
  
##  <a name="circular"></a> Segmenti di arco circolare  
 Tre tipi di cui è possibile creare istanze possono accettare segmenti di arco circolare: `CircularString`, `CompoundCurve` e `CurvePolygon`.  Un segmento di arco circolare è definito da tre punti in un piano bidimensionale. Il terzo punto non può corrispondere al primo punto.  
  
 Nelle figure A e B vengono illustrati segmenti di arco circolare tipici. Si noti come ognuno dei tre punti giace sul perimetro di un cerchio.  
  
 Nelle figure C e D viene illustrato come un segmento di linea possa essere definito segmento di arco circolare.  Si noti che sono ancora necessari tre punti per definire il segmento di arco circolare, diversamente da un segmento di linea regolare, che può essere definito solo da due punti.  
  
 I metodi che operano sui tipi di segmento di arco circolare utilizzano segmenti di linea retta per simulare l'arco circolare. Il numero di segmenti di linea utilizzati per simulare l'arco dipenderanno dalla lunghezza e dalla curvatura dell'arco. Benché sia possibile archiviare i valori Z per ognuno dei tipi di segmento di arco circolare, i metodi non utilizzeranno i valori Z nei calcoli.  
  
> [!NOTE]  
>  Se si specificano valori Z per segmenti di arco circolare, tali valori devono essere gli stessi per tutti i punti nel segmento di arco circolare perché questo venga accettato per l'input. Ad esempio, `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` è ammesso, mentre `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` non lo è.  
  
### <a name="linestring-and-circularstring-comparison"></a>Confronto tra LineString e CircularString  
 Nel diagramma seguente vengono illustrati triangoli isosceli identici. Nel triangolo A vengono utilizzati segmenti di linea per definire il triangolo, mentre nel triangolo B vengono utilizzati segmenti di arco circolare.  
  
 ![](../../database-engine/media/7e382f76-59da-4b62-80dc-caf93e637c14.png "7e382f76-59da-4b62-80dc-caf93e637c14")  
  
 In questo esempio viene illustrato come archiviare i triangoli isosceli precedenti utilizzando un'istanza `LineString` e un'istanza `CircularString`:  
  
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
  
 Si noti che un'istanza `CircularString` richiede sette punti per definire il triangolo, mentre un'istanza `LineString` richiede solo quattro punti. Il motivo è che un'istanza `CircularString` archivia segmenti di arco circolare e non segmenti di linea. Di conseguenza, i lati del triangolo archiviati nell'istanza `CircularString` sono ABC, CDE ed EFA, mentre i lati del triangolo archiviati nell'istanza `LineString` sono AC, CE ed EA.  
  
 Si consideri il frammento di codice seguente:  
  
```sql  
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);  
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);  
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];  
```  
  
 Il frammento di codice produrrà i risultati seguenti:  
  
```  
LS LengthCS Length  
5.65685...6.28318...  
```  
  
 La figura seguente mostra come viene archiviato ogni tipo (linea rossa indica `LineString``@g1`blu, riga mostra `CircularString``@g2`):  
  
 ![](../../database-engine/media/e52157b5-5160-4a4b-8560-50cdcf905b76.png "e52157b5-5160-4a4b-8560-50cdcf905b76")  
  
 Come illustrato nella figura precedente, le istanze `CircularString` utilizzano un numero minore di punti per archiviare i limiti delle curve con maggiore precisione delle istanze `LineString`. Le istanze `CircularString` sono ideali per l'archiviazione di limiti circolari come un raggio cercato di venti miglia da un punto specifico. Le istanze `LineString` sono ideali per l'archiviazione di limiti lineari come un blocco urbano quadrato.  
  
### <a name="linestring-and-compoundcurve-comparison"></a>Confronto tra LineString e CompoundCurve  
 Negli esempi di codice seguenti viene illustrato come archiviare la stessa figura utilizzando istanze `LineString` e `CompoundCurve`:  
  
```sql  
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');  
```  
  
 o Gestione configurazione  
  
 Negli esempi precedenti un'istanza `LineString` o un'istanza `CompoundCurve` potrebbe archiviare la figura.  Nell'esempio seguente viene utilizzata un'istanza `CompoundCurve` per archiviare una sezione di un grafico a torta:  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  
  
 Un'istanza `CompoundCurve` consente di archiviare direttamente il segmento di arco circolare (2 2, 1 3, 0 2), mentre con un'istanza `LineString` è necessario convertire la curva in diversi segmenti di linea più piccoli.  
  
### <a name="circularstring-and-compoundcurve-comparison"></a>Confronto tra CircularString e CompoundCurve  
 Nell'esempio di codice seguente viene illustrata l'archiviazione di una sezione di un grafico a torta in un'istanza `CircularString`:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
SELECT @g.ToString(), @g.STLength();  
```  
  
 Per archiviare la sezione del grafico a torta utilizzando un'istanza `CircularString`, è necessario utilizzare tre punti per ogni segmento di linea.  Se un punto intermedio non è noto, deve essere calcolato oppure è necessario raddoppiare l'endpoint del segmento di linea, come illustrato nel frammento di codice seguente:  
  
```sql  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');  
```  
  
 `CompoundCurve` le istanze consentono entrambe `LineString` e `CircularString` componenti in modo che solo due punti nei segmenti di linea della sezione a torta debbano essere noti.  In questo esempio di codice viene illustrato come utilizzare un'istanza `CompoundCurve` per archiviare la stessa figura:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');  
SELECT @g.ToString(), @g.STLength();  
```  
  
### <a name="polygon-and-curvepolygon-comparison"></a>Confronto tra Polygon e CurvePolygon  
 Le istanze `CurvePolygon` possono utilizzare istanze `CircularString` e `CompoundCurve` per definire i relativi anelli esterni e interni.  Le istanze `Polygon` non possono utilizzare i tipi di segmento di arco circolare: `CircularString` e `CompoundCurve`.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [Guida di riferimento ai metodi per il tipo di dati geometry](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [Guida di riferimento ai metodi per il tipo di dati geography](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [STNumCurves &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stnumcurves-geometry-data-type)   
 [STNumCurves &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stnumcurves-geography-data-type)   
 [STGeomFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)   
 [STGeomFromText &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
  
