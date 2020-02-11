---
title: 'Da SQL a C: GUID | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a2ed3cffcb196cb09841df3b54fbfab53e22477
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056869"
---
# <a name="sql-to-c-guid"></a>Da SQL a C: GUID
L'identificatore per il tipo di dati SQL ODBC GUID è:  
  
 SQL_GUID  
  
 Nella tabella seguente sono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati di SQL GUID. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Lunghezza in byte *BufferLength* > caratteri|data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_WCHAR|Lunghezza in caratteri > *bufferLength*|data|36|n/d|  
||*BufferLength* < 37|Non definito|Non definito|22003|  
|SQL_C_BINARY|Lunghezza in byte dei \< = dati *bufferLength*|data|Lunghezza dei dati in byte|n/d|  
||Lunghezza in byte dei dati > *bufferLength*|Non definito|Non definito|22003|  
|SQL_C_GUID|Nessuno [a]|data|16 [b]|n/d|  
  
 [a] il valore di *bufferLength* viene ignorato per la conversione. Il driver presuppone che le dimensioni di **TargetValuePtr* siano le dimensioni del tipo di dati C.  
  
 [b] corrisponde alla dimensione del tipo di dati C corrispondente.
