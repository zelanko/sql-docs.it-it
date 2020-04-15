---
title: 'Da SQL a C: Bit Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296751"
---
# <a name="sql-to-c-bit"></a>Da SQL a C: bit
L'identificatore per il tipo di dati SQL ODBC bit è:  
  
 SQL_BIT  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL di bit. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* ><br /><br /> *bufferLength* <1|Data<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Nessuno[a]|Data|Dimensione del tipo di dati C|n/d|  
|SQL_C_BIT|Nessuno[a]|Data|1[b]|n/d|  
|SQL_C_BINARY|*bufferLength* >1<br /><br /> *BufferLength* <|Data<br /><br /> Non definito|1<br /><br /> Non definito|n/d<br /><br /> 22003|  
  
 Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] Questa è la dimensione del tipo di dati C corrispondente.  
  
 Quando i dati SQL bit vengono convertiti in dati di tipo carattere C, i valori possibili sono "0" e "1".
