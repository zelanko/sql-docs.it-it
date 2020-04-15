---
title: 'Da SQL a C: Data Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296531"
---
# <a name="sql-to-c-date"></a>Da SQL a C: data
L'identificatore per il tipo di dati SQL ODBC data è:  
  
 SQL_TYPE_DATE  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL data. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > Lunghezza byte del carattere<br /><br /> 11 <- *<BufferLength* - Lunghezza byte carattere<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Lunghezza dei caratteri<br /><br /> 11 <- *bufferLength* <- Lunghezza dei caratteri<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nessuno[a]|Data|6[c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno[a]|Dati[b]|16[c]|n/d|  
  
 Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] I campi relativi all'ora della struttura timestamp sono impostati su zero.  
  
 [c] Questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL di data vengono convertiti in dati di tipo c, la stringa risultante è nel formato "*aaaa*-*mm*-*gg*". Questo formato non è interessato dall'impostazione del paese di Windows®.
