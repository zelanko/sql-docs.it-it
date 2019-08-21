---
title: Utilizzo di tipi di tipo di spazio Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026938"
---
# <a name="using-spatial-datatypes"></a>Uso dei tipi di dati spaziali

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

I tipi di databases spaziali (Geometry e geography) sono supportati dall'avvio della versione di anteprima del driver JDBC 6.5.0. I tipi di valori spaziali non sono attualmente supportati con le stored procedure, i parametri con valori di tabella (TVP), BulkCopy e Always Encrypted. In questa pagina vengono illustrati i diversi casi d'uso dei tipi di dati geometry e geography con il driver JDBC. Per una panoramica sui tipi di dati spaziali, vedere la pagina [Panoramica dei tipi di dati spaziali](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) .

## <a name="creating-a-geometry--geography-object"></a>Creazione di un oggetto Geometry/geography

Esistono due modi principali per creare un oggetto Geometry/geography: è possibile eseguire la conversione da un testo noto (WKT) o un well-known binary (WKB).

### <a name="creating-from-wkt"></a>Creazione da WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Verrà creato un oggetto Geometry LINESTRING con SRID (Spatial Reference System Identifier) e un oggetto geography con SRID 4326.

### <a name="creating-from-wkb"></a>Creazione da WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Verrà creato un oggetto Geometry e geography equivalente a quelli creati in precedenza da WKT.

## <a name="working-with-a-geometry--geography-object"></a>Uso di un oggetto Geometry/geography

Supponendo che l'utente disponga di una tabella SQL Server come riportato di seguito:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Uno script di esempio per inserire un valore geometrico sarà:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

È possibile eseguire la stessa operazione per la controparte Geography, usando una colonna geography e il metodo **segeography ()** .

Per leggere una colonna geometry/geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

È possibile eseguire la stessa operazione per la controparte Geography, usando una colonna geography e il metodo **GetGeography ()** .

## <a name="newly-introduced-apis"></a>API appena introdotte

Queste sono le nuove API pubbliche introdotte con questa aggiunta, nelle classi **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**e **geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Metodo|Descrizione|
|:------|:----------|
|void segeometry (int n, Geometry x)| Imposta il parametro designato sull'oggetto classe Microsoft. SQL. Geometry specificato.
|void segeography (int n, geography x)| Imposta il parametro designato sull'oggetto classe Microsoft. SQL. Geography specificato.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Metodo|Descrizione|
|:------|:----------|
|Geometry GetGeometry (int colunIndex)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com. Microsoft. SqlServer. JDBC. Geometry nel linguaggio di programmazione Java.
|Geometry GetGeometry (String columnName)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com. Microsoft. SqlServer. JDBC. Geometry nel linguaggio di programmazione Java.
|Geography GetGeography (int colunIndex)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com. Microsoft. SqlServer. JDBC. Geography nel linguaggio di programmazione Java.
|Geography GetGeography (String columnName)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com. Microsoft. SqlServer. JDBC. Geography nel linguaggio di programmazione Java.

### <a name="geometry"></a>Geometry

|Metodo|Descrizione|
|:------|:----------|
|Geometry STGeomFromText (String WKT, int SRID)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geometry STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geometry di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Geometrie deserializzate (byte [] WKB)| Costruttore per un'istanza geometry da un formato di SQL Server interno per i dati spaziali.
|Analisi Geometry (String WKT)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Per impostazione predefinita, l'identificatore di riferimento spaziale è 0.
|Punto di geometria (double x, double y, int SRID)| Costruttore per un'istanza geometry che rappresenta un'istanza Point dai relativi valori X e Y e da un identificatore di riferimento spaziale.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary()| Restituisce la rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geometry.
|hasM booleano ()| Restituisce se l'oggetto contiene un valore M (misura).
|hasZ booleano ()| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|Doppio I GetX ()| Restituisce il valore della coordinata X.
|Doppio getY ()| Restituisce il valore della coordinata Y.
|Doppio getM ()| Restituisce il valore M (misura) dell'oggetto.
|Doppio getZ ()| Restituisce il valore Z (innalzamento) dell'oggetto.
|int getSrid()| Restituisce il valore SRID (Spatial Reference Identifier).
|boolean isNull()| Restituisce se l'oggetto Geometry è null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto Geometry.
|Stringa STGeometryType ()| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geometria.
|Stringa asTextZM ()| Restituisce la rappresentazione Well-Known Text (WKT) dell'oggetto Geometry.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geometry.

### <a name="geography"></a>Geography

|Metodo|Descrizione|
|:------|:----------|
|Geography STGeomFromText (String WKT, int SRID)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geography STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geography di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Deserializzazione Geography (byte [] WKB)| Costruttore per un'istanza geography da un formato di SQL Server interno per i dati spaziali.
|Analisi geografia (String WKT)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Per impostazione predefinita, l'identificatore di riferimento spaziale è 0.
|Punto geografico (doppio Lon, doppio Lat, int SRID)| Costruttore per un'istanza Geography che rappresenta un'istanza Point dalla latitudine e longitudine e un identificatore SRID.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geography. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary())| Restituisce una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geography. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geography.
|hasM booleano ()| Restituisce se l'oggetto contiene un valore M (misura).
|hasZ booleano ()| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|Double getLatitude()| Restituisce il valore di latitudine.
|Doppia getlongitudine ()| Restituisce il valore della longitudine.
|Doppio getM ()| Restituisce il valore M (misura) dell'oggetto.
|Doppio getZ ()| Restituisce il valore Z (innalzamento) dell'oggetto.
|int getSrid()| Restituisce il valore SRID (Spatial Reference Identifier).
|boolean isNull()| Restituisce se l'oggetto geography è null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto geography.
|String STGeographyType()| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geografia.
|Stringa asTextZM ()| Restituisce la rappresentazione Well-Known Text (WKT) dell'oggetto geography.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitazioni dei tipi di DataType spaziali

1. I tipi di elementi secondari spaziali **CircularString**, **CompoundCurve**, **CurvePolygon**e **FullGlobe** sono supportati solo a partire da SQL Server 2012 e versioni successive.

2. Non è possibile usare Always Encrypted con i tipi di i tipi di tipo Spatial.

3. Le operazioni di stored procedure, TVP e BulkCopy non sono attualmente supportate con i tipi di tipo Spatial.

## <a name="see-also"></a>Vedere anche

[Esempio di tipi di dati spaziali (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
