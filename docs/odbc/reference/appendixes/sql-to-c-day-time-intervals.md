---
title: 'SQL a c: Intervalli di tempo | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee08f42a4ccd7eb51f45e1654f20e264f80c49d2
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420036"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL a c: Intervalli di tempo

Gli identificatori per i tipi di dati di intervallo giorno-ora ODBC SQL sono i seguenti:

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

Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui può essere convertito l'intervallo di tempo i dati di SQL. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Tutti i tipi di intervallo C / ora|La parte di campi non troncato finale<br /><br /> La parte di campi troncato finale<br /><br /> Precisione della destinazione iniziale non è sufficientemente grande per contenere i dati dall'origine|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza dei dati<br /><br /> Lunghezza dei dati<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|Intervallo di precisione è un singolo campo e i dati sono stati convertiti senza troncamenti<br /><br /> Intervallo di precisione è un singolo campo e troncati frazionario<br /><br /> Intervallo di precisione è un singolo campo e intero troncato<br /><br /> Intervallo di precisione non è un singolo campo|Dati<br /><br /> Dati troncati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Lunghezza dei dati<br /><br /> Lunghezza dei dati<br /><br /> Dimensione del tipo di dati C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Dati<br /><br /> Non definito|Lunghezza dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Lunghezza in byte di caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervallo di tempo A tipo SQL può essere convertito in qualsiasi tipo di intervallo giorno-time C.  
  
 [b] se l'intervallo di precisione è un singolo campo (uno del giorno, ora, minuto o secondo), l'intervallo di tipo SQL può essere convertito in qualsiasi numerico esatto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
La conversione predefinita di un intervallo di tipo SQL è il tipo di dati di intervallo C corrispondenti. L'applicazione quindi associa la colonna o parametro (o imposta il campo SQL_DESC_DATA_PTR nel record appropriato del ARD) in modo che punti alla struttura SQL_INTERVAL_STRUCT inizializzata (o passa un puntatore alla struttura di SQL _ INTERVAL_STRUCT come le *TargetValuePtr* argomento in una chiamata a **SQLGetData**).  
  
Nell'esempio seguente viene illustrato come trasferire i dati da una colonna di tipo SQL_INTERVAL_DAY_TO_MINUTE nella struttura SQL_INTERVAL_STRUCT tale che viene restituita come un intervallo di DAY_TO_HOUR.  

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
