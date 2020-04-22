---
title: Uso delle sequenze di escape SQL in JDBC
description: Il driver Microsoft JDBC per SQL Server supporta l'uso di sequenze di escape SQL, in base a quanto definito dall'API JDBC.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68b595c1901d010b798ebf1767e270e468fb9163
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528186"
---
# <a name="using-sql-escape-sequences"></a>Uso delle sequenze di escape SQL

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta l'uso di sequenze di escape SQL, in base a quanto definito dall'API JDBC. Le sequenze di escape vengono utilizzate all'interno di un'istruzione SQL per indicare al driver che la parte della stringa SQL per cui vengono utilizzati caratteri di escape deve essere gestita in modo diverso. Quando la parte della stringa SQL per cui vengono utilizzati caratteri di escape viene elaborata dal driver JDBC, tale parte viene tradotta in codice SQL compreso da SQL Server.  
  
 L'API JDBC richiede cinque tipi di sequenze di escape, tutti supportati dal driver JDBC:  
  
- Valori letterali dei caratteri jolly LIKE
- Gestione delle funzioni
- Valori letterali data e ora
- Chiamate di stored procedure
- Outer join
- Sintassi di escape per Limit

La sintassi della sequenza di escape utilizzata dal driver JDBC è la seguente:  
  
`{keyword ...parameters...}`  
  
> [!NOTE]  
> L'elaborazione delle sequenze di escape SQL è sempre attivata per il driver JDBC.  
  
Nelle sezioni seguenti vengono descritti i cinque tipi di sequenze di escape e viene illustrato in che modo sono supportati dal driver JDBC:  
  
## <a name="like-wildcard-literals"></a>Valori letterali dei caratteri jolly LIKE

Il driver JDBC supporta la sintassi `{escape 'escape character'}` per l'uso dei caratteri jolly della clausola LIKE come valori letterali. Il codice seguente restituisce, ad esempio, i valori per col3 se il valore di col2 inizia letteralmente con un carattere di sottolineatura (e non nel caso di utilizzo del carattere jolly).  

```java
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```

> [!NOTE]  
> La sequenza di escape deve essere alla fine dell'istruzione SQL. Se vi sono più istruzioni SQL in una stringa di comando, la sequenza di escape deve essere alla fine di ogni istruzione SQL rilevante.  

## <a name="function-handling"></a>Gestione delle funzioni

Il driver JDBC supporta le sequenze di escape delle funzioni nelle istruzioni SQL con la sintassi seguente:  

```sql
{fn functionName}  
```

dove `functionName` è una funzione supportata dal driver JDBC. Ad esempio: 

```sql
SELECT {fn UCASE(Name)} FROM Employee  
```

Nella tabella seguente sono elencate le varie funzioni supportate dal driver JDBC in caso di utilizzo di una sequenza di escape delle funzioni:  
  
| Funzioni di stringa                                                                                                                                                                                                                                                                                                                        | Funzioni numeriche                                                                                                                                                                                                                                                                                                                                                                                                   | Funzioni data/ora                                                                                                                                                                                                                                                                                                                                             | Funzioni di sistema                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE | ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE | CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> GIORNOANNO<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR | DATABASE<br /><br /> IFNULL<br /><br /> USER |

> [!NOTE]  
> Se si tenta di utilizzare una funzione non supportata dal database, si verifica un errore.  

## <a name="date-and-time-literals"></a>Valori letterali data e ora

La sintassi di escape per i valori letterali data, ora e timestamp è la seguente:  

```sql
{literal-type 'value'}  
```

dove `literal-type` è uno dei valori seguenti:  
  
| Tipo di valore letterale | Descrizione | Formato del valore               |
| ------------ | ----------- | -------------------------- |
| d            | Data        | aaaa-mm-gg                 |
| t            | Tempo        | hh:mm:ss [1]               |
| ts           | TimeStamp   | aaaa-mm-gg hh:mm:ss[.f...] |
  
Ad esempio:  

```sql
UPDATE Orders SET OpenDate={d '2005-01-31'}
WHERE OrderID=1025  
```

## <a name="stored-procedure-calls"></a>Chiamate di stored procedure

Il driver JDBC supporta la sintassi di escape `{? = call proc_name(?,...)}` e `{call proc_name(?,...)}` per le chiamate di stored procedure, a seconda che si debba o meno elaborare un parametro restituito.  
  
Una stored procedure è un oggetto eseguibile archiviato nel database. In genere, si tratta di una o più istruzioni SQL precompilate. La sintassi della sequenza di escape per la chiamata di un stored procedure è la seguente:  

```sql
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```

dove `procedure-name` specifica il nome di una stored procedure e `parameter` specifica un parametro della stored procedure.  
  
Per altre informazioni sull'uso della sequenza di escape `call` con le stored procedure, vedere [Uso delle istruzioni con le stored procedure](../../connect/jdbc/using-statements-with-stored-procedures.md).  

## <a name="outer-joins"></a>Outer join

Il driver JDBC supporta la sintassi left, right e full outer join SQL92. La sequenza di escape per gli outer join è la seguente:  

```sql
{oj outer-join}  
```

dove outer-join è:  

```sql
table-reference {LEFT | RIGHT | FULL} OUTER JOIN
{table-reference | outer-join} ON search-condition  
```

dove `table-reference` è il nome di una tabella e `search-condition` è la condizione di join che si desidera usare per le tabelle.  
  
Ad esempio:  

```sql
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status
   FROM {oj Customers LEFT OUTER JOIN
      Orders ON Customers.CustID=Orders.CustID}
   WHERE Orders.Status='OPEN'  
```

Le sequenze di escape dell'outer join seguenti sono supportate dal driver JDBC:  

- Left outer join
- Right outer join
- Full outer join
- Outer join nidificati

## <a name="limit-escape-syntax"></a>Sintassi di escape per Limit  

> [!NOTE]  
> La sintassi di escape per LIMIT è supportata solo da Microsoft JDBC Driver 4.2 (o versioni successive) per SQL Server quando si usa JDBC 4.1 o versione successiva.  
  
 La sintassi di escape per LIMIT è la seguente:  

```sql
LIMIT <rows> [OFFSET <row offset>]  
```

La sintassi di escape è costituita da due parti: \<*righe*> è obbligatorio e specifica il numero di righe da restituire. OFFSET e \<*offset di riga*> sono facoltativi e specificano il numero di righe da ignorare prima di iniziare a restituire le righe. Il driver JDBC supporta solo la parte obbligatoria trasformando la query per l'utilizzo di TOP invece di LIMIT. SQL Server non supporta la clausola LIMIT. **Il driver JDBC non supporta il parametro facoltativo \<offset di riga> e il driver genera un'eccezione se viene usato**.  
  
## <a name="see-also"></a>Vedere anche

[Uso delle istruzioni con il driver JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
