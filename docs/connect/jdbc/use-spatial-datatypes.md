---
title: Usando tipi di dati spaziali | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d00692b0b5872b1020f900587a24a3116aee9be
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737012"
---
# <a name="using-spatial-datatypes"></a>Uso dei tipi di dati spaziali

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Tipi di dati spaziali (Geometry e Geography) sono supportate a partire la versione di anteprima del Driver JDBC 6.5.0. Tipi di dati spaziali non sono attualmente supportati con le stored procedure, la parametri con valori di tabella (TVP), BulkCopy e Always Encrypted. Questa pagina illustra che vari casi dei tipi di dati Geometry e Geography di utilizzo con il Driver JDBC. Per una panoramica sui tipi di dati spaziali, controllare [panoramica dei tipi di dati spaziali](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) pagina.

## <a name="creating-a-geometry--geography-object"></a>Creazione di una geometria / oggetto di geografia

Esistono due modi principali per creare una geometria / oggetto di geografia - conversione da un Well-Known Text WKT (WELL) né un Well-Known Binary (WKB).

### <a name="creating-from-wkt"></a>Creazione da WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Si creerà un oggetto di geometria LINESTRING con sistema identificatore SRID (Spatial Reference) 0 e un oggetto geografico con SRID 4326.

### <a name="creating-from-wkb"></a>Creazione da WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Si creerà un oggetto Geometry e Geography equivalente a quelli creati in precedenza dal WKT.

## <a name="working-with-a-geometry--geography-object"></a>Utilizzo di una geometria / oggetto di geografia

Supponendo che l'utente dispone di una tabella in SQL Server, come di seguito:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Uno script di esempio per inserire un valore di geometria sarebbe:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

Lo stesso può essere eseguito per la controparte di geografia, con una colonna di tipo geografia e **setGeography()** (metodo).

Per leggere una geometria / colonna di tipo geografia:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Lo stesso può essere eseguito per la controparte di geografia, con una colonna di tipo geografia e **getGeography()** (metodo).

## <a name="newly-introduced-apis"></a>API appena introdotte

Queste sono le nuove API pubbliche che sono state introdotte con questa aggiunta, nelle classi **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**e  **Geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Metodo|Descrizione|
|:------|:----------|
|setGeometry void (int n, Geometry x)| Imposta il parametro designato per l'oggetto della classe microsoft.sql.Geometry specificato.
|setGeography void (int n, Geography x)| Imposta il parametro designato per l'oggetto della classe microsoft.sql.Geography specificato.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Metodo|Descrizione|
|:------|:----------|
|Geometria getGeometry (colunIndex int)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto set di risultati come oggetto com.microsoft.sqlserver.jdbc.Geometry nel linguaggio di programmazione Java.
|Geometria getGeometry (columnName stringa)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto set di risultati come oggetto com.microsoft.sqlserver.jdbc.Geometry nel linguaggio di programmazione Java.
|Geography getGeography (colunIndex int)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto set di risultati come oggetto com.microsoft.sqlserver.jdbc.Geography nel linguaggio di programmazione Java.
|Geography getGeography (columnName stringa)| Restituisce il valore della colonna designata nella riga corrente di questo oggetto set di risultati come oggetto com.microsoft.sqlserver.jdbc.Geography nel linguaggio di programmazione Java.

### <a name="geometry"></a>Geometry

|Metodo|Descrizione|
|:------|:----------|
|Geometria STGeomFromText (wkt String, int SRID)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geometry STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geometry di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Geometrie deserializzare (byte [] Well-Known Binary)| Costruttore per un'istanza Geometry da un formato di SQL Server interno per i dati spaziali.
|Analisi della geometria (stringa wkt)| Costruttore per un'istanza Geometry da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Identificatore SRID è impostato sul valore predefinito 0.
|Punto di geometria (double x, y double, int SRID)| Costruttore per un'istanza di geometria che rappresenta un'istanza del punto dai relativi valori X e Y e un identificatore SRID.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary()| Restituisce la rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geometry. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geometry.
|hasM() booleano| Restituisce se l'oggetto contiene un valore M (misura).
|hasZ() booleano| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|GetX (Double)| Restituisce il valore della coordinata X.
|GetY (Double)| Restituisce il valore della coordinata Y.
|GetM() Double| Restituisce il valore M (misura) dell'oggetto.
|GetZ() Double| Restituisce il valore Z (innalzamento) dell'oggetto.
|int getSrid()| Restituisce il valore di identificatore di riferimento spaziale (SRID).
|boolean isNull()| Restituisce se l'oggetto Geometry è null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto di geometria.
|Stgeometrytype (stringa)| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geometria.
|Stringa Astextzm| Restituisce la rappresentazione Well-Known Text (WKT) dell'oggetto Geometry.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geometry.

### <a name="geography"></a>Geography

|Metodo|Descrizione|
|:------|:----------|
|STGeomFromText Geography (wkt String, int SRID)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) integrata con qualsiasi valore Z (innalzamento) e M (misura) appartenente all'istanza.
|Geography STGeomFromWKB(byte[] wkb)| Costruttore per un'istanza Geography di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
|Geography deserializzare (byte [] Well-Known Binary)| Costruttore per un'istanza di geografia da un formato di SQL Server interno per i dati spaziali.
|Analisi di geografia WKT (Well stringa)| Costruttore per un'istanza Geography da una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium). Identificatore SRID è impostato sul valore predefinito 0.
|Punto geografico (lon, lat double, int SRID doppio)| Costruttore per un'istanza Geography che rappresenta un'istanza Point dalla latitudine e longitudine e un identificatore SRID.
|String STAsText()| Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza Geography. Il testo non conterrà alcun valore Z (innalzamento) o M (misura) appartenente all'istanza.
|byte[] STAsBinary())| Restituisce una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium) di un'istanza Geography. Il valore non conterrà alcun valore Z o M appartenente all'istanza.
|byte[] serialize()| Restituisce i byte che rappresentano un formato SQL Server interno di tipo Geography.
|hasM() booleano| Restituisce se l'oggetto contiene un valore M (misura).
|hasZ() booleano| Restituisce se l'oggetto contiene un valore Z (innalzamento).
|Double getLatitude()| Restituisce il valore di latitudine.
|GetLongitude() Double| Restituisce il valore di longitudine.
|GetM() Double| Restituisce il valore M (misura) dell'oggetto.
|GetZ() Double| Restituisce il valore Z (innalzamento) dell'oggetto.
|int getSrid()| Restituisce il valore di identificatore di riferimento spaziale (SRID).
|boolean isNull()| Restituisce se l'oggetto di geografia è null.
|int STNumPoints()| Restituisce il numero di punti nell'oggetto di geografia.
|String STGeographyType()| Restituisce il nome del tipo OGC (Open Geospatial Consortium) rappresentato da un'istanza di geografia.
|Stringa Astextzm| Restituisce la rappresentazione Well-Known Text (WKT) dell'oggetto Geografia.
|String toString()| Restituisce la rappresentazione stringa dell'oggetto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitazioni dei tipi di dati spaziali

1. La sub-datatypes spaziale **CircularString**, **CompoundCurve**, **CurvePolygon**, e **FullGlobe** sono supportati solo avvio da SQL Server 2012 e versioni successive.

2. Always Encrypted non è utilizzabile con tipi di dati spaziali.

3. Stored procedure, TVP e BulkCopy operazioni non sono attualmente supportate con tipi di dati spaziali.

## <a name="see-also"></a>Vedere anche

[Esempio di tipi di dati spaziali (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
