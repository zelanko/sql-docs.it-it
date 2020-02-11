---
title: 'Da SQL a C: timestamp | Microsoft Docs'
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
ms.openlocfilehash: ee3852c688f495d54eb07ca9c2866ac17a1f5a1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118841"
---
# <a name="sql-to-c-timestamp"></a>Da SQL a C: timestamp

L'identificatore per il tipo di dati timestamp ODBC SQL è il seguente:

- SQL_TYPE_TIMESTAMP  

Nella tabella seguente sono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati di timestamp SQL. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Lunghezza in byte *BufferLength* > caratteri<br /><br /> 20 <= *BufferLength* <= lunghezza in byte carattere<br /><br /> *BufferLength* < 20|data<br /><br /> Dati troncati [b]<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri > *bufferLength*<br /><br /> 20 <= *BufferLength* <= Lunghezza carattere<br /><br /> *BufferLength* < 20|data<br /><br /> Dati troncati [b]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <= *bufferLength*<br /><br /> Lunghezza in byte dei dati > *bufferLength*|data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|La parte relativa all'ora del timestamp è zero [a]<br /><br /> La parte relativa all'ora del timestamp è diversa da zero [a]|data<br /><br /> Dati troncati [c]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|La parte relativa ai secondi frazionari del timestamp è zero [a]<br /><br /> La parte relativa ai secondi frazionari del timestamp è diversa da zero [a]|Dati [d]<br /><br /> Dati troncati [d], [e]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|La parte relativa ai secondi frazionari del timestamp non è troncata [a]<br /><br /> Il timestamp della parte relativa ai secondi frazionari è troncato [a]|Dati [e]<br /><br /> Dati troncati [e]|16 [f]<br /><br /> 16 [f]|n/d<br /><br /> 01S07|  

 [a] il valore di *bufferLength* viene ignorato per la conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* siano le dimensioni del tipo di dati C.  
  
 [b] i secondi frazionari del timestamp vengono troncati.  
  
 [c] la parte relativa all'ora del timestamp viene troncata.  
  
 [d] la parte relativa alla data del timestamp viene ignorata.  
  
 [e] la parte relativa ai secondi frazionari del timestamp viene troncata.  
  
 [f] corrisponde alla dimensione del tipo di dati C corrispondente.  

Quando i dati timestamp SQL vengono convertiti in dati di tipo carattere C, la stringa risultante si trova in "*aaaa*-*mm*-*GG* *HH*:*mm*:*SS*[.* f...*] " formato, in cui è possibile utilizzare fino a nove cifre per i secondi frazionari. Questo formato non è influenzato dall'impostazione di Windows® Country. (Ad eccezione del separatore decimale e dei secondi frazionari, è necessario utilizzare l'intero formato, indipendentemente dalla precisione del tipo di dati timestamp SQL).
