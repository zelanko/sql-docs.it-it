---
title: 'Da SQL a C: Carattere | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3a0a7036d67716a3d90bd8953a3c7ba2c575c92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259506"
---
# <a name="sql-to-c-character"></a>Da SQL a C: Carattere

Gli identificatori per i tipi di dati carattere SQL ODBC sono le seguenti:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati SQL di tipo carattere. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Lunghezza in byte dei dati < *BufferLength*<br /><br /> Lunghezza in byte di dati > = *BufferLength*|Dati<br /><br /> Dati troncati|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Lunghezza dei dati in caratteri < *BufferLength*<br /><br /> Lunghezza dei dati in caratteri > = *BufferLength*|Dati<br /><br /> Dati troncati|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT  SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT  SQL_C_SLONG SQL_C_ULONG SQL_C_LONG  SQL_C_NUMERIC|I dati convertiti senza troncamento [b]<br /><br /> I dati convertiti con troncamento delle cifre frazionarie [a]<br /><br /> La conversione dei dati potrebbe comportare la perdita di cifre [a] intero (in contrapposizione frazionari)<br /><br /> I dati non sono un *letterali numerici*[b].|Dati<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|Numero di byte del tipo di dati C<br /><br /> Numero di byte del tipo di dati C<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Data è compreso nell'intervallo del tipo di dati a cui il numero viene convertito [a]<br /><br /> I dati non rientra nell'intervallo del tipo di dati a cui il numero viene convertito [a]<br /><br /> I dati non sono un *letterali numerici*[b].|Dati<br /><br /> Non definito<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, inferiore a 2 e non è uguale a 1<br /><br /> I dati sono minore di 0 oppure maggiore o uguale a 2<br /><br /> I dati non sono un *letterali numerici*|Dati<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|1[b]<br /><br /> 1[b]<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Dati<br /><br /> Dati troncati|Lunghezza in byte dei dati<br /><br /> Lunghezza dei dati|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Valore dei dati è un valido *valore di data*[a]<br /><br /> Valore dei dati è un valido *valore di timestamp*; la parte dell'ora è uguale a zero [a]<br /><br /> Valore dei dati è un valido *valore di timestamp*; la parte dell'ora è diverso da zero [a], [c]<br /><br /> Valore di dati non valido *valore di data* oppure *valore timestamp*[a]|Dati<br /><br /> Dati<br /><br /> Dati troncati<br /><br /> Non definito|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Non definito|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Valore dei dati è un valido *valore di ora e i valore è 0 i secondi frazionari*[a]<br /><br /> Valore dei dati è un valido *valore di timestamp o un valore di ora valido*; frazionari parte relativa ai secondi è pari a zero [a], [d]<br /><br /> Valore dei dati è un valido *valore di timestamp*; frazionari parte relativa ai secondi è diverso da zero [a], [d], [e]<br /><br /> Valore di dati non valido *valore di ora* oppure *valore timestamp*[a]|Dati<br /><br /> Dati<br /><br /> Dati troncati<br /><br /> Non definito|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Non definito|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|Valore dei dati è un valido *valore di timestamp o un valore di ora valido*; frazionari parte relativa ai secondi non troncato [a]<br /><br /> Valore dei dati è un valido *valore di timestamp o un valore di ora valido*; frazionari parte relativa ai secondi troncato [a]<br /><br /> Valore dei dati è un valido *valore di data*[a]<br /><br /> Valore dei dati è un valido *valore di ora*[a]<br /><br /> Valore di dati non valido *valore di data*, *valore di ora*, o *valore timestamp*[a]|Dati<br /><br /> Dati troncati<br /><br /> Data[f]<br /><br /> Dati [g]<br /><br /> Non definito|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Tutti i tipi di intervallo C|Valore dei dati è un valido *valore dell'intervallo*; nessun troncamento<br /><br /> Valore dei dati è un valido *valore dell'intervallo*; il troncamento di uno o più campi finali<br /><br /> I dati sono intervallo valido. campo significativi precisione iniziale viene persa<br /><br /> Il valore dei dati non è un valore di intervallo valido|Dati<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] questa è la dimensione del tipo di dati C corrispondente.  
  
 [c] la porzione dell'ora il *valore di timestamp* viene troncato.  
  
 [d] la parte relativa alla data del *valore di timestamp* viene ignorato.  
  
 [e] la parte frazionaria dei secondi del timestamp viene troncata.  
  
 [f] i campi di tempo della struttura di timestamp sono impostati su zero.  
  
 [g] i campi data della struttura di timestamp sono impostati sulla data corrente.  

**Spazi aggiuntivi**

Spazi iniziali e finali vengono ignorati quando dati carattere SQL vengono convertiti in uno qualsiasi dei tipi seguenti:

- Data
- NUMERIC
- time
- TIMESTAMP
- dati di intervallo C
