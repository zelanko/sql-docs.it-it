---
title: Esempio di memorizzazione nella cache dei dati dei set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33998300281a274067a0879775dc33c9d7635471
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028408"
---
# <a name="caching-result-set-data-sample"></a>Esempio di memorizzazione nella cache dei dati dei set di risultati

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Con questa applicazione di esempio [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] viene illustrato come recuperare un set di dati di grandi dimensioni da un database e quindi controllare il numero di righe di dati memorizzate nella cache del client usando il metodo [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
> La limitazione del numero di righe inserite nella cache del client è un'operazione diversa dalla limitazione del numero totale di righe contenute in un set di risultati. Per controllare il numero totale di righe contenute in un set di risultati, usare il metodo [setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), ereditato dagli oggetti [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
Per impostare un limite per il numero di righe memorizzate nella cache del client, è prima necessario usare un cursore lato server quando si crea uno degli oggetti Statement specificando esplicitamente il tipo di cursore da usare durante la creazione dell'oggetto Statement. Ad esempio, nel driver JDBC è disponibile il tipo di cursore TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, ovvero un cursore lato server di sola lettura, fast forward only, da usare con i database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Un'alternativa all'utilizzo del tipo di cursore specifico per SQL Server è l'utilizzo della proprietà della stringa di connessione selectMethod, impostandone il valore su "cursor". Per altre informazioni sui tipi di cursore supportati dal driver JDBC, vedere [Informazioni sui tipi di cursore](../../../connect/jdbc/understanding-cursor-types.md).  
  
Dopo che è stata eseguita la query nell'oggetto Statement e dopo che al client sono stati restituiti i dati come set di risultati, è possibile chiamare il metodo setFetchSize per controllare la quantità dei dati recuperati contemporaneamente dal database. Ad esempio, se si dispone di una tabella che contiene 100 righe di dati e si imposta su 10 la dimensione del recupero, verranno inserite nella cache del client solo 10 righe di dati in qualsiasi momento. In questo modo verrà ridotta la velocità di elaborazione dei dati, ma si otterrà il vantaggio di utilizzare una quantità inferiore di memoria nel client, il che può risultare particolarmente utile quando si elaborano grandi quantità di dati.  
  
Il file di codice per questo esempio è CacheResultSet.java, disponibile nel percorso seguente:  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets  
```

## <a name="requirements"></a>Requisiti  

Per eseguire questa applicazione di esempio, è necessario impostare il classpath in modo da includere il file con estensione jar mssql-jdbc. È anche necessario accedere al database di esempio di [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Per altre informazioni su come impostare il classpath, vedere [Uso del driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
> Con [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sono inclusi file di libreria di classi mssql-jdbc da usare a seconda delle impostazioni Java Runtime Environment (JRE) preferite. Per altre informazioni su quale file JAR scegliere, vedere [Requisiti di sistema per il driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  

## <a name="example"></a>Esempio  

Nell'esempio seguente, mediante il codice di esempio viene eseguita una connessione al database [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] di esempio. Viene quindi usata un'istruzione SQL con l'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), viene specificato il tipo di cursore lato server, quindi viene eseguita l'istruzione SQL e i dati restituiti vengono collocati in un oggetto SQLServerResultSet.  
  
Il codice di esempio esegue quindi una chiamata al metodo timerTest personalizzato, passando come argomenti la dimensione di recupero da usare e il set di risultati. Il metodo timerTest imposta quindi la dimensione di recupero del set di risultati tramite il metodo setFetchSize, imposta l'ora di inizio del test e quindi scorre il set di risultati con un ciclo `While`. Non appena terminato il ciclo `While`, viene impostata l'ora di fine del test e quindi viene visualizzato il risultato del test stesso con le dimensioni di recupero, il numero di righe elaborate e il tempo impiegato per l'esecuzione.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheResultSet {

    @SuppressWarnings("serial")
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            for (int n : new ArrayList<Integer>() {
                {
                    add(1);
                    add(10);
                    add(100);
                    add(1000);
                    add(0);
                }
            }) {
                // Perform a fetch for every nth row in the result set.
                try (ResultSet rs = stmt.executeQuery(SQL)) {
                    timerTest(n, rs);
                }
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

        // Declare the variables for tracking the row count and elapsed time.
        int rowCount = 0;
        long startTime = 0;
        long stopTime = 0;
        long runTime = 0;

        // Set the fetch size then iterate through the result set to
        // cache the data locally.
        rs.setFetchSize(fetchSize);
        startTime = System.currentTimeMillis();
        while (rs.next()) {
            rowCount++;
        }
        stopTime = System.currentTimeMillis();
        runTime = stopTime - startTime;

        // Display the results of the timer test.
        System.out.println("FETCH SIZE: " + rs.getFetchSize());
        System.out.println("ROWS PROCESSED: " + rowCount);
        System.out.println("TIME TO EXECUTE: " + runTime);
        System.out.println();
    }
}
```

## <a name="see-also"></a>Vedere anche  

[Uso dei set di risultati](../../../connect/jdbc/code-samples/working-with-result-sets.md)  
