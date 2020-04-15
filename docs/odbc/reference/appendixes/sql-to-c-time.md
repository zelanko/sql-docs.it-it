---
title: 'Da SQL a C: Tempo Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296381"
---
# <a name="sql-to-c-time"></a>Da SQL a C: ora
L'identificatore per il tipo di dati SQL ODBC è:  
  
 SQL_TYPE_TIME  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > Lunghezza byte del carattere<br /><br /> *9* <= *BufferLength* <- Lunghezza byte carattere<br /><br /> *BufferLength* < 9|Data<br /><br /> Dati troncati[a]<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Lunghezza dei caratteri<br /><br /> *9* <= *<BufferLength* - Lunghezza carattere<br /><br /> *BufferLength* < 9|Data<br /><br /> Dati troncati[a]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nessuno[b]|Data|6[d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno[b]|Dati[c]|16[d]|n/d|  
  
 [a] I secondi frazionari dell'ora vengono troncati.  
  
 [b] Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [c] I campi data della struttura timestamp sono impostati sulla data corrente e il campo dei secondi frazionari della struttura timestamp è impostato su zero.  
  
 [d] Questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL vengono convertiti in dati di tipo C, la stringa risultante è nel formato "*hh*:*mm*:*ss*". Questo formato non è interessato dall'impostazione del paese di Windows®.
