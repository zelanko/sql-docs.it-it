---
title: 'Da C a SQL: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5863935ddf595409d48be79dc646c0994ddeb0b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019318"
---
# <a name="c-to-sql-guid"></a>Da C a SQL: GUID
L'identificatore per il tipo di dati C ODBC GUID è:  
  
 SQL_C_GUID  
  
 La tabella seguente illustra il codice SQL ODBC dei tipi di dati a cui possono essere convertiti i dati di GUID C. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Lunghezza in byte di colonna > = 36|n/d|  
|SQL_VARCHAR|Colonna di lunghezza < 36 byte|22001|  
|SQL_LONGVARCHAR|Valore di dati non è un GUID valido|22018|  
|SQL_WCHAR|Lunghezza in caratteri colonna > = 36|n/d|  
|SQL_WVARCHAR|Colonna carattere a lunghezza < 36|22001|  
|SQL_WLONGVARCHAR|Valore di dati non è un GUID valido|22018|  
|SQL_GUID|Nessuno [a]|n/d|  
  
 [a] tutti i valori esadecimali sono validi come GUID.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal tipo di dati GUID C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati GUID C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
