---
title: 'Da SQL a C: Timestamp | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69c9f1258f35a69d6554783f5d1b4ca79be313d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259262"
---
# <a name="sql-to-c-timestamp"></a>Da SQL a C: Timestamp

L'identificatore per il tipo di dati SQL ODBC timestamp è il seguente:

- SQL_TYPE_TIMESTAMP  

La tabella seguente illustra i dati ODBC C i tipi di dati a cui possono essere convertiti dati timestamp SQL. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > lunghezza in byte di caratteri<br /><br /> 20 < = *BufferLength* < = lunghezza in byte di caratteri<br /><br /> *BufferLength* < 20|Dati<br /><br /> Dati troncati [b]<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > lunghezza in caratteri<br /><br /> 20 < = *BufferLength* < = lunghezza in caratteri<br /><br /> *BufferLength* < 20|Dati<br /><br /> Dati troncati [b]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Dati<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Parte relativa all'ora del timestamp è uguale a zero [a]<br /><br /> Parte relativa all'ora del timestamp è diverso da zero [a]|Dati<br /><br /> Dati troncati [c]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|Parte relativa ai secondi frazionari di timestamp è uguale a zero [a]<br /><br /> Parte relativa ai secondi frazionari di timestamp è diverso da zero [a]|Data[d]<br /><br /> Dati troncati [d], [e]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|Parte relativa ai secondi frazionari di timestamp non viene troncato [a]<br /><br /> Parte relativa ai secondi frazionari di timestamp viene troncato [a]|Dati [e]<br /><br /> Dati troncati [e]|16[f]<br /><br /> 16[f]|n/d<br /><br /> 01S07|  

 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] i secondi frazionari del timestamp vengono troncati.  
  
 [c] la parte relativa all'ora del timestamp viene troncato.  
  
 [d] la parte relativa alla data del timestamp viene ignorato.  
  
 [e] la parte frazionaria dei secondi del timestamp viene troncata.  
  
 [f] questa è la dimensione del tipo di dati C corrispondente.  

Quando i dati SQL timestamp viene convertiti in dati di tipo carattere C, la stringa risultante è nel "*yyyy*-*mm*-*gg* *hh* :*mm*:*ss*[.*f...*] "formato, dove può essere usato fino a nove cifre per i secondi frazionari. Questo formato non è interessato dall'impostazione paese Windows®. (Fatta eccezione per il separatore decimale e i secondi frazionari, il formato intero che sarà utilizzato, indipendentemente dalla precisione del tipo di dati timestamp SQL.)
