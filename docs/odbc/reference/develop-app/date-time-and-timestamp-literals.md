---
title: Valori letterali data, ora e timestamp | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076979"
---
# <a name="date-time-and-timestamp-literals"></a>Valori letterali data, ora e timestamp
La sequenza di escape per i valori letterali data, ora e timestamp è  
  
 **{**  _-Type_ **'** _value_ **'}**  
  
 dove *literal-type* è uno dei valori elencati nella tabella seguente.  
  
|*tipo di valore letterale*|Significato|Formato del *valore*|  
|---------------------|-------------|-----------------------|  
|**d**|Data|*aaaa*-** mm-*GG*|  
|**t**|Tempo|*HH*:*mm*:*SS*[1]|  
|**ts**|Timestamp|*aaaa*-** mm-*GG* *HH*:*mm*:*SS*[.* f...*] 1|  
  
 [1] il numero di cifre a destra del separatore decimale in un valore letterale intervallo temporale o timestamp contenente un componente secondi dipende dalla precisione dei secondi, come contenuto nel campo del descrittore SQL_DESC_PRECISION. Per ulteriori informazioni, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Per ulteriori informazioni sulle sequenze di escape di data, ora e timestamp, vedere [sequenze di escape di data, ora e timestamp](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) nell'Appendice C: grammatica SQL.  
  
 Ad esempio, entrambe le istruzioni SQL seguenti aggiornano la data di apertura dell'ordine di vendita 1023 nella tabella Orders. La prima istruzione usa la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa di Oracle RDB per la colonna DATE e non è interoperativa.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 Anche la sequenza di escape per un valore letterale di data, ora o timestamp può essere inserita in una variabile di tipo carattere associata a un parametro di data, ora o timestamp. Il codice seguente, ad esempio, usa un parametro date associato a una variabile di tipo carattere per aggiornare la data di apertura dell'ordine di vendita 1023 nella tabella Orders:  
  
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
  
 Tuttavia, in genere è più efficiente associare il parametro direttamente a una struttura di data:  
  
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
  
 Per determinare se un driver supporta le sequenze di escape ODBC per i valori letterali data, ora o timestamp, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati data, ora o timestamp, deve supportare anche la sequenza di escape corrispondente.  
  
 Le origini dati possono inoltre supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diversi dalle sequenze di escape ODBC per i valori letterali data, ora o timestamp. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Per determinare se un driver supporta le sequenze di escape ODBC per i valori letterali di intervallo, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati intervallo DateTime, deve supportare anche la sequenza di escape corrispondente.  
  
 Le origini dati possono inoltre supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diversi dalle sequenze di escape ODBC per i valori letterali di intervallo DateTime. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.
