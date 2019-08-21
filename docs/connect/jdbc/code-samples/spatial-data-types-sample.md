---
title: Esempio di tipi di dati spaziali | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2f56ed8036602357f8128b0426fbb90c0bab801
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028275"
---
# <a name="spatial-data-types-sample"></a>Esempio di tipi di dati spaziali

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Questa [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] applicazione di esempio illustra come creare, inserire e recuperare i tipi di dati spaziali (Geometry e geography).
  
Il file di codice per questo esempio è denominato SpatialDataTypes.java e si trova nella seguente posizione:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>Requisiti  

Per eseguire questa applicazione di esempio, è necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. Per ulteriori informazioni su come impostare il classpath, vedere [utilizzo del driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Esempio

Nell'esempio seguente, il codice di esempio crea una tabella denominata SpatialDataTypesTable_JDBC_Sample che contiene le colonne ' Geometry ' è Geography '.

Nell'esempio vengono prima creati oggetti ' Geometry ' è Geography ' da un WKT (Well-Known-Text) che rappresenta un punto. Usa un SQLServerPreparedStatement con una query con parametri per eseguire il mapping dei dati a ogni colonna di conseguenza.

Infine, l'esempio inserisce i dati nella tabella e li recupera. I dati vengono visualizzati sotto forma di WKT.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import com.microsoft.sqlserver.jdbc.Geography;
import com.microsoft.sqlserver.jdbc.Geometry;
import com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement;
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class SpatialDataTypes {

    private static String tableName = "SpatialDataTypesTable_JDBC_Sample";

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";
        // Establish the connection.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            dropAndCreateTable(stmt);

            // TODO: Implement Sample code
            String geoWKT = "POINT(3 40 5 6)";
            Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
            Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);

            try (SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) con
                    .prepareStatement("insert into " + tableName + " values (?, ?)");) {
                pstmt.setGeometry(1, geomWKT);
                pstmt.setGeography(2, geogWKT);
                pstmt.execute();

                SQLServerResultSet rs = (SQLServerResultSet) stmt.executeQuery("select * from " + tableName);
                rs.next();

                System.out.println("Geometry data: " + rs.getGeometry(1));
                System.out.println("Geography data: " + rs.getGeography(2));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void dropAndCreateTable(Statement stmt) throws SQLException {
        stmt.executeUpdate("if object_id('" + tableName + "','U') is not null" + " drop table " + tableName);

        stmt.executeUpdate("Create table " + tableName + " (c1 geometry, c2 geography)");
    }
}
```

## <a name="see-also"></a>Vedere anche  

[Uso dei tipi di dati &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)  
  
