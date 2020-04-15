---
title: Esempi di conversione dei dati da SQL a C Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b10dd93c807aaa49a7e10e198f789fb47ccdeb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296651"
---
# <a name="sql-to-c-data-conversion-examples"></a>Esempi di conversione di dati da SQL a C

Gli esempi illustrati nella tabella seguente illustrano come il driver converte i dati SQL in dati C :  
  
|Tipo SQL<br /><br /> identificatore|SQL data<br /><br /> value|Tipo C<br /><br /> identificatore|Buffer<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef-0[a]|n/d|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde-0[a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234,56.0[a]|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234-0[a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|Ignorato|1234.56|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|Ignorato|1234|01S07 (intito)|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|Ignorato|----|22003|  
|SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|Ignorato|1.2345678|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|Ignorato|1.234567|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|Ignorato|1|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|Ignorato|1992,12,31, 0,0,0,0[b]|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "-0" rappresenta un byte di terminazione null. Il driver termina sempre SQL_C_CHAR dati.  
  
 [b] I numeri in questo elenco sono i numeri memorizzati nei campi della struttura TIMESTAMP_STRUCT.
