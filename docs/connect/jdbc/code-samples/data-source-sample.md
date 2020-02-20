---
title: Esempio di origine dati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c1ad1118b6576a5740f7c5a0f36309d39736407
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028345"
---
# <a name="data-source-sample"></a>Esempio di origine dati

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Con questa applicazione di esempio [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] viene illustrato come connettersi a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando un oggetto origine dati. Viene inoltre illustrato come recuperare dati da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando una stored procedure.

Il file di codice per questo esempio è denominato ConnectDataSource.java ed è disponibile nel percorso seguente:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisiti

Per eseguire questa applicazione di esempio, è necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. È anche necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Per altre informazioni su come impostare il classpath, vedere [Uso del driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Esempio

Nell'esempio seguente il codice imposta le varie proprietà di connessione usando i metodi di impostazione dell'oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md), quindi esegue la chiamata al metodo [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) dell'oggetto SQLServerDataSource per restituire un oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).

Il codice di esempio usa quindi il metodo [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) dell'oggetto SQLServerConnection per creare un oggetto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) e viene eseguita la chiamata al metodo [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) per l'esecuzione della stored procedure.

Infine, viene usato l'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) restituito dal metodo executeQuery per scorrere i risultati restituiti dalla stored procedure.

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(Integer.parseInt("<port>"));
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
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

[Connessione e recupero dei dati](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
