---
title: 'Da SQL a C: Numerico | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a23e60b161c09367cfb079cea1f7ca146b4ebee5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056856"
---
# <a name="sql-to-c-numeric"></a>Da SQL a C: Numeric

Gli identificatori per i tipi di dati SQL ODBC numerici sono i seguenti:

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_INTEGER SQL_DOUBLE  

Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati numerici di SQL. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Lunghezza in byte di caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|I dati convertiti senza troncamento, [a]<br /><br /> I dati convertiti con troncamento delle cifre frazionarie [a]<br /><br /> La conversione dei dati potrebbe comportare la perdita di cifre [a] intero (in contrapposizione frazionari)|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|Data è compreso nell'intervallo del tipo di dati a cui il numero viene convertito [a]<br /><br /> I dati non rientra nell'intervallo del tipo di dati a cui il numero viene convertito [a]|Data<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_BIT|I dati sono 0 o 1, [a]<br /><br /> I dati sono maggiori di 0, inferiore a 2 e non è uguale a 1, [a]<br /><br /> I dati sono minore di 0 oppure maggiore o uguale a 2, [a]|Data<br /><br /> Dati troncati<br /><br /> Non definito|1[b]<br /><br /> 1[b]<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] [c] SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_DAY [c] [c] SQL_C_INTERVAL_HOUR SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|Dati non troncati<br /><br /> Parte relativa ai secondi frazionari troncato<br /><br /> Parte intera del numero troncato|Data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|Parte intera del numero troncato|Non definito|Non definito|22015|  
  
 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] questa è la dimensione del tipo di dati C corrispondente.  
  
 [c] questa conversione è supportata solo per i tipi di dati numerici esatti (SQL_DECIMAL SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER e SQL_BIGINT). Non è supportata per i tipi di dati numerico approssimato (SQL_REAL, SQL_FLOAT o SQL_DOUBLE).  

## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC e SQLSetDescField

 Il [funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) è necessario per eseguire l'associazione manuale con valori SQL_C_NUMERIC. (Si noti che in ODBC 3.0 è stato aggiunto SQLSetDescField). Per eseguire il binding manuale, è prima necessario ottenere l'handle descrittore.  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
