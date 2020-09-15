---
description: Colonne di tipo sparse
title: Colonne di tipo sparse | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 406f4fea8df9a3c410f126f5a766aeb2e1ad4bb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396297"
---
# <a name="sparse-columns"></a>Colonne di tipo sparse

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Le colonne di tipo sparse sono colonne comuni che dispongono di archiviazione ottimizzata per i valori Null. Tali colonne consentono di ridurre i requisiti di spazio per i valori Null aumentando tuttavia l'overhead per il recupero dei valori non Null. È consigliabile utilizzare colonne di tipo sparse quando la quantità di spazio risparmiata è compresa almeno tra il 20% e il 40%.

Il driver JDBC 3.0 per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta colonne di tipo sparse quando si connette a un server [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] (o versioni successive). È possibile utilizzare l'oggetto [SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md), l'oggetto [SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md) o l'oggetto [SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) per determinare quale colonna è di tipo sparse e quale quella del set di colonne.

Il file di codice per questo esempio è denominato SparseColumns.java e si trova nella seguente posizione:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\sparse  
```

I set di colonne sono colonne calcolate che restituiscono tutte le colonne di tipo sparse nel form XML non tipizzato. È necessario utilizzare i set di colonne quando il numero di colonne di una tabella è elevato o maggiore di 1024 o l'esecuzione di operazioni sulle singole colonne di tipo sparse risulta eccessivamente complessa. Un set di colonne può contenere fino a 30.000 colonne.

## <a name="example"></a>Esempio

### <a name="description"></a>Descrizione

In questo esempio viene illustrato come rilevare i set di colonne e come analizzare l'output XML di un set di colonne per ottenere dati dalle colonne di tipo sparse.

Il listato di codice è il codice sorgente Java. Prima di compilare l'applicazione, modificare la stringa di connessione.

### <a name="code"></a>Codice

```java
import java.io.StringReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.sql.Statement;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;

import org.w3c.dom.Document;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;
import org.xml.sax.InputSource;


public class SparseColumns {

    public static void main(String args[]) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {

            createColdCallingTable(stmt);

            // Determine the column set column
            String columnSetColName = null;
            String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";

            try (ResultSet rs = stmt.executeQuery(strCmd)) {
                if (rs.next()) {
                    columnSetColName = rs.getString(1);
                    System.out.println(columnSetColName + " is the column set column!");
                }
            }

            strCmd = "SELECT * FROM ColdCalling";
            try (ResultSet rs = stmt.executeQuery(strCmd)) {

                // Iterate through the result set
                ResultSetMetaData rsmd = rs.getMetaData();

                DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
                DocumentBuilder db = dbf.newDocumentBuilder();
                InputSource is = new InputSource();
                while (rs.next()) {
                    // Iterate through the columns
                    for (int i = 1; i <= rsmd.getColumnCount(); ++i) {
                        String name = rsmd.getColumnName(i);
                        String value = rs.getString(i);

                        // If this is the column set column
                        if (name.equalsIgnoreCase(columnSetColName)) {
                            System.out.println(name);

                            // Instead of printing the raw XML, parse it
                            if (value != null) {
                                // Add artificial root node "sparse" to ensure XML is well formed
                                String xml = "<sparse>" + value + "</sparse>";

                                is.setCharacterStream(new StringReader(xml));
                                Document doc = db.parse(is);

                                // Extract the NodeList from the artificial root node that was added
                                NodeList list = doc.getChildNodes();
                                Node root = list.item(0); // This is the <sparse> node
                                NodeList sparseColumnList = root.getChildNodes(); // These are the xml column nodes

                                // Iterate through the XML document
                                for (int n = 0; n < sparseColumnList.getLength(); ++n) {
                                    Node sparseColumnNode = sparseColumnList.item(n);
                                    String columnName = sparseColumnNode.getNodeName();
                                    // The column value is not in the sparseColumNode, it is the value of the
                                    // first child of it
                                    Node sparseColumnValueNode = sparseColumnNode.getFirstChild();
                                    String columnValue = sparseColumnValueNode.getNodeValue();

                                    System.out.println("\t" + columnName + "\t: " + columnValue);
                                }
                            }
                        } else { // Just print the name + value of non-sparse columns
                            System.out.println(name + "\t: " + value);
                        }
                    }
                    System.out.println();// New line between rows
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void createColdCallingTable(Statement stmt) throws SQLException {
        stmt.execute("if exists (select * from sys.objects where name = 'ColdCalling')" + "drop table ColdCalling");

        String sql = "CREATE TABLE ColdCalling  (  ID int IDENTITY(1,1) PRIMARY KEY,  [Date] date,  [Time] time,  PositiveFirstName nvarchar(50) SPARSE,  PositiveLastName nvarchar(50) SPARSE,  SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  );";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time])  VALUES ('10-13-09','07:05:24')  ";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  VALUES ('07-20-09','05:00:24', 'AA', 'B')  ";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  VALUES ('07-20-09','05:15:00', 'CC', 'DD')  ";
        stmt.execute(sql);
    }
}

```

## <a name="see-also"></a>Vedere anche

[Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
