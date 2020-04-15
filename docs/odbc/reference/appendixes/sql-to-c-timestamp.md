---
title: 'Da SQL a C: Timestamp . Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296351"
---
# <a name="sql-to-c-timestamp"></a>Da SQL a C: timestamp

L'identificatore per il tipo di dati ODBC SQL timestamp è il seguente:

- SQL_TYPE_TIMESTAMP  

Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL timestamp. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > Lunghezza byte del carattere<br /><br /> 20 <- *bufferLength* <- Lunghezza byte carattere<br /><br /> *BufferLength* < 20|Data<br /><br /> Dati troncati[b]<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Lunghezza dei caratteri<br /><br /> 20 <- *<BufferLength* - Lunghezza dei caratteri<br /><br /> *BufferLength* < 20|Data<br /><br /> Dati troncati[b]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|La parte relativa all'ora del timestamp è zero[a]<br /><br /> La parte relativa all'ora del timestamp è diversa da zero[a]|Data<br /><br /> Dati troncati[c]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07 (intito)|  
|SQL_C_TYPE_TIME|La parte dei secondi frazionari del timestamp è zero[a]<br /><br /> La parte relativa ai secondi frazionari del timestamp è diversa da zero[a]|Dati[d]<br /><br /> Dati troncati[d], [e]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07 (intito)|  
|SQL_C_TYPE_TIMESTAMP|La parte relativa ai secondi frazionari del timestamp non viene troncata[a]<br /><br /> La parte relativa ai secondi frazionari del timestamp viene troncata[a]|Dati[e]<br /><br /> Dati troncati[e]|16[f]<br /><br /> 16[f]|n/d<br /><br /> 01S07 (intito)|  

 Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] I secondi frazionari del timestamp vengono troncati.  
  
 [c] La parte relativa all'ora del timestamp viene troncata.  
  
 [d] La parte relativa alla data del timestamp viene ignorata.  
  
 [e] La parte dei secondi frazionari del timestamp viene troncata.  
  
 [f] Questa è la dimensione del tipo di dati C corrispondente.  

Quando i dati SQL timestamp vengono convertiti in dati di tipo carattere C, la stringa risultante si trova nel "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*]" formato, in cui è possibile utilizzare fino a nove cifre per i secondi frazionari. Questo formato non è interessato dall'impostazione del paese di Windows®. (Ad eccezione del separatore decimale e dei secondi frazionari, è necessario utilizzare l'intero formato, indipendentemente dalla precisione del tipo di dati SQL timestamp.)
