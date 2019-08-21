---
title: Esempio di modifica dei dati del set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 51e13941945a1be2d3ad1f02ce61fda98696f275
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027965"
---
# <a name="modifying-result-set-data-sample"></a>Esempio di modifica dei dati dei set di risultati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa applicazione di esempio [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dimostra come recuperare un set aggiornabile di dati da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usando quindi i metodi dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) viene inserita, modificata e infine eliminata una riga di dati dal set di dati.

Il file di codice per questo esempio è denominato UpdateResultSet.java ed è disponibile nel percorso seguente:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. È anche necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Per ulteriori informazioni su come impostare il classpath, vedere [utilizzo del driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Esempio

Nell'esempio seguente, mediante il codice di esempio viene eseguita una connessione al database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] di esempio. Quindi, usando un'istruzione SQL con l'oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), viene eseguita l'istruzione SQL e i dati restituiti vengono posizionati in un oggetto SQLServerResultSet aggiornabile.

Il codice di esempio usa quindi il metodo [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) per spostare il cursore del set di risultati nella riga di inserimento, usa una serie di metodi [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) per inserire i dati nella nuova riga ed esegue la chiamata al metodo [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) per rendere permanente la nuova riga di dati nel database.

Dopo aver inserito la nuova riga di dati, il codice di esempio usa un'istruzione SQL per recuperare la riga precedentemente inserita, quindi usa la combinazione dei metodi updateString e [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) per aggiornare la riga di dati e renderla di nuovo permanente nel database.

Infine, recupera la riga di dati precedentemente aggiornata e la elimina dal database usando il metodo [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md).

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

            // Insert a row of data.
            rs.moveToInsertRow();
            rs.updateString("Name", "Accounting");
            rs.updateString("GroupName", "Executive General and Administration");
            rs.updateString("ModifiedDate", "08/01/2006");
            rs.insertRow();

            // Retrieve the inserted row of data and display it.
            SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";
            rs = stmt.executeQuery(SQL);
            displayRow("ADDED ROW", rs);

            // Update the row of data.
            rs.first();
            rs.updateString("GroupName", "Finance");
            rs.updateRow();

            // Retrieve the updated row of data and display it.
            rs = stmt.executeQuery(SQL);
            displayRow("UPDATED ROW", rs);

            // Delete the row of data.
            rs.first();
            rs.deleteRow();
            System.out.println("ROW DELETED");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}
```

## <a name="see-also"></a>Vedere anche

[Uso dei set di risultati](../../connect/jdbc/working-with-result-sets.md)
