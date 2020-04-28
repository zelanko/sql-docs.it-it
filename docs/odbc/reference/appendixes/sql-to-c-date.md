---
title: 'Da SQL a C: data | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296531"
---
# <a name="sql-to-c-date"></a>Da SQL a C: data
L'identificatore per il tipo di dati SQL ODBC data è il seguente:  
  
 SQL_TYPE_DATE  
  
 Nella tabella seguente sono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati di SQL Data. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Lunghezza in byte *BufferLength* > caratteri<br /><br /> 11 <= *BufferLength* <= lunghezza in byte carattere<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Lunghezza in caratteri > *bufferLength*<br /><br /> 11 <= *BufferLength* <= Lunghezza carattere<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati <= *bufferLength*<br /><br /> Lunghezza in byte dei dati > *bufferLength*|Data<br /><br /> Non definito|Lunghezza dei dati in byte<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nessuno [a]|Data|6 [c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno [a]|Dati [b]|16 [c]|n/d|  
  
 [a] il valore di *bufferLength* viene ignorato per la conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* siano le dimensioni del tipo di dati C.  
  
 [b] i campi di tempo della struttura timestamp sono impostati su zero.  
  
 [c] corrisponde alla dimensione del tipo di dati C corrispondente.  
  
 Quando i dati di data SQL vengono convertiti in dati di tipo carattere C, la stringa risultante è nel formato "*aaaa*-*mm*-*GG*". Questo formato non è influenzato dall'impostazione di Windows® Country.
