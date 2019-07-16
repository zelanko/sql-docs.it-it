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
ms.openlocfilehash: 8d00a3c26d842b196e20861da6d8ae3e818d4cbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056898"
---
# <a name="sql-to-c-bit"></a>Da SQL a C: Bit
L'identificatore per il tipo di dati SQL ODBC bit è:  
  
 SQL_BIT  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati SQL di bit. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* < = 1|Data<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Nessuno [a]|Data|Dimensione del tipo di dati C|n/d|  
|SQL_C_BIT|Nessuno [a]|Data|1[b]|n/d|  
|SQL_C_BINARY|*BufferLength* > = 1<br /><br /> *BufferLength* < 1|Data<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
  
 [a] hodnotou *BufferLength* viene ignorata per questa conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL bit viene convertiti in dati di tipo carattere C, i valori possibili sono "0" e "1".
