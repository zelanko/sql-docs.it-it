---
title: 'Da C a SQL: Intervalli giorno-tempo Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3f7efb443b442d44a94cfd43629cdaedd6195b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291921"
---
# <a name="c-to-sql-day-time-intervals"></a>Da C a SQL: intervalli di data/ora
Gli identificatori per i tipi di dati ODBC C dell'intervallo di giorno sono:  
  
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
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati dell'intervallo C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[aa]<br /><br /> SQL_LONGVARCHAR[a]|Lunghezza byte colonna >: lunghezza byte carattere<br /><br /> Lunghezza byte colonna < Lunghezza byte carattere[a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo validoData value is not a valid interval literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Lunghezza carattere colonna >: lunghezza dei caratteri dei dati<br /><br /> Lunghezza carattere colonna < Lunghezza del carattere dei dati[a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo validoData value is not a valid interval literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|La conversione di un intervallo a campo singolo non ha comportato il troncamento di cifre intere<br /><br /> La conversione ha comportato il troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|Il valore dei dati è stato convertito senza troncamento dei campi<br /><br /> Uno o più campi del valore di dati sono stati troncati durante la conversione|n/d<br /><br /> 22015|  
  
 [a] Tutti i tipi di dati dell'intervallo C possono essere convertiti in un tipo di dati carattere.  
  
 [b] Se il campo type nella struttura dell'intervallo è tale che l'intervallo è un singolo campo (SQL_DAY, SQL_HOUR, SQL_MINUTE o SQL_SECOND), il tipo di intervallo C può essere convertito in qualsiasi numero esatto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversione predefinita di un tipo di intervallo C è nel tipo SQL dell'intervallo di giorno corrispondente.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati di intervallo C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati dell'intervallo C. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.  
  
 Nell'esempio seguente viene illustrato come inviare i dati di intervallo C archiviati nella struttura SQL_INTERVAL_STRUCT in una colonna di database. La struttura dell'intervallo contiene un intervallo di DAY_TO_SECOND; verrà memorizzato in una colonna di database di tipo SQL_INTERVAL_DAY_TO_MINUTE.  
  
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
