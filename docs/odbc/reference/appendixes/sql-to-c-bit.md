---
title: 'Da SQL a C: Bit | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7ff0bd2988460596623eb47ded276392dc3d443
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270974"
---
# <a name="sql-to-c-bit"></a>Da SQL a C: bit
L'identificatore per il tipo di dati SQL ODBC bit è:  
  
 SQL_BIT  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati SQL di bit. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* <= 1|Dati<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|None[a]|Dati|Dimensione del tipo di dati C|n/d|  
|SQL_C_BIT|None[a]|Dati|1[b]|n/d|  
|SQL_C_BINARY|*BufferLength* >= 1<br /><br /> *BufferLength* < 1|Dati<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
  
 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL bit viene convertiti in dati di tipo carattere C, i valori possibili sono "0" e "1".
