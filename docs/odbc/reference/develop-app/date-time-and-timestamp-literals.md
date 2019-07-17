---
title: Date, Time e Timestamp valori letterali | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6191995c9d1c488fc5af056248ba39dd3eb4607
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076979"
---
# <a name="date-time-and-timestamp-literals"></a>Valori letterali data, ora e timestamp
La sequenza di escape per i valori letterali data, ora e timestamp  
  
 **{** _-tipo_ **'** _valore_ **'}**  
  
 in cui *-tipo di valore letterale* è uno dei valori elencati nella tabella seguente.  
  
|*literal-type*|Significato|Formato di *valore*|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*aaaa*-*mm*-*gg*|  
|**t**|Ora *|*hh*:*mm*:*ss*[1]|  
|**ts**|Timestamp|*aaaa*-*mm*-*gg* *hh*:*mm*:*ss*[.*f...* ] [1]|  
  
 [1] il numero di cifre a destra del separatore decimale in un intervallo di tempo o timestamp letterale contenente un componente relativo ai secondi dipende la precisione in secondi, quanto contenuto nel campo del descrittore SQL_DESC_PRECISION. (Per altre informazioni, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Per altre informazioni sulla data, ora e timestamp sequenze di escape, vedere [Date, Time e Timestamp sequenze di Escape](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) nell'appendice c: Grammatica SQL.  
  
 Ad esempio, entrambe le istruzioni SQL seguenti aggiornare open data di ordine di vendita 1023 nella tabella Orders. La prima istruzione Usa la sintassi della sequenza di escape. La seconda istruzione viene utilizzata la sintassi di nativo Oracle Rdb per la colonna delle DATE e non è interoperativa.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 La sequenza di escape per una data, ora o timestamp letterale può essere inserita in una variabile di caratteri associata a una data, ora o timestamp parametro. Ad esempio, il codice seguente usa un parametro data associato a una variabile di tipo carattere per aggiornare la data dell'ordine di vendita 1023 nella tabella Orders open:  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Tuttavia, è in genere più efficiente per associare il parametro direttamente a una struttura di data:  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Per determinare se un driver supporta le sequenze di escape ODBC per data, ora o timestamp valori letterali, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati di data, ora o timestamp, deve anche supportare la sequenza di escape corrispondente.  
  
 Origini dati possono anche supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diverse dalle sequenze di escape ODBC per data, ora o timestamp valori letterali. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Per determinare se un driver supporta le sequenze di escape ODBC per i valori letterali intervallo, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati di intervallo data/ora, deve anche supportare la sequenza di escape corrispondente.  
  
 Origini dati possono anche supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diverse dalle sequenze di escape ODBC per i valori letterali intervallo data/ora. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.
