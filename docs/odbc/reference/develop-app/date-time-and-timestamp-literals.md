---
title: 'Valori letterali di data, ora e timestamp : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288297"
---
# <a name="date-time-and-timestamp-literals"></a>Valori letterali data, ora e timestamp
La sequenza di escape per i valori letterali di data, ora e timestamp è  
  
 **-tipo**_-type_ **'** _valore_ **'**    
  
 dove *literal-type* è uno dei valori elencati nella tabella seguente.  
  
|*tipo letterale*|Significato|Formato del *valore*|  
|---------------------|-------------|-----------------------|  
|**D**|Data|*yyyy*-*mm*-*gg*|  
|**T**|Il tempo|*hh*:*mm*:*ss*[1]|  
|**Ts**|Timestamp|*yyyy*-*mm*-*gg* *hh*:*mm*:*ss*[.* f...*] [1]|  
  
 [1] Il numero di cifre a destra del separatore decimale in un valore letterale di intervallo di tempo o timestamp contenente un componente secondi dipende dalla precisione dei secondi, come contenuto nel campo descrittore SQL_DESC_PRECISION. (Per ulteriori informazioni, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Per altre informazioni sulle sequenze di escape di data, ora e timestamp, vedere Sequenze di escape [di data, ora e timestamp](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) nell'Appendice C: Grammatica SQL.  
  
 Ad esempio, entrambe le istruzioni SQL seguenti aggiornano la data di apertura dell'ordine cliente 1023 nella tabella Orders. La prima istruzione utilizza la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa Oracle Rdb per la colonna DATE e non è interoperabile.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 La sequenza di escape per un valore letterale di data, ora o timestamp può anche essere inserita in una variabile di tipo carattere associata a un parametro di data, ora o timestamp. Ad esempio, il codice seguente usa un parametro date associato a una variabile di caratteri per aggiornare la data di apertura dell'ordine cliente 1023 nella tabella Orders:  
  
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
  
 Tuttavia, è in genere più efficiente associare il parametro direttamente a una struttura di data:However, it is usually more efficient to bind the parameter directly to a date structure:  
  
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
  
 Per determinare se un driver supporta le sequenze di escape ODBC per valori letterali di data, ora o timestamp, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati data, ora o timestamp, deve supportare anche la sequenza di escape corrispondente.  
  
 Le origini dati possono inoltre supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diversi dalle sequenze di escape ODBC per i valori letterali di data, ora o timestamp. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Per determinare se un driver supporta le sequenze di escape ODBC per i valori letterali di intervallo, un'applicazione chiama **SQLGetTypeInfo**. Se l'origine dati supporta un tipo di dati intervallo datetime, deve supportare anche la sequenza di escape corrispondente.  
  
 Le origini dati possono inoltre supportare i valori letterali datetime definiti nella specifica ANSI SQL-92, che sono diversi dalle sequenze di escape ODBC per i valori letterali di intervallo datetime. Per determinare se un'origine dati supporta i valori letterali ANSI, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ANSI_SQL_DATETIME_LITERALS.
