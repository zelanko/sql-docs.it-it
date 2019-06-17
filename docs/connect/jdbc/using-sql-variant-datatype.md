---
title: Utilizzando il tipo di dati Sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c004bc40ed0c85b82612be9069e1a53041c8095c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798589"
---
# <a name="using-sqlvariant-data-type"></a>Utilizzo di dati Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partire dalla versione 6.3.0, il driver JDBC supporta il tipo di dati sql_variant. Sql_variant è supportato anche quando usando funzionalità quali BulkCopy e parametri con valori di tabella con alcune limitazioni indicate più avanti in questa pagina. Non tutti i tipi di dati possono essere archiviati nel tipo di dati sql_variant. Per un elenco dei tipi di dati supportati con sql_variant, controllare il Server SQL [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>La compilazione e il recupero di una tabella:
Supponendo uno che dispone di una tabella con una colonna sql_variant come:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Uno script di esempio per inserire valori istruzione using:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserimento valore usando istruzione preparata:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Se è noto il tipo sottostante di dati passati, è possibile che il rispettivo setter è utilizzabile. Ad esempio, `preparedStatement.setInt()` può essere utilizzato durante l'inserimento di un valore intero.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Per la lettura dei valori della tabella, è possibile utilizzare il rispettivo getter. Ad esempio, `getInt()` o `getString()` metodi possono essere utilizzati se i valori provenienti dal server sono noti:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>Utilizzo di stored procedure con sql_variant:   
Con una stored procedure, ad esempio:     

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

## <a name="limitations-of-sqlvariant"></a>Limitazioni di sql_variant:
- Quando si usa TVP per popolare una tabella con una `datetime` / `smalldatetime` / `date` valore archiviato in un tipo sql_variant, chiamare `getDateTime()` / `getSmallDateTime()` / `getDate()` in un Set di risultati non funziona e genera l'eccezione seguente:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Soluzione alternativa: utilizzare `getString()` o `getObject()` invece. 
    
- Usa TVP per popolare una tabella e l'invio di un valore null in un tipo sql_variant non è supportato e genera un'eccezione:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
