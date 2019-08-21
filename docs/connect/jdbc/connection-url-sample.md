---
title: Esempio di URL di connessione | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a74757846f14b2cee6f8d68cfdec87a02ded4c5
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028140"
---
# <a name="connection-url-sample"></a>Esempio di URL di connessione

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Con questa applicazione di esempio [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] viene illustrato come connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un URL di connessione. Viene inoltre illustrato come recuperare i dati da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un'istruzione SQL.

Il file di codice per questo esempio è ConnectURL.java ed è disponibile nel seguente percorso:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. È anche necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Per ulteriori informazioni su come impostare il classpath, vedere [utilizzo del driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Esempio

Nell'esempio seguente il codice di esempio imposta le varie proprietà di connessione nell'URL della connessione, quindi esegue una chiamata al metodo getConnection della classe DriverManager per restituire un oggetto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Il codice di esempio usa quindi il metodo [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) dell'oggetto SQLServerConnection per creare un oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) e viene eseguita la chiamata al metodo [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) per l'esecuzione dell'istruzione SQL.

Infine, viene usato l'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) restituito dal metodo executeQuery per scorrere i risultati restituiti dall'istruzione SQL.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>Vedere anche

[Connessione e recupero dei dati](../../connect/jdbc/connecting-and-retrieving-data.md)
