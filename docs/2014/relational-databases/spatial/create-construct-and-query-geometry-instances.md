---
title: Creare, costruire ed eseguire query di istanze di geometria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8daff4753eb5921ee80eef8f44de96487ea86a15
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374853"
---
# <a name="create-construct-and-query-geometry-instances"></a>Creazione, costruzione e query di istanze geometry
  Il tipo di dati spaziali planare, `geometry`, rappresenta i dati in un sistema di coordinate euclideo (piano). Questo tipo è implementato come tipo di dati CLR (Common Language Runtime) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Il tipo `geometry` è predefinito e disponibile in ogni database. È possibile creare colonne di tabella di tipo `geometry` e operare sui dati `geometry` nello stesso modo in cui si utilizzano gli altri tipi CLR.  
  
 Il tipo di dati `geometry` (planare) supportato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è conforme allo standard Open Geospatial Consortium (OGC) Simple Features for SQL Specification versione 1.1.0.  
  
 Per ulteriori informazioni sulle specifiche OGC, vedere quanto riportato di seguito:  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC Specifications, Simple Feature Access Part 2 - SQL Options](https://go.microsoft.com/fwlink/?LinkId=93629) (Specifiche OGC, accesso semplificato alle caratteristiche Parte 2 - Opzioni SQL)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta un subset dello standard GML 3.1 esistente che viene definito nello schema seguente: [https://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](https://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating"></a> Creazione o costruzione di una nuova istanza geometry  
  
###  <a name="existing"></a> Creazione di una nuova istanza geometry da un'istanza esistente  
 Il tipo di dati `geometry` offre molti metodi predefiniti che è possibile utilizzare per creare nuove istanze `geometry` in base a quelle esistenti.  
  
 **Per creare un buffer relativo a una geometria**  
 [STBuffer &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stbuffer-geometry-data-type)  
  
 [BufferWithTolerance &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type)  
  
 **Per creare una versione semplificata di una geometria**  
 [Reduce &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/reduce-geometry-data-type)  
  
 **Per creare la struttura convessa di una geometria**  
 [STConvexHull &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stconvexhull-geometry-data-type)  
  
 **Per creare una geometria dall'intersezione di due geometrie**  
 [STIntersection &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stintersection-geometry-data-type)  
  
 **Per creare una geometria dall'unione di due geometrie**  
 [STUnion &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stunion-geometry-data-type)  
  
 **Per creare una geometria dai punti in cui una non si sovrappone all'altra**  
 [STDifference &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stdifference-geometry-data-type)  
  
 **Per creare una geometria dai punti in cui due geometrie non si sovrappongono**  
 [STSymDifference &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stsymdifference-geometry-data-type)  
  
 **Per creare un'istanza Point arbitraria che giace su una geometria esistente**  
 [STPointOnSurface &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
  
  
###  <a name="wkt"></a> Costruzione di un'istanza geometry da un input WKT (well-known text)  
 Il tipo di dati `geometry` fornisce molti metodi predefiniti che generano una geometria dalla rappresentazione WKT OGC (Open Geospatial Consortium). Lo standard WKT è una stringa di testo che consente lo scambio di dati geometrici in formato testuale.  
  
 **Per costruire qualsiasi tipo di istanza geometry da input WKT**  
 [STGeomFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)  
  
 [Parse &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/parse-geometry-data-type)  
  
 **Per costruire un'istanza di geometria Point dall'input WKT**  
 [STPointFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromtext-geometry-data-type)  
  
 **Per costruire un'istanza MultiPoint di tipo geometry da un input WKT**  
 [STMPointFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromtext-geometry-data-type)  
  
 **Per costruire un'istanza LineString di tipo geometry da un input WKT**  
 [STLineFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromtext-geometry-data-type)  
  
 **Per costruire un'istanza MultiLineString di tipo geometry da un input WKT**  
 [STMLineFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromtext-geometry-data-type)  
  
 **Per costruire un'istanza Polygon di tipo geometry da un input WKT**  
 [STPolyFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromtext-geometry-data-type)  
  
 **Per costruire un'istanza MultiPolygon di tipo geometry da un input WKT**  
 [STMPolyFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type)  
  
 **Per costruire un'istanza GeometryCollection di tipo geometry da un input WKT**  
 [STGeomCollFromText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type)  
  
  
  
###  <a name="wkb"></a> Costruzione di un'istanza geometry da un input WKB (well-known binary)  
 WKB è un formato binario definito da OGC (Open Geospatial Consortium) che consente di scambiare i dati `geometry` tra un'applicazione client e un database SQL. Le funzioni seguenti accettano input WKB per costruire le geometrie:  
  
 **Per costruire qualsiasi tipo di istanza geometry da un input WKB**  
 [STGeomFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type)  
  
 **Per costruire un'istanza Point di tipo geometry da un input WKB**  
 [STPointFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromwkb-geometry-data-type)  
  
 **Per costruire un'istanza MultiPoint di tipo geometry da un input WKB**  
 [STMPointFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type)  
  
 **Per costruire un'istanza LineString di tipo geometry da un input WKB**  
 [STLineFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromwkb-geometry-data-type)  
  
 **Per costruire un'istanza MultiLineString di tipo geometry da un input WKB**  
 [STMLineFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type)  
  
 **Per costruire un'istanza Polygon di tipo geometry da un input WKB**  
 [STPolyFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type)  
  
 **Per costruire un'istanza MultiPolygon di tipo geometry da un input WKB**  
 [STMPolyFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type)  
  
 **Per costruire un'istanza GeometryCollection di tipo geometry da un input WKB**  
 [STGeomCollFromWKB &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type)  
  
  
  
###  <a name="gml"></a> Costruzione di un'istanza geometry da un input di testo GML  
 Il `geometry` tipo di dati fornisce un metodo che genera un `geometry` istanza da GML, una rappresentazione XML di oggetti geometrici. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta un subset di GML.  
  
 **Per costruire qualsiasi tipo di istanza geometry da un input GML**  
 [GeomFromGml &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/geomfromgml-geometry-data-type)  
  
  
  
##  <a name="returning"></a> Restituzione di WKT e WKB da un'istanza geometry  
 È possibile utilizzare i metodi seguenti per restituire il formato WKT o WKB di un'istanza `geometry`:  
  
 **Per restituire la rappresentazione WKT di un'istanza geometry**  
 [STAsText &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stastext-geometry-data-type)  
  
 [ToString &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/tostring-geometry-data-type)  
  
 **Per restituire la rappresentazione WKT di un'istanza geometry, con qualsiasi valore Z e M.**  
 [AsTextZM &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/astextzm-geometry-data-type)  
  
 **Per restituire la rappresentazione WKB di un'istanza geometry**  
 [STAsBinary &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stasbinary-geometry-data-type)  
  
 **Per restituire la rappresentazione GML di un'istanza geometry**  
 [AsGml &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/asgml-geometry-data-type)  
  
  
  
##  <a name="querying"></a> Esecuzione di query sulle proprietà e i comportamenti delle istanze geometry  
 Tutti i `geometry` istanze hanno un numero di proprietà che possono essere recuperate tramite metodi che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce. Negli argomenti seguenti vengono definiti le proprietà e i comportamenti dei tipi di geometria, nonché i metodi per l'esecuzione di query per ognuno di essi.  
  
###  <a name="valid"></a> Informazioni sulla validità, sul tipo di istanza e su GeometryCollection  
 Dopo aver costruito un'istanza `geometry`, è possibile utilizzare i metodi seguenti per determinare se essa è corretta, per restituire il tipo di istanza o, se si tratta di un'istanza di raccolta, per restituire un'istanza `geometry` specifica.  
  
 **Per restituire il tipo di istanza di una geometria**  
 [STGeometryType &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeometrytype-geometry-data-type)  
  
 **Per determinare se una geometria è un tipo di istanza specificato**  
 [InstanceOf &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/instanceof-geometry-data-type)  
  
 **Per determinare se un'istanza geometry è corretta per il tipo di istanza**  
 [STIsValid &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
 **Per convertire un'istanza geometry in un'istanza geometry corretta con un tipo di istanza**  
 [MakeValid &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
  
 **Per restituire il numero delle geometrie in un'istanza GeometryCollection**  
 [STNumGeometries &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stnumgeometries-geometry-data-type)  
  
 Per restituire una specifica geometria in un'istanza GeometryCollection  
 [STGeometryN &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stgeometryn-geometry-data-type)STGeometryN (tipo di dati geometry)  
  
  
  
###  <a name="number"></a> Numero di punti  
 Tutti non vuoti `geometry` sono costituite da istanze *punti*. Tali punti rappresentano le coordinate X e Y del piano su cui vengono tracciate le geometrie. Il tipo di dati `geometry` offre numerosi metodi predefiniti per l'esecuzione di query sui punti di un'istanza.  
  
 **Per restituire il numero di punti che comprendono un'istanza**  
 [STNumPoints &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
  
 **Per restituire un punto specifico in un'istanza**  
 [STPointN](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Per restituire un punto arbitrario che si trova in un'istanza**  
 [STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
 **Per restituire il punto di inizio di un'istanza**  
 [STStartPoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)  
  
 **Per restituire il punto di fine di un'istanza**  
 [STEndpoint](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
  
 **Per restituire la coordinata X di un'istanza Point**  
 [STX &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)  
  
 **Per restituire la coordinata Y di un'istanza Point**  
 [STY](/sql/t-sql/spatial-geometry/sty-geometry-data-type)  
  
 **Per restituire il punto centrale geometrico di un'istanza Polygon, CurvePolygon o MultiPolygon**  
 [STCentroid](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)  
  
  
  
###  <a name="dimension"></a> Dimensione  
 Un'istanza `geometry` non vuota può essere a 0, 1 o 2 dimensioni. Le istanze `geometries` senza dimensioni, ad esempio `Point` e `MultiPoint` non dispongono di lunghezza o area. Gli oggetti unidimensionali, ad esempio `LineString, CircularString, CompoundCurve` e `MultiLineString`, dispongono della lunghezza. Le istanze bidimensionali, ad esempio `Polygon`, `CurvePolygon` e `MultiPolygon`, dispongono di area e lunghezza. Per le istanze vuote verrà indicata una dimensione di -1 e per `GeometryCollection` verrà indicata un'area dipendente dai tipi del contenuto.  
  
 **Per restituire la dimensione di un'istanza**  
 [STDimension](/sql/t-sql/spatial-geometry/stdimension-geometry-data-type)  
  
 **Per restituire la lunghezza di un'istanza**  
 [STLength](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
  
 **Per restituire l'area di un'istanza**  
 [STArea](/sql/t-sql/spatial-geometry/starea-geometry-data-type)  
  
  
  
###  <a name="empty"></a> Vuoto  
 Un' *vuote* `geometry` istanza non contiene punti. La lunghezza delle istanze `LineString, CircularString`, `CompoundCurve` e `MultiLineString` vuote è pari a zero. L'area delle istanze `Polygon`, `CurvePolygon` e `MultiPolygon` vuote è pari a 0.  
  
 **Per determinare se un'istanza è vuota**  
 [STIsEmpty](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type).  
  
  
  
###  <a name="simple"></a> Simple  
 Per un `geometry` dell'istanza sia *semplice*, deve soddisfare entrambi questi requisiti:  
  
-   Ogni figura dell'istanza non deve intersecarsi, salvo agli endpoint.  
  
-   Le figure dell'istanza non possono intersecarsi tra di loro in un punto non esistente in entrambi i loro limiti.  
  
> [!NOTE]  
>  Le geometrie vuote sono sempre semplici.  
  
 **Per determinare se un'istanza è semplice**  
 [STIsSimple](/sql/t-sql/spatial-geometry/stissimple-geometry-data-type).  
  
  
  
###  <a name="boundary"></a> Limite interno ed esterno  
 Il *interni* di un `geometry` istanza è lo spazio occupato dall'istanza e il *esterno* è lo spazio non occupato da essa.  
  
 Il*limite* è definito da OGC come segue:  
  
-   Le istanze `Point` e `MultiPoint` non hanno un limite.  
  
-   I limiti `LineString` e `MultiLineString` sono formati dai punti di inizio e di fine, rimuovendo quelli che si hanno per un numero di volte pari.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 Il limite di un'istanza `Polygon` o `MultiPolygon` è il set dei suoi anelli.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Per restituire il limite di un'istanza**  
 [STBoundary](/sql/t-sql/spatial-geometry/stboundary-geometry-data-type)  
  
  
  
###  <a name="envelope"></a> Envelope  
 Il *busta* di un `geometry` , noto anche come istanza di *rettangolo delimitatore*, è il rettangolo allineato all'asse formato dal valore minimo e coordina le massime (X, Y) dell'istanza.  
  
 **Per restituire l'envelope di un'istanza**  
 [STEnvelope](/sql/t-sql/spatial-geometry/stenvelope-geometry-data-type)  
  
  
  
###  <a name="closure"></a> Chiusura  
 Oggetto *chiusa* `geometry` istanza è una figura i cui punti di inizio e di punti di fine corrispondono. Le istanze `Polygon` sono considerate chiuse. Le istanze `Point` non sono considerate chiuse.  
  
 Un anello è un'istanza `LineString` semplice chiusa.  
  
 **Per determinare se un'istanza è chiusa**  
 [STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
  
 **Per determinare se un'istanza è un anello**  
 [STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
  
 **Per restituire l'anello esterno di un'istanza Polygon**  
 [STExteriorRing](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)  
  
 **Per restituire il numero di anelli interni in un'istanza Polygon**  
 [STNumInteriorRing](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)  
  
 **Per restituire un anello interno specificato di un'istanza Polygon**  
 [STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)  
  
  
  
###  <a name="srid"></a> Identificatore SRID  
 L'identificatore SRID specifica in quale sistema di coordinate è rappresentata l'istanza `geometry`. Due istanze con identificatori SRID diversi non possono essere confrontate.  
  
 **Per impostare o restituire l'identificatore SRID di un'istanza**  
 [STSrid](/sql/t-sql/spatial-geometry/stsrid-geometry-data-type)  
  
 Questa proprietà può essere modificata.  
  
  
  
##  <a name="rel"></a> Determinazione delle relazioni esistenti tra istanze geometry  
 Il tipo di dati `geometry` offre molti metodi predefiniti che è possibile utilizzare per determinare relazioni tra due istanze `geometry`.  
  
 **Per determinare se due istanze includono lo stesso punto impostato**  
 [STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Per determinare se due istanze sono disgiunte**  
 [STDisjoint](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Per determinare se due istanze si intersecano**  
 [STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Per determinare se due istanze entrano in contatto**  
 [STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)  
  
 **Per determinare se due istanze si sovrappongono**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Per determinare se due istanze si incrociano**  
 [STCrosses](/sql/t-sql/spatial-geometry/stcrosses-geometry-data-type)  
  
 **Per determinare se un'istanza è all'interno dell'altra**  
 [STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)  
  
 **Per determinare se un'istanza contiene l'altra**  
 [STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)  
  
 **Per determinare se un'istanza si sovrappone all'altra**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Per determinare se due istanze sono collegate a livello spaziale**  
 [STRelate](/sql/t-sql/spatial-geometry/strelate-geometry-data-type)  
  
 **Per determinare la distanza più breve tra punti in due geometrie**  
 [STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
  
  
##  <a name="defaultsrid"></a> Istanze geometry con SRID zero per impostazione predefinita  
 L'identificatore SRID predefinito per le istanze `geometry` in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è 0. Con i dati spaziali `geometry` lo specifico identificatore SRID dell'istanza spaziale non deve eseguire i calcoli. Di conseguenza le istanze possono risiedere nello spazio planare indefinito. Per indicare lo spazio planare indefinito nei calcoli di metodi del tipo di dati `geometry`, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizza SRID 0.  
  
##  <a name="examples"></a> Esempi  
 Nei due esempi seguenti viene illustrato come aggiungere ed eseguire query su dati di tipo geometry.  
  
-   Nel primo esempio viene creata una tabella con una colonna di identità e una colonna `geometry``GeomCol1`. Una terza colonna effettua il rendering della colonna `geometry` nella rappresentazione Well-Known Text (WKT) OGC (Open Geospatial Consortium) e utilizza il metodo `STAsText()`. Vengono quindi inserite due righe: in una riga è contenuta un'istanza `LineString` di `geometry`e in una seconda è contenuta un'istanza `Polygon` .  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeomCol1 geometry,   
        GeomCol2 AS GeomCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
    GO  
    ```  
  
-   Nel secondo esempio viene utilizzato il metodo `STIntersection()` per restituire i punti in cui si intersecano le due istanze `geometry` inserite in precedenza.  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
