---
title: Uso dei tipi di dati spaziali | Microsoft Docs
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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026938"
---
# <a name="using-spatial-datatypes"></a>Uso dei tipi di dati spaziali

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

I tipi di dati spaziali (Geometry e Geography) sono supportati a partire dalla versione di anteprima di JDBC Driver 6.5.0. I tipi di dati spaziali non sono attualmente supportati con stored procedure, TVP (Table Valued Parameter, parametri con valori di tabella), copia bulk e Always Encrypted. Questa pagina illustra diversi casi d'uso dei tipi di dati Geometry e Geography con JDBC Driver. Per una panoramica dei tipi di dati spaziali, vedere [Panoramica dei tipi di dati spaziali](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview).

## <a name="creating-a-geometry--geography-object"></a>Creazione di un oggetto Geometry/Geography

Esistono due modi principali per creare un oggetto Geometry/Geography. È possibile conversione da WKT (well-known text) o da WKB (well-known binary).

### <a name="creating-from-wkt"></a>Creazione da WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Verrà creato un oggetto Geometry LINESTRING con identificatore SRID 0 (Spatial Reference System Identifier) e un oggetto Geography con identificatore SRID 4326.

### <a name="creating-from-wkb"></a>Creazione da WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Verrà creato un oggetto Geometry e Geography equivalente a quelli creati in precedenza da WKT.

## <a name="working-with-a-geometry--geography-object"></a>Uso di un oggetto Geometry/Geography

Si supponga che l'utente disponga di una tabella in SQL Server come riportato di seguito:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Di seguito un script di esempio per inserire un valore Geometry:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

È possibile eseguire la stessa operazione per la controparte Geography, usando una colonna Geography e il metodo **setGeography()** .

Per leggere una colonna Geometry/Geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

È possibile eseguire la stessa operazione per la controparte Geography, usando una colonna Geography e il metodo **getGeography()** .

## <a name="newly-introduced-apis"></a>Nuove API introdotte

Nelle classi **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry** e **Geography** sono state aggiunte le nuove API pubbliche riportate di seguito.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Metodo|Descrizione|
|:------|:----------|
|void setGeometry(int n, Geometry x)| Imposta il parametro designato per l'oggetto classe microsoft.sql.Geometry.
|void setGeography(int n, Geography x)| Imposta il parametro designato per l'oggetto classe microsoft.sql.Geography.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Metodo|Descrizione|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com.microsoft.sqlserver.jdbc.Geometry nel linguaggio di programmazione Java.
|Geometry getGeometry(String columnName)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com.microsoft.sqlserver.jdbc.Geometry nel linguaggio di programmazione Java.
|Geography getGeography(int colunIndex)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com.microsoft.sqlserver.jdbc.Geography nel linguaggio di programmazione Java.
|Geography getGeography(String columnName)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto ResultSet come oggetto com.microsoft.sqlserver.jdbc.Geography nel linguaggio di programmazione Java.

### <a name="geometry"></a>Geometry

|Metodo|Descrizione|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geometry STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geometry di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Geometries deserialize(byte[] wkb)| Costruttore per un'istanza Geometry da un formato di SQL Server interno per dati spaziali.
|Geometry parse(String wkt)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Il valore predefinito per l'identificatore SRID è 0.
|Geometry point(double x, double y, int SRID)| Costruttore per un'istanza Geometry che rappresenta un'istanza Point dai relativi valori X e Y e un identificatore SRID.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary()| Restituisce la rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geometry.
|boolean hasM()| Restituisce se l'oggetto contiene un valore M (misura).
|boolean hasZ()| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|Double getX()| Restituisce il valore della coordinata X.
|Double getY()| Restituisce il valore della coordinata Y.
|Double getM()| Restituisce il valore M (misura) dell'oggetto .
|Double getZ()| Restituisce il valore Z (innalzamento) dell'oggetto .
|int getSrid()| Restituisce il valore dell'identificatore SRID.
|boolean isNull()| Restituisce se l'oggetto Geometry è Null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto Geometry.
|String STGeometryType()| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geometria.
|String asTextZM()| Restituisce la rappresentazione WKT (well-known text) dell'oggetto Geometry.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geometry.

### <a name="geography"></a>Area geografica

|Metodo|Descrizione|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geography STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geography di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Geography deserialize(byte[] wkb)| Costruttore per un'istanza Geography da un formato di SQL Server interno per dati spaziali.
|Geography parse(String wkt)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Il valore predefinito per l'identificatore SRID è 0.
|Geography point(double lon, double lat, int SRID)| Costruttore per un'istanza Geography che rappresenta un'istanza Point dalla latitudine e longitudine e un identificatore SRID.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geography. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary())| Restituisce una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geography. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geography.
|boolean hasM()| Restituisce se l'oggetto contiene un valore M (misura).
|boolean hasZ()| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|Double getLatitude()| Restituisce il valore di latitudine.
|Double getLongitude()| Restituisce il valore di longitudine.
|Double getM()| Restituisce il valore M (misura) dell'oggetto.
|Double getZ()| Restituisce il valore Z (innalzamento) dell'oggetto.
|int getSrid()| Restituisce il valore dell'identificatore SRID.
|boolean isNull()| Restituisce se l'oggetto Geography è Null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto Geography.
|String STGeographyType()| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geografia.
|String asTextZM()| Restituisce la rappresentazione WKT (well-known text) dell'oggetto Geography.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitazioni dei tipi di dati spaziali

1. I tipi di dati spaziali secondari **CircularString**, **CompoundCurve**, **CurvePolygon** e **FullGlobe** sono supportati solo a partire da SQL Server 2012 e versioni successive.

2. Non è possibile usare Always Encrypted con i tipi di dati spaziali.

3. Stored procedure, TVP e operazioni di copia bulk non sono attualmente supportati con i tipi di dati spaziali.

## <a name="see-also"></a>Vedere anche

[Esempio di tipi di dati spaziali (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
