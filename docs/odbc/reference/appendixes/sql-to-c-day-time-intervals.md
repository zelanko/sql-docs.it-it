---
title: 'Da SQL a C: Intervalli giorno-temporale Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296471"
---
# <a name="sql-to-c-day-time-intervals"></a>Da SQL a C: intervalli di tempo

Gli identificatori per i tipi di dati SQL ODBC dell'intervallo di urna sono i seguenti:

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

Nella tabella seguente vengono illustrati i tipi di dati C ODBC in cui è possibile convertire i dati SQL dell'intervallo diurni. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Tutti i tipi di intervallo C giorno-tempo|Parte dei campi finali non troncata<br /><br /> Parte dei campi finali troncata<br /><br /> La precisione iniziale della destinazione non è sufficienteper contenere i dati dall'origine|Data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza dei dati<br /><br /> Lunghezza dei dati<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|La precisione dell'intervallo era un singolo campo e i dati sono stati convertiti senza troncamento<br /><br /> La precisione dell'intervallo era un singolo campo e troncato<br /><br /> La precisione dell'intervallo era un singolo campo e troncato intero<br /><br /> La precisione dell'intervallo non era un singolo campo|Data<br /><br /> Dati troncati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Lunghezza dei dati<br /><br /> Lunghezza dei dati<br /><br /> Dimensione del tipo di dati C|n/d<br /><br /> 01S07 (intito)<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Lunghezza byte carattere < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >: *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza dei caratteri < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >: *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Un tipo SQL di intervallo di urne può essere convertito in qualsiasi tipo di intervallo di giorno-ora C.  
  
 [b] Se la precisione dell'intervallo è un singolo campo (uno dei valori DAY, HOUR, MINUTE o SECOND), il tipo SQL dell'intervallo può essere convertito in qualsiasi numero esatto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
La conversione predefinita di un tipo SQL a intervalli è nel tipo di dati dell'intervallo C corrispondente. L'applicazione associa quindi la colonna o il parametro (o imposta il campo SQL_DESC_DATA_PTR nel record appropriato del ARD) in modo che punti alla struttura SQL_INTERVAL_STRUCT inizializzata (o passa un puntatore alla struttura di INTERVAL_STRUCT SQL_ come argomento *TargetValuePtr* in una chiamata a **SQLGetData**).  
  
Nell'esempio seguente viene illustrato come trasferire dati da una colonna di tipo SQL_INTERVAL_DAY_TO_MINUTE nella struttura SQL_INTERVAL_STRUCT in modo che venga nuovamente riproviene come intervallo di DAY_TO_HOUR.  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
