---
title: 'Da C a SQL: Intervalli di tempo | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb41d658637258c6d60b5adb4e0d7abb9ae81d91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213417"
---
# <a name="c-to-sql-day-time-intervals"></a>Da C a SQL: intervalli di data/ora
Gli identificatori per i tipi di dati di intervallo giorno-ora ODBC C sono:  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 La tabella seguente illustra il codice SQL ODBC i tipi di dati a cui l'intervallo di dati C può essere convertito. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Lunghezza in byte di colonna > = lunghezza in byte di caratteri<br /><br /> Lunghezza in byte colonna < [a] lunghezza in byte di caratteri<br /><br /> Valore di dati non è un intervallo valido di valore letterale|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Lunghezza in caratteri colonna > = lunghezza in caratteri di dati<br /><br /> Lunghezza in caratteri colonna < lunghezza dei dati [a] in caratteri<br /><br /> Valore di dati non è un intervallo valido di valore letterale|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|Conversione di un intervallo di un solo campo non ha restituito il troncamento di cifre intere<br /><br /> Conversione comportato il troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|Valore dei dati è stato convertito senza troncamento di tutti i campi<br /><br /> Uno o più campi del valore dei dati sono stati troncati durante la conversione|n/d<br /><br /> 22015|  
  
 [a] tipi di dati di intervallo C tutto possono essere convertito in un tipo di dati carattere.  
  
 [b] se il campo di tipo nella struttura di intervallo è tale che l'intervallo è un singolo campo (SQL_DAY, SQL_HOUR, SQL_MINUTE o SQL_SECOND), l'intervallo di tipo C può essere convertito in qualsiasi numerico esatto (SQL_INTEGER SQL_TINYINT, SQL_SMALLINT, SQL_BIGINT SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversione di predefinito di un tipo di intervallo C è l'intervallo di tempo corrispondente tipo SQL.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal tipo di dati di intervallo C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati di intervallo C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.  
  
 Nell'esempio seguente viene illustrato come inviare i dati di intervallo C archiviati nella struttura SQL_INTERVAL_STRUCT in una colonna di database. La struttura di intervallo contiene un intervallo di tempo DAY_TO_SECOND; verrà archiviato in una colonna di database di tipo SQL_INTERVAL_DAY_TO_MINUTE.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
