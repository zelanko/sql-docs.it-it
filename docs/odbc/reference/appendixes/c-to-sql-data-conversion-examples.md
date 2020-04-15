---
title: Esempi di conversione di dati da C a SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e21654f183946675c63cee10a3c08754e1508f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291991"
---
# <a name="c-to-sql-data-conversion-examples"></a>Esempi di conversione di dati da C a SQL
Negli esempi seguenti viene illustrato come il driver converte i dati C in dati SQL:  
  
|Identificatore del tipo C|Valore dati C|Tipo SQL<br /><br /> identificatore|Colonna<br /><br /> length|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef-0[a]|SQL_CHAR|6|abcdef|n/d|  
|SQL_C_CHAR|abcdef-0[a]|SQL_CHAR|5|Abcde|22001|  
|SQL_C_CHAR|1234,56.0[a]|SQL_DECIMAL|8[b]|1234.56|n/d|  
|SQL_C_CHAR|1234,56.0[a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234,56.0[a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/d|1234.56|n/d|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/d|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/d|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|10|1992-12-31|n/d|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_TIMESTAMP|n/d|1992-12-31 00:00:00.0|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|18|----|22003|  
  
 [a] "-0" rappresenta un byte di terminazione null. Il byte di terminazione null è necessario solo se la lunghezza dei dati è SQL_NTS.  
  
 [b] Oltre ai byte per i numeri, è necessario un byte per un segno e un altro byte è necessario per il separatore decimale.  
  
 [c] I numeri in questo elenco sono i numeri memorizzati nei campi della struttura SQL_DATE_STRUCT.  
  
 [d] I numeri in questo elenco sono i numeri memorizzati nei campi della struttura SQL_TIMESTAMP_STRUCT.
