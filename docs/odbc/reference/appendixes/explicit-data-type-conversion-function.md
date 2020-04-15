---
title: Funzione di conversione del tipo di dati esplicito . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306992"
---
# <a name="explicit-data-type-conversion-function"></a>Funzione di conversione esplicita del tipo di dati
La conversione esplicita del tipo di dati viene specificata in termini di definizioni dei tipi di dati SQL.  
  
 La sintassi ODBC per la funzione di conversione esplicita del tipo di dati non limita le conversioni. La validità di conversioni specifiche di un tipo di dati in un altro tipo di dati verrà determinata da ogni implementazione specifica del driver. Il driver, come converte la sintassi ODBC nella sintassi nativa, rifiutare quelle conversioni che, anche se valido nella sintassi ODBC, non sono supportati dall'origine dati. La funzione ODBC **SQLGetInfo**, con le opzioni di conversione (ad esempio SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH e così via), consente di informazioni sulle conversioni supportate dall'origine dati.  
  
 Il formato della funzione **CONVERT** è:  
  
 **CONVERT(** _value_exp_, _data_type_**)**  
  
 La funzione restituisce il valore specificato da *value_exp* convertito *nell'data_type*specificato , dove *data_type* è una delle seguenti parole chiave:  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 La sintassi ODBC per la funzione di conversione esplicita del tipo di dati non supporta la specifica del formato di conversione. Se la specifica di formati espliciti è supportata dall'origine dati sottostante, un driver deve specificare un valore predefinito o implementare la specifica di formato.  
  
 L'argomento *value_exp* può essere un nome di colonna, il risultato di un'altra funzione scalare o un valore letterale numerico o stringa. Ad esempio:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 converte l'output della funzione scalare CURDATE in una stringa di caratteri.  
  
 Poiché ODBC non impone un tipo di dati per i valori restituiti da funzioni scalari (poiché le funzioni sono spesso specifiche dell'origine dati), le applicazioni devono utilizzare la funzione scalare CONVERT quando possibile per forzare la conversione del tipo di dati.  
  
 Nei due esempi seguenti viene illustrato l'utilizzo della funzione **CONVERT.** Questi esempi presuppongono l'esistenza di una tabella denominata EMPLOYEES, con una colonna EMPNO di tipo SQL_SMALLINT e una colonna EMPNAME di tipo SQL_CHAR.  
  
 Se un'applicazione specifica la seguente istruzione SQL:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Un driver per ORACLE converte l'istruzione SQL in:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Un driver per SQL Server converte l'istruzione SQL in:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Se un'applicazione specifica la seguente istruzione SQL:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Un driver per ORACLE converte l'istruzione SQL in:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Un driver per SQL Server converte l'istruzione SQL in:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Un driver per Ingres converte l'istruzione SQL in:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
