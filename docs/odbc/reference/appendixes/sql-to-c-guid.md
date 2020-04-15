---
title: 'Da SQL a C: GUID Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296461"
---
# <a name="sql-to-c-guid"></a>Da SQL a C: GUID
L'identificatore per il tipo di dati SQL ODBC GUID è:  
  
 SQL_GUID  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati GUID SQL. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > Lunghezza byte del carattere|Data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_WCHAR|*BufferLength* > Lunghezza dei caratteri|Data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_BINARY|Lunghezza in \< = byte dei dati *BufferLength*|Data|Lunghezza dei dati in byte|n/d|  
||Lunghezza in byte dei dati > *BufferLength*|Non definito|Non definito|22003|  
|SQL_C_GUID|Nessuno[a]|Data|16[b]|n/d|  
  
 Il valore di *BufferLength* viene ignorato per questa conversione. Il driver presuppone che la dimensione di*TargetValuePtr* è la dimensione del tipo di dati C.  
  
 [b] Questa è la dimensione del tipo di dati C corrispondente.
