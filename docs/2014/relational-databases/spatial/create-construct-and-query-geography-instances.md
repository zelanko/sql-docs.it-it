---
title: Creare, costruire ed eseguire query di istanze geografiche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5dde7575a3f657b89d29fefa0da52002bcd6af28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014301"
---
# <a name="create-construct-and-query-geography-instances"></a>Creare, Costruire e Istanze geografiche di Query
  Il tipo di dati spaziali geografici, `geography`, rappresenta i dati in un sistema di coordinate terrestri. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è implementato come tipo di dati CLR (Common Language Runtime) .NET. Il tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` consente di archiviare dati ellissoidali (terra rotonda), ad esempio coordinate di latitudine e longitudine GPS.  
  
 Il tipo `geography` è predefinito e disponibile in ogni database. È possibile creare colonne di tabella di tipo `geography` e utilizzare dati `geography` nello stesso modo in cui verrebbero utilizzati gli altri tipi forniti dal sistema.  
  
##  <a name="creating"></a>Creazione o costruzione di una nuova istanza geography  
  
###  <a name="existing"></a>Creazione di una nuova istanza geography da un'istanza esistente  
 Il tipo di dati `geography` offre molti metodi predefiniti che è possibile utilizzare per creare nuove istanze `geography` in base a quelle esistenti.  
  
 **Per creare un buffer intorno a una geografia**  
 [Tipo di dati STBuffer &#40;geography&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **Per creare un buffer intorno a una geografia, consentendo una tolleranza**  
 [Tipo di dati BufferWithTolerance &#40;geography&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **Per creare una geografia dall'intersezione di due istanze geography**  
 [Tipo di dati STIntersection &#40;geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Per creare una geografia dall'Unione di due istanze geography**  
 [Tipo di dati di STUnion &#40;geography&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **Per creare una geografia dai punti in cui una geografia non si sovrappone a un'altra**  
 [Tipo di dati STDifference &#40;geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a>Costruzione di un'istanza geography da un input di testo ben noto  
 Il tipo di dati `geography` fornisce diversi metodi predefiniti che generano una geografia dalla rappresentazione WKT Open Geospatial Consortium (OGC). Lo standard WKT è una stringa di testo che consente ai dati geografici di essere scambiati in formato testuale.  
  
 **Per costruire qualsiasi tipo di istanza geography dall'input WKT**  
 [STGeomFromText &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [Analizza &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **Per costruire un'istanza geografica Point dall'input WKT**  
 [Tipo di dati STPointFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **Per costruire un'istanza geografica MultiPoint dall'input WKT**  
 [Tipo di dati STMPointFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **Per costruire un'istanza geografica LineString dall'input WKT**  
 STLineFromText (tipo di dati geography)  
  
 **Per costruire un'istanza geografica MultiLineString dall'input WKT**  
 [Tipo di dati STMLineFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **Per costruire un'istanza geografica Polygon dall'input WKT**  
 [Tipo di dati STPolyFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **Per costruire un'istanza geografica MultiPolygon dall'input WKT**  
 [Tipo di dati STMPolyFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **Per costruire un'istanza geografica GeometryCollection dall'input WKT**  
 [Tipo di dati STGeomCollFromText &#40;geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a>Creazione di un'istanza geography da un input binario noto  
 WKB è un formato binario specificato da OGC che consente di scambiare dati `Geography` tra un'applicazione client e un database SQL. Le seguenti funzioni accettano l'input WKB per costruire le istanze geografiche:  
  
 **Per costruire qualsiasi tipo di istanza geography da un input WKB**  
 [Tipo di dati STGeomFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica Point dall'input WKB**  
 [Tipo di dati STPointFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica MultiPoint dall'input WKB**  
 [Tipo di dati STMPointFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica LineString dall'input WKB**  
 [Tipo di dati STLineFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica MultiLineString da un input WKB**  
 [Tipo di dati STMLineFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica Polygon dall'input WKB**  
 [Tipo di dati STPolyFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica MultiPolygon dall'input WKB**  
 [Tipo di dati STMPolyFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **Per costruire un'istanza geografica GeometryCollection dall'input WKB**  
 [Tipo di dati STGeomCollFromWKB &#40;geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type) STGeomCollFromWKB (tipo di dati geography)  
  
###  <a name="gml"></a>Costruzione di un'istanza geography da un input di testo GML  
 Il `geography` tipo di dati fornisce un metodo che genera `geography` un'istanza da GML, una rappresentazione XML di `geography` un'istanza. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta un subset di GML.  
  
 Per altre informazioni su Geography Markup Language (GML), vedere la specifica OGC [OGC Specifications, Geography Markup Language](https://go.microsoft.com/fwlink/?LinkId=93629)(Specifiche OGC, Geography Markup Language).  
  
 **Per costruire qualsiasi tipo di istanza geography dall'input GML**  
 [Tipo di dati GeomFromGML &#40;geography&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a>Restituzione di un testo noto e di un file binario noto da un'istanza geography  
 È possibile utilizzare i metodi seguenti per restituire il formato WKT o WKB di un'istanza `geography`:  
  
 **Per restituire la rappresentazione WKT di un'istanza geography**  
 [Tipo di dati STAsText &#40;geography&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [Tipo di dati ToString &#40;geography&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **Per restituire la rappresentazione WKT di un'istanza geography, inclusi i valori Z e M**  
 [AsTextZM &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **Per restituire la rappresentazione WKB di un'istanza geography**  
 [Tipo di dati STAsBinary &#40;geography&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **Per restituire una rappresentazione GML di un'istanza geography**  
 [Tipo di dati AsGml &#40;geography&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a>Esecuzione di query sulle proprietà e i comportamenti delle istanze geography  
 Tutte `geography` le istanze hanno un certo numero di proprietà che possono essere recuperate [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite metodi disponibili in. Negli argomenti seguenti vengono definite le proprietà e i comportamenti dei tipi di geografia, nonché i metodi per l'esecuzione di query per ognuno di essi.  
  
###  <a name="valid"></a>Informazioni sulla validità, sul tipo di istanza e su GeometryCollection  
 Dopo aver costruito un'istanza `geography`, è possibile utilizzare i seguenti metodi per restituire il tipo di istanza oppure, se si tratta di un'istanza `GeometryCollection`, restituire un'istanza `geography` specifica.  
  
 **Per restituire il tipo di istanza di una geografia**  
 [STGeometryType &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **Per determinare se una geografia è un tipo di istanza specificato**  
 [Tipo di dati InstanceOf &#40;geography&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **Per determinare se un'istanza geography è ben formata per il tipo di istanza**  
 [Tipo di dati STNumGeometries &#40;geography&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **Per restituire una specifica geografia in un'istanza GeometryCollection**  
 [Tipo di dati STGeometryN &#40;geography&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type) STGeometryN (tipo di dati geography)  
  
###  <a name="number"></a>Numero di punti  
 Tutte le istanze `geography` non vuote sono costituite da *punti*. che rappresentano le coordinate di latitudine e longitudine terrestri sulle quali vengono tracciate le istanze `geography`. Il tipo di dati `geography` fornisce numerosi metodi predefiniti per l'esecuzione di query sui punti di un'istanza.  
  
 **Per restituire il numero di punti che comprendono un'istanza**  
 [STNumPoints &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **Per restituire un punto specifico in un'istanza**  
 [STPointN &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Per restituire il punto di inizio di un'istanza**  
 [Tipo di dati STStartPoint &#40;geography&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **Per restituire il punto di fine di un'istanza**  
 [Tipo di dati STEndpoint &#40;geography&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a>Dimensione  
 Un'istanza `geography` non vuota può essere a 0, 1 o 2 dimensioni. Le istanze con `geography` dimensione zero, ad esempio `MultiPoint`e, non hanno lunghezza o area. `Point` Gli oggetti unidimensionali, ad esempio `LineString, CircularString`, `CompoundCurve` e `MultiLineString`, dispongono della lunghezza. Le istanze bidimensionali, ad esempio `Polygon, CurvePolygon` e `MultiPolygon`, dispongono di area e lunghezza. Le istanze vuote indicano una dimensione di -1 e `GeometryCollection` indica le dimensioni massime del contenuto.  
  
 **Per restituire la dimensione di un'istanza**  
 [Tipo di dati STDimension &#40;geography&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **Per restituire la lunghezza di un'istanza**  
 [STLength &#40;tipo di dati geography&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **Per restituire l'area di un'istanza**  
 [Tipo di dati STArea &#40;geography&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a>Vuoto  
 Un'istanza *vuota* `geography` non contiene punti. La lunghezza delle istanze vuote `LineString, CircularString`, `CompoundCurve` e `MultiLineString` è 0. L'area delle istanze vuote `Polygon, CurvePolygon` and `MultiPolygon` è 0.  
  
 **Per determinare se un'istanza è vuota**  
 [Tipo di dati STIsEmpty &#40;geography&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a>Chiusura  
 Un'istanza *chiusa* `geography` è una figura i cui punti di inizio e di fine sono gli stessi. Le istanze `Polygon` sono considerate chiuse. Le istanze `Point` non sono considerate chiuse.  
  
 Un anello è un'istanza `LineString` semplice chiusa.  
  
 **Per determinare se un'istanza è chiusa**  
 [Tipo di dati STIsClosed &#40;geography&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **Per restituire il numero di anelli in un'istanza Polygon**  
 [Tipo di dati NumRings &#40;geography&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **Per restituire un anello specificato di un'istanza geography**  
 [Tipo di dati RingN &#40;geography&#41;](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a>ID di riferimento spaziale (SRID)  
 L'identificatore SRID specifica in quale sistema di coordinate ellissoidali è rappresentata l'istanza `geography`. Non è possibile confrontare due istanze `geography` con identificatori SRID diversi.  
  
 **Per impostare o restituire l'identificatore SRID di un'istanza**  
 [Tipo di dati STSrid &#40;geography&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 Questa proprietà può essere modificata.  
  
##  <a name="rel"></a>Determinazione delle relazioni tra istanze geography  
 Il tipo di dati `geography` offre molti metodi predefiniti che è possibile utilizzare per determinare relazioni tra due istanze `geography`.  
  
 **Per determinare se due istanze includono lo stesso punto impostato**  
 [STEquals &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Per determinare se due istanze sono disgiunte**  
 [STDisjoint &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Per determinare se due istanze si intersecano**  
 [STIntersects &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Per determinare il punto o i punti in cui due istanze si intersecano**  
 [Tipo di dati STIntersection &#40;geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Per determinare la distanza più breve tra punti in due istanze geography**  
 [STDistance &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **Per determinare la differenza in termini di punti tra due istanze geography**  
 [Tipo di dati STDifference &#40;geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **Per derivare la differenza simmetrica o i punti univoci di un'istanza geography rispetto a un'altra istanza**  
 [Tipo di dati STSymDifference &#40;geography&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a>le istanze geography devono usare SRID supportato  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta gli identificatori SRID basati sugli standard EPSG. È necessario utilizzare un identificatore SRID supportato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze `geography` se si eseguono calcoli o si utilizzano metodi con dati spaziali di geografia. L'identificatore SRID deve corrispondere a uno di quelli visualizzati nella vista del catalogo **sys.spatial_reference_systems** Come indicato in precedenza, quando si eseguono i calcoli sui dati spaziali utilizzando il tipo di dati `geography` i risultati dipenderanno dal tipo di ellissoide utilizzato nella creazione dei dati, in quanto a ogni ellissoide è assegnato un identificatore SRID specifico.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza l'identificatore predefinito SRID di 4326., che esegue il mapping al sistema di riferimento spaziale WHS 84 in caso si utilizzino metodi nelle istanze `geography`. Se si utilizzano dati da un sistema di riferimento spaziale diverso da WGS 84 (o SRID 4326), sarà necessario determinare lo specifico identificatore SRID per i dati spaziali geografici.  
  
##  <a name="examples"></a> Esempi  
 Negli esempi seguenti viene illustrato come aggiungere ed eseguire query su dati geography.  
  
-   Nel primo esempio viene creata una tabella con una colonna di identità e una colonna `geography``GeogCol1`. Una terza colonna effettua il rendering della colonna `geography` nella rappresentazione Well-Known Text (WKT) OGC (Open Geospatial Consortium) e utilizza il metodo `STAsText()` . Vengono quindi inserite due righe: in una riga è contenuta un'istanza `LineString` di `geography`e in una seconda è contenuta un'istanza `Polygon` .  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeogCol1 geography,   
        GeogCol2 AS GeogCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
    GO  
    ```  
  
-   Nel secondo esempio viene utilizzato il metodo `STIntersection()` per restituire i punti in cui si intersecano le due istanze `geography` inserite in precedenza.  
  
    ```  
    DECLARE @geog1 geography;  
    DECLARE @geog2 geography;  
    DECLARE @result geography;  
  
    SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geog1.STIntersection(@geog2);  
    SELECT @result.STAsText();  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
