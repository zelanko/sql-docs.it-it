---
title: 'Da SQL a C: Carattere Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296671"
---
# <a name="sql-to-c-character"></a>Da SQL a C: carattere

Gli identificatori per i tipi di dati SQL ODBC carattere sono i seguenti:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire dati SQL di tipo carattere. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore del tipo C|Test|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Lunghezza in byte dei dati < *BufferLength*<br /><br /> Lunghezza in byte dei dati >- *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Lunghezza dei caratteri dei dati < *BufferLength*<br /><br /> Lunghezza dei caratteri dei dati >: *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Dati convertiti senza troncamento[b]<br /><br /> Dati convertiti con troncamento delle cifre frazionarie[a]<br /><br /> La conversione dei dati comporterebbe la perdita di cifre intere (anziché frazionarie)[a]<br /><br /> I dati non sono valori *numerici*[b]|Data<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|Numero di byte del tipo di dati C<br /><br /> Numero di byte del tipo di dati C<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|I dati sono compresi nell'intervallo del tipo di dati in cui viene convertito il numero[a]<br /><br /> I dati non rientrano nell'intervallo del tipo di dati in cui viene convertito il numero[a]<br /><br /> I dati non sono valori *numerici*[b]|Data<br /><br /> Non definito<br /><br /> Non definito|Dimensione del tipo di dati C<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, minori di 2 e non uguali a 1<br /><br /> I dati sono minori di 0 o maggiori o uguali a 2<br /><br /> I dati non sono valori *numerici*|Data<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|1[b]<br /><br /> 1[b]<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Il valore dei dati è un *valore di data*valido [a]<br /><br /> Il valore dei dati è un *timestamp-value*valido; la parte relativa all'ora è zero[a]<br /><br /> Il valore dei dati è un *timestamp-value*valido; time portion è diverso da zero[a],[c]<br /><br /> Il valore dei dati non è un *valore di data* o un *timestamp-value*valido [a]|Data<br /><br /> Data<br /><br /> Dati troncati<br /><br /> Non definito|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Non definito|n/d<br /><br /> n/d<br /><br /> 01S07 (intito)<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Il valore dei dati è un valore di tempo valido *e il valore dei secondi frazionari è 0*[a]<br /><br /> Il valore dei dati è un *timestamp-value*valido o un valore di ora valido. la parte dei secondi frazionari è zero[a],[d]<br /><br /> Il valore dei dati è un *timestamp-value*valido; la parte dei secondi frazionari è diversa da zero[a],[d],[e]<br /><br /> Il valore dei dati non è un *valore di ora* valido o *timestamp-valore*[a]|Data<br /><br /> Data<br /><br /> Dati troncati<br /><br /> Non definito|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Non definito|n/d<br /><br /> n/d<br /><br /> 01S07 (intito)<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|Il valore dei dati è un *timestamp-value*valido o un valore di ora valido. parte dei secondi frazionari non troncata[a]<br /><br /> Il valore dei dati è un *timestamp-value*valido o un valore di ora valido. parte dei secondi frazionari troncata[a]<br /><br /> Il valore dei dati è un *valore di data*valido [a]<br /><br /> Il valore dei dati è un *valore di tempo*valido [a]<br /><br /> Il valore dei dati non è un valore di *data,* un *valore di ora*o un *timestamp-value*[a]|Data<br /><br /> Dati troncati<br /><br /> Dati[f]<br /><br /> Dati[g]<br /><br /> Non definito|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Tutti i tipi di intervallo C|Il valore dei dati è un valore di *intervallo*valido; nessun troncamento<br /><br /> Il valore dei dati è un valore di *intervallo*valido; troncamento di uno o più campi finali<br /><br /> I dati sono intervalli validi; campo di primo piano si perde la precisione significativa del campo<br /><br /> Il valore dei dati non è un valore di intervallo valido|Data<br /><br /> Dati troncati<br /><br /> Non definito<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito<br /><br /> Non definito|n/d<br /><br /> 01S07 (intito)<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] Questa è la dimensione del tipo di dati C corrispondente.  
  
 [c] La parte relativa all'ora del *timestamp-value* viene troncata.  
  
 [d] La parte relativa alla data del *timestamp-value* viene ignorata.  
  
 [e] La parte dei secondi frazionari del timestamp viene troncata.  
  
 [f] I campi relativi all'ora della struttura timestamp sono impostati su zero.  
  
 [g] I campi data della struttura timestamp sono impostati sulla data corrente.  

**Spazi extra**

Gli spazi iniziali e finali vengono ignorati quando i dati di tipo carattere SQL vengono convertiti in uno dei tipi seguenti:

- Data
- NUMERIC
- time
-  timestamp
- dati di intervallo C
