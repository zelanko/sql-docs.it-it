---
title: 'Da SQL a C: Data | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d282798a31ac9059ed3c1901ea01f1f3104f09c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056878"
---
# <a name="sql-to-c-date"></a>Da SQL a C: Date
L'identificatore per il tipo di dati SQL ODBC Data è:  
  
 SQL_TYPE_DATE  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui può essere convertito i dati di SQL Data. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > lunghezza in byte di caratteri<br /><br /> 11 < = *BufferLength* < = lunghezza in byte di caratteri<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > lunghezza in caratteri<br /><br /> 11 < = *BufferLength* < = lunghezza in caratteri<br /><br /> *BufferLength* < 11|Data<br /><br /> Dati troncati<br /><br /> Non definito|10<br /><br /> Lunghezza dei dati in caratteri<br /><br /> Non definito|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Data<br /><br /> Non definito|Lunghezza in byte dei dati<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nessuno [a]|Data|6[c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nessuno [a]|Dati [b]|16[c]|n/d|  
  
 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] i campi di tempo della struttura di timestamp sono impostati su zero.  
  
 [c] questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati di SQL Data viene convertito in dati di tipo carattere C, la stringa risultante è nel "*yyyy*-*mm*-*gg*" formato. Questo formato non è interessato dall'impostazione paese Windows®.
