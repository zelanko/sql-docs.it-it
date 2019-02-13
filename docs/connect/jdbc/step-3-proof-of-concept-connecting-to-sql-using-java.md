---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL tramite Java | Microsoft Docs'
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1504a348-1774-47ab-8967-288ec3985ae4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 305be93a342b66a18cae6de4f60ba9efa98e1738
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736902"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-java"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite Java
  
In questo esempio deve essere considerato un modello di verifica solo. Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  
  
## <a name="step-1--connect"></a>Passaggio 1: connettersi  
  
Usare la classe di connessione per connettersi al Database SQL.   
  
```java  
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class SQLDatabaseConnection {
    // Connect to your database.
    // Replace server name, username, and password with your credentials
    public static void main(String[] args) {
        String connectionUrl =
                "jdbc:sqlserver://yourserver.database.windows.net:1433;"
                        + "database=AdventureWorks;"
                        + "user=yourusername@yourserver;"
                        + "password=yourpassword;"
                        + "encrypt=true;"
                        + "trustServerCertificate=false;"
                        + "loginTimeout=30;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);) {
            // Code here.
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```  
  
## <a name="step-2-execute-a-query"></a>Passaggio 2: Eseguire una query  
In questo esempio, connettersi al Database SQL di Azure, eseguire un'istruzione SELECT e restituire le righe selezionate.   
  
```java  
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class SQLDatabaseConnection {

    // Connect to your database.
    // Replace server name, username, and password with your credentials
    public static void main(String[] args) {
        String connectionUrl =
                "jdbc:sqlserver://yourserver.database.windows.net:1433;"
                + "database=AdventureWorks;"
                + "user=yourusername@yourserver;"
                + "password=yourpassword;"
                + "encrypt=true;"
                + "trustServerCertificate=false;"
                + "loginTimeout=30;";

        ResultSet resultSet = null;

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Create and execute a SELECT SQL statement.
            String selectSql = "SELECT TOP 10 Title, FirstName, LastName from SalesLT.Customer";
            resultSet = statement.executeQuery(selectSql);

            // Print results from select statement
            while (resultSet.next()) {
                System.out.println(resultSet.getString(2) + " " + resultSet.getString(3));
            }
        }
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```  
  
## <a name="step-3-insert-a-row"></a>Passaggio 3: Inserire una riga  
In questo esempio, eseguire un'istruzione INSERT, passare i parametri e recuperare il valore di chiave primaria generata automaticamente.   
  
```java  
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;

public class SQLDatabaseConnection {

    // Connect to your database.
    // Replace server name, username, and password with your credentials
    public static void main(String[] args) {
        String connectionUrl =
                "jdbc:sqlserver://yourserver.database.windows.net:1433;"
                        + "database=AdventureWorks;"
                        + "user=yourusername@yourserver;"
                        + "password=yourpassword;"
                        + "encrypt=true;"
                        + "trustServerCertificate=false;"
                        + "loginTimeout=30;";

        String insertSql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES "
                + "('NewBike', 'BikeNew', 'Blue', 50, 120, '2016-01-01');";

        ResultSet resultSet = null;

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                PreparedStatement prepsInsertProduct = connection.prepareStatement(insertSql, Statement.RETURN_GENERATED_KEYS);) {

            prepsInsertProduct.execute();
            // Retrieve the generated key from the insert.
            resultSet = prepsInsertProduct.getGeneratedKeys();

            // Print the ID of the inserted row.
            while (resultSet.next()) {
                System.out.println("Generated: " + resultSet.getString(1));
            }
        }
        // Handle any errors that may have occurred.
        catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```  
  
## <a name="additional-samples"></a>Esempi aggiuntivi  
[Applicazioni di esempio del driver JDBC](../../connect/jdbc/sample-jdbc-driver-applications.md)
