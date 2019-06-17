---
title: Funzione di conversione del tipo di dati espliciti | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77cb69877324b36120b3a277688bb1ad737f5c4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188982"
---
# <a name="explicit-data-type-conversion-function"></a>Funzione di conversione esplicita del tipo di dati
Conversione tipo di dati esplicito è specificata in termini di definizioni dei tipi di dati SQL.  
  
 La sintassi ODBC per la funzione di conversione tipo di dati esplicito non limita le conversioni. La validità delle conversioni specifiche di un tipo di dati in un altro tipo di dati verrà determinata da ogni implementazione specifici del driver. Il driver rifiuterà, come la sintassi ODBC converte in sintassi native, tali conversioni, anche se la sintassi ODBC, non sono supportate dall'origine dati. La funzione ODBC **SQLGetInfo**, con la conversione opzioni (ad esempio SQL_CONVERT_BIGINT SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH e così via), fornisce un modo per richiedere informazioni sulle conversioni supportate dall'origine dati .  
  
 Il formato del **CONVERTIRE** funzione è:  
  
 **CONVERT(** _value_exp_, _data_type_ **)**  
  
 La funzione restituisce il valore specificato da *value_exp* convertito all'entità specificata *data_type*, dove *data_type* è una delle parole chiave seguenti:  
  
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
  
 La sintassi ODBC per la funzione di conversione tipo di dati esplicito supporta l'impostazione del formato di conversione. Se specifica dei formati espliciti è supportata dall'origine dati sottostante, un driver necessario specificare un valore predefinito o implementare specifica di formato.  
  
 L'argomento *value_exp* può essere un nome di colonna, il risultato di un'altra funzione scalare o un valore numerico o stringa letterale. Ad esempio:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 Converte l'output della funzione scalare CURDATE in una stringa di caratteri.  
  
 Poiché ODBC non obbliga a usare un tipo di dati per i valori restituiti da funzioni scalari (perché le funzioni sono spesso specifici dell'origine dati), le applicazioni devono utilizzare la funzione scalare CONVERT ogni volta che è possibile forzare una conversione tipo di dati.  
  
 I due esempi seguenti viene illustrato l'utilizzo dei **CONVERTIRE** (funzione). Questi esempi presuppongono l'esistenza di una tabella denominata EMPLOYEES, con una colonna EMPNO typu SQL_SMALLINT e una colonna EMPNAME typu SQL_CHAR.  
  
 Se un'applicazione specifica l'istruzione SQL seguente:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Un driver per ORACLE viene convertito l'istruzione SQL da:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Un driver per SQL Server converte l'istruzione SQL da:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Se un'applicazione specifica l'istruzione SQL seguente:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Un driver per ORACLE viene convertito l'istruzione SQL da:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Un driver per SQL Server converte l'istruzione SQL da:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Un driver per Ingres traduce l'istruzione SQL da:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
