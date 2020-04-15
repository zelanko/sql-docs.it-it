---
title: 'Da SQL a C: Intervalli anno-mese Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296391"
---
# <a name="sql-to-c-year-month-intervals"></a>Da SQL a C: intervalli anno-mese

Gli identificatori per i tipi di dati SQL ODBC dell'intervallo anno-mese sono i seguenti:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

Nella tabella seguente vengono illustrati i tipi di dati C ODBC in cui è possibile convertire i dati SQL dell'intervallo anno-mese. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore del tipo C|Test|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|Parte dei campi finali non troncata<br /><br /> Parte dei campi finali troncata<br /><br /> La precisione iniziale della destinazione non è sufficienteper contenere i dati dall'origine|Data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|La precisione dell'intervallo era un singolo campo e i dati sono stati convertiti senza troncamento<br /><br /> La precisione dell'intervallo era un singolo campo e troncato intero<br /><br /> La precisione dell'intervallo non era un singolo campo|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Lunghezza dei dati in byte<br /><br /> Dimensione del tipo di dati C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Lunghezza byte carattere < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >: *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza dei caratteri < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *BufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >: *BufferLength*|Data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Un tipo SQL di intervallo anno-mese può essere convertito in qualsiasi tipo di intervallo C del mese dell'anno.  
  
 [b] Se la precisione dell'intervallo è un singolo campo (uno di ANNO o MESE), il tipo SQL dell'intervallo può essere convertito in qualsiasi valore numerico esatto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversioni predefinite

La conversione predefinita di un tipo SQL a intervalli è nel tipo di dati dell'intervallo C corrispondente. L'applicazione associa quindi la colonna o il parametro (o imposta il campo SQL_DESC_DATA_PTR nel record appropriato del ARD) in modo che punti alla struttura SQL_INTERVAL_STRUCT inizializzata (o passa un puntatore alla struttura di INTERVAL_STRUCT SQL_ come argomento *TargetValuePtr* in una chiamata a **SQLGetData**).
