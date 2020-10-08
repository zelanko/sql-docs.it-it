---
description: Uso del tipo di dati Sql_variant
title: Uso del tipo di dati sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 198c8a21fcea9a1386effe8d30c8d954180d6dc5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727484"
---
# <a name="using-sql_variant-data-type"></a>Uso del tipo di dati Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partire dalla versione 6.3.0, JDBC Driver supporta il tipo di dati sql_variant. Il tipo di dati sql_variant è supportato anche quando si usano funzionalità come ad esempio TVP (Table Valued Parameter, parametri con valori di tabella) e copia bulk. Esistono alcune limitazioni specificate più avanti in questa pagina. Non tutti i tipi di dati possono essere archiviati nel tipo di dati sql_variant. Per un elenco dei tipi di dati supportati con sql_variant, vedere la [documentazione](../../t-sql/data-types/sql-variant-transact-sql.md) di SQL Server.

##  <a name="populating-and-retrieving-a-table"></a>Popolamento e recupero di una tabella:
Si supponga di avere una tabella con una colonna sql_variant come riportato di seguito:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Script di esempio per inserire i valori usando un'istruzione:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserimento del valore usando un'istruzione preparata:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Se il tipo sottostante dei dati passati è noto, è possibile usare il rispettivo setter. È ad esempio possibile usare `preparedStatement.setInt()` quando si inserisce un valore intero.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Per leggere i valori della tabella, è possibile usare i rispettivi getter. È ad esempio possibile usare i metodi `getInt()` o `getString()` se i valori provenienti dal server sono noti:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Uso delle stored procedure con sql_variant:   
Si supponga di avere una stored procedure come riportato di seguito:     

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
- Quando si usano TVP per popolare una tabella con un valore `datetime`/`smalldatetime`/`date` archiviato in un tipo di dati sql_variant, la chiamata di `getDateTime()`/`getSmallDateTime()`/`getDate()` in ResultSet non funziona e genera l'eccezione seguente:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Soluzione alternativa: usare invece `getString()` o `getObject()`. 
    
- L'uso di TVP per popolare una tabella e l'invio di un valore Null in un tipo di dati sql_variant non sono supportati e generano un'eccezione:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)