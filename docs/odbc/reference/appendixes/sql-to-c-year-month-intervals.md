---
title: 'Da SQL a C: intervalli anno-mese | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7412226dd0674022da022b0a0a63e5bf2063cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065039"
---
# <a name="sql-to-c-year-month-intervals"></a>Da SQL a C: intervalli anno-mese

Gli identificatori per i tipi di dati ODBC SQL con intervallo anno-mese sono i seguenti:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

Nella tabella seguente sono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL dell'intervallo di anno mese. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|Porzione campi finali non troncata<br /><br /> Porzione campi finali troncata<br /><br /> La precisione principale della destinazione non è abbastanza grande da poter conservare i dati dall'origine|data<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|La precisione dell'intervallo è un singolo campo e i dati sono stati convertiti senza troncamento<br /><br /> La precisione dell'intervallo è un singolo campo e l'intero troncato<br /><br /> La precisione dell'intervallo non è un campo singolo|data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensioni del tipo di dati C<br /><br /> Lunghezza dei dati in byte<br /><br /> Dimensioni del tipo di dati C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Lunghezza in byte dei dati <= *bufferLength*<br /><br /> Lunghezza in byte dei dati > *bufferLength*|data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Lunghezza in byte di caratteri < *bufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *bufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >= *bufferLength*|data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensioni del tipo di dati C<br /><br /> Dimensioni del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri < *bufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) < *bufferLength*<br /><br /> Numero di cifre intere (anziché frazionarie) >= *bufferLength*|data<br /><br /> Dati troncati<br /><br /> Non definito|Dimensioni del tipo di dati C<br /><br /> Dimensioni del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] un tipo SQL con intervallo di anno mese può essere convertito in un tipo C con intervallo di mesi di anno.  
  
 [b] se la precisione dell'intervallo è un singolo campo (un anno o un mese), il tipo di intervallo SQL può essere convertito in un valore numerico esatto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversioni predefinite

La conversione predefinita di un tipo SQL intervallo corrisponde al tipo di dati intervallo C corrispondente. L'applicazione associa quindi la colonna o il parametro (oppure imposta il campo SQL_DESC_DATA_PTR nel record appropriato del sistema ARD) in modo che punti alla struttura di SQL_INTERVAL_STRUCT inizializzata (o passa un puntatore alla struttura SQL_ INTERVAL_STRUCT come argomento *TargetValuePtr* in una chiamata a **SQLGetData**).
