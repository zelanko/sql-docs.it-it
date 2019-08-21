---
title: Recupero di ParameterMetaData tramite useFmtOnly | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 6877a6421622ab52a92b89502c68f47c4c315d93
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025498"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>Recupero di ParameterMetaData tramite useFmtOnly
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC driver per SQL Server include un metodo alternativo per eseguire query sui metadati dei parametri dal server, **useFmtOnly**. Questa funzionalità è stata introdotta per la prima volta nella versione 7,4 del driver ed è necessaria come soluzione alternativa per `sp_describe_undeclared_parameters`i problemi noti in.
  
  Il driver utilizza principalmente il stored procedure `sp_describe_undeclared_parameters` per eseguire query sui metadati dei parametri, poiché si tratta dell'approccio consigliato per il recupero dei metadati dei parametri nella maggior parte dei casi. Tuttavia, l'esecuzione del stored procedure attualmente non riesce nei casi d'uso seguenti:
  
-   Su Always Encrypted colonne
  
-   Su tabelle temporanee e variabili di tabella
  
-   Su viste 
  
  La soluzione proposta per questi casi di utilizzo consiste nell'analizzare la query SQL dell'utente per i parametri e le destinazioni della tabella `SELECT` , quindi `FMTONLY` eseguire una query con Enabled. Il frammento di codice seguente consente di visualizzare la funzionalità.
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>Attivazione/disattivazione della funzionalità 
 La funzionalità **useFmtOnly** è disattivata per impostazione predefinita. Gli utenti possono abilitare questa funzionalità tramite la stringa di connessione `useFmtOnly=true`specificando. Ad esempio: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`.
 
 In alternativa, la funzionalità è disponibile tramite `SQLServerDataSource`.
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 La funzionalità è disponibile anche a livello di istruzione. Gli utenti possono attivare o disattivare `PreparedStatement.setUseFmtOnly(boolean)`la funzionalità.
> [!NOTE]  
>  Il driver definirà la priorità della proprietà a livello di istruzione sulla proprietà a livello di connessione.

## <a name="using-the-feature"></a>Uso della funzionalità
  Una volta abilitato, il driver inizierà a `sp_describe_undeclared_parameters` utilizzare la nuova funzionalità anziché eseguire query sui metadati dei parametri. Non sono necessarie altre azioni da parte dell'utente finale.
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  La funzionalità supporta `SELECT/INSERT/UPDATE/DELETE` solo le query. Le query devono iniziare con una delle quattro parole chiave supportate o un' [espressione di tabella comune](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017) seguita da una delle query supportate. I parametri all'interno di espressioni di tabella comuni non sono supportati.

## <a name="known-issues"></a>Problemi noti
  Esistono attualmente alcuni problemi con la funzionalità causati da malfunzionamenti nella logica di analisi di SQL. Questi problemi possono essere risolti in un aggiornamento futuro della funzionalità e sono documentati di seguito insieme ai suggerimenti per la soluzione alternativa.
  
A. Uso di un alias ' dichiarati '
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. Nome di colonna ambiguo quando le tabelle hanno nomi di colonna condivisi
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. Consente di selezionare da una sottoquery con parametri
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. Sottoquery in una clausola SET
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>Vedere anche  
 [Impostazione delle proprietà delle connessioni](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
