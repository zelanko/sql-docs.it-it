---
title: Analisi dei risultati | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 127c97ec155ef1e19df4103b12a6e10b8b67fe74
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027866"
---
# <a name="parsing-the-results"></a>Analisi dei risultati

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo descrive il modo in cui SQL Server prevede che gli utenti elaborino completamente i risultati restituiti da qualsiasi query.

## <a name="update-counts-and-result-sets"></a>Conteggio aggiornamenti e set di risultati

In questa sezione vengono illustrati i due risultati più comuni restituiti da SQL Server: conteggio aggiornamenti e ResultSet. In generale, qualsiasi query eseguita da un utente provocherà la restituzione di uno di questi risultati. si prevede che gli utenti gestiscano entrambi durante l'elaborazione dei risultati.

Il codice seguente è un esempio di come un utente può scorrere tutti i risultati dal server:
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>Eccezioni
Quando si esegue un'istruzione che restituisce un errore o un messaggio informativo, SQL Server risponderà in modo diverso a seconda che sia in grado di generare un piano di esecuzione. Il messaggio di errore può essere generato immediatamente dopo l'esecuzione dell'istruzione o potrebbe richiedere un set di risultati distinto. Nel secondo caso, è necessario che le applicazioni analizzino il set di risultati per recuperare l'eccezione.

Quando SQL Server non è in grado di generare un piano di esecuzione, l'eccezione viene generata immediatamente.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

Quando SQL Server restituisce un messaggio di errore in un set di risultati, è necessario elaborare il set di risultati per recuperare l'eccezione.

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

Se l'esecuzione dell'istruzione genera più set di risultati, ogni set di risultati deve essere elaborato finché non viene raggiunto quello con l'eccezione.

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

Nel caso di `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`, l'eccezione viene generata `execute()` immediatamente e `SELECT 1` non viene eseguita affatto.

Se l'errore da SQL Server presenta la gravità `0` a `9`, viene considerato come un messaggio informativo e restituito come `SQLWarning`.

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
