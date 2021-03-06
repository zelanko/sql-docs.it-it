---
description: 'Da C a SQL: GUID'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fca2ba20df65222eaf1ce6f4384f449a1524334
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499984"
---
# <a name="c-to-sql-guid"></a>Da C a SQL: GUID
Identificatore per il tipo di dati C ODBC GUID:  
  
 SQL_C_GUID  
  
 Nella tabella seguente sono illustrati i tipi di dati ODBC SQL in cui è possibile convertire i dati GUID C. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore del tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Lunghezza byte colonna >= 36|n/d|  
|SQL_VARCHAR|Lunghezza in byte della colonna < 36|22001|  
|SQL_LONGVARCHAR|Il valore dei dati non è un GUID valido|22018|  
|SQL_WCHAR|Lunghezza carattere colonna >= 36|n/d|  
|SQL_WVARCHAR|Lunghezza carattere colonna < 36|22001|  
|SQL_WLONGVARCHAR|Il valore dei dati non è un GUID valido|22018|  
|SQL_GUID|Nessuno [a]|n/d|  
  
 [a] tutti i valori di esadecimali sono validi come GUID.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati GUID C e presuppone che le dimensioni del buffer dei dati siano le dimensioni del tipo di dati GUID C. Il valore di lunghezza/indicatore viene passato nell'argomento *StrLen_Or_Ind* in **SQLPutData** e nel buffer specificato con l'argomento *StrLen_or_IndPtr* in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
