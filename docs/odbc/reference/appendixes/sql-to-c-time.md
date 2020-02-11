---
title: 'Da SQL a C: ora | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065085"
---
# <a name="sql-to-c-time"></a>Da SQL a C: ora
Identificatore per il tipo di dati time ODBC SQL:  
  
 SQL_TYPE_TIME  
  
 Nella tabella seguente sono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Lunghezza in byte *BufferLength* > caratteri<br /><br /> *9* <= *bufferLength* <= lunghezza in byte carattere<br /><br /> *BufferLength* < 9|data<br /><br /> Dati troncati [a]<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri > *bufferLength*<br /><br /> *9* <= *bufferLength* <= Lunghezza carattere<br /><br /> *BufferLength* < 9|data<br /><br /> Dati troncati [a]<br /><br /> Non definito|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <= *bufferLength*<br /><br /> Lunghezza in byte dei dati > *bufferLength*|data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nessuno [b]|data|6 [d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno [b]|Dati [c]|16 [d]|n/d|  
  
 [a] i secondi frazionari del tempo vengono troncati.  
  
 [b] il valore di *bufferLength* viene ignorato per la conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* siano le dimensioni del tipo di dati C.  
  
 [c] i campi relativi alla data della struttura del timestamp vengono impostati sulla data corrente e il campo dei secondi frazionari della struttura del timestamp è impostato su zero.  
  
 [d] corrisponde alla dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL vengono convertiti in dati di tipo carattere C, la stringa risultante si trova nel formato "*HH*:*mm*:*SS*". Questo formato non è influenzato dall'impostazione di Windows® Country.
