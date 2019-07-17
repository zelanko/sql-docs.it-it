---
title: C per esempi di conversione dei dati SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e475abb699c7fa7240ca6eb39b1b32f1730d33c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125744"
---
# <a name="c-to-sql-data-conversion-examples"></a>Esempi di conversione di dati da C a SQL
Gli esempi seguenti illustrano come il driver converte dati C ai dati SQL:  
  
|Identificatore di tipo C|Valore di dati C|Tipo SQL<br /><br /> identifier|Colonna<br /><br /> length|SQL data<br /><br /> Valore|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|6|abcdef|n/d|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8[b]|1234.56|n/d|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/d|1234.56|n/d|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/d|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/d|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|n/d|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|n/d|1992-12-31 00:00:00.0|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/d|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" rappresenta un byte di terminazione null. Il byte di terminazione null è necessario solo se la lunghezza dei dati è SQL_NTS.  
  
 [b] oltre a byte per i numeri, un byte è obbligatorio per un segno e un altro byte è necessario per il separatore decimale.  
  
 [c] i numeri in questo elenco sono i numeri memorizzati nei campi della struttura del valore SQL_DATE_STRUCT.  
  
 [d] numeri di questo elenco sono i numeri memorizzati nei campi della struttura di SQL_TIMESTAMP_STRUCT.
