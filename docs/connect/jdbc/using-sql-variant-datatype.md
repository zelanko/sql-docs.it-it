---
title: Utilizzo del tipo di dati sql_variant | Microsoft Docs
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
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025846"
---
# <a name="using-sql_variant-data-type"></a>Uso del tipo di dati Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partire dalla versione 6.3.0, il driver JDBC per supporta il tipo di dati sql_variant. Sql_variant è inoltre supportato quando si utilizzano caratteristiche quali i parametri con valori di tabella e BulkCopy con alcune limitazioni indicate più avanti in questa pagina. Non tutti i tipi di dati possono essere archiviati nel tipo di dati sql_variant. Per un elenco dei tipi di dati supportati con sql_variant, controllare il SQL Server [docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>Popolamento e recupero di una tabella:
Supponendo che uno disponga di una tabella con una colonna sql_variant:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Uno script di esempio per inserire i valori utilizzando l'istruzione:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserimento del valore utilizzando l'istruzione preparata:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Se il tipo sottostante dei dati passati è noto, è possibile usare il rispettivo Setter. Ad esempio, `preparedStatement.setInt()` può essere usato quando si inserisce un valore integer.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Per la lettura di valori dalla tabella, è possibile usare i rispettivi Getter. Ad esempio, `getInt()` è `getString()` possibile usare i metodi o se i valori provenienti dal server sono noti:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Utilizzo di stored procedure con sql_variant:   
Con stored procedure, ad esempio:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
I parametri di output devono essere registrati:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Limitazioni di sql_variant:
- Quando si utilizza TVP per popolare una tabella con `datetime` un `smalldatetime` `getSmallDateTime()` `getDateTime()` / / `getDate()` valore archiviato in un sql_variant, chiamare su / / `date` Il set di risultati non funziona e genera l'eccezione seguente:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Soluzione alternativa: `getString()` usare `getObject()` o. 
    
- L'uso di TVP per popolare una tabella e l'invio di un valore null in un sql_variant non è supportato e genera un'eccezione:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
