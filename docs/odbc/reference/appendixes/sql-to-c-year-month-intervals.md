---
title: 'SQL a c: Intervalli anno-mese | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 01af57739f23db586991f8a54d14b90b47f15933
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419936"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL a c: Intervalli anno-mese

Gli identificatori per i tipi di dati SQL ODBC intervallo anno-mese sono i seguenti:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

Nella tabella seguente mostra i dati ODBC C i tipi di dati per anno-mese in cui può essere convertita l'intervallo di dati SQL. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|La parte di campi non troncato finale<br /><br /> La parte di campi troncato finale<br /><br /> Precisione della destinazione iniziale non è sufficientemente grande per contenere i dati dall'origine|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|Intervallo di precisione è un singolo campo e i dati sono stati convertiti senza troncamenti<br /><br /> Intervallo di precisione è un singolo campo e intero troncato<br /><br /> Intervallo di precisione non è un singolo campo|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Lunghezza in byte dei dati<br /><br /> Dimensione del tipo di dati C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Dati<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Lunghezza in byte di caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri < *BufferLength*<br /><br /> Numero di cifre intero (in contrapposizione frazionari) < *BufferLength*<br /><br /> Numero di cifre (in contrapposizione frazionari) intero > = *BufferLength*|Dati<br /><br /> Dati troncati<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Dimensione del tipo di dati C<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervallo anno-mese di un tipo SQL può essere convertito in qualsiasi tipo di intervallo C anno-mese.  
  
 [b] se l'intervallo di precisione è un singolo campo (uno di anno o un mese), l'intervallo di tipo SQL può essere convertito in qualsiasi numerico esatto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversioni predefinite

La conversione predefinita di un intervallo di tipo SQL è il tipo di dati di intervallo C corrispondenti. L'applicazione quindi associa la colonna o parametro (o imposta il campo SQL_DESC_DATA_PTR nel record appropriato del ARD) in modo che punti alla struttura SQL_INTERVAL_STRUCT inizializzata (o passa un puntatore alla struttura di SQL _ INTERVAL_STRUCT come le *TargetValuePtr* argomento in una chiamata a **SQLGetData**).
