---
title: 'Da C a SQL: GUID Documenti Microsoft'
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
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306622"
---
# <a name="c-to-sql-guid"></a>Da C a SQL: GUID
L'identificatore per il tipo di dati GUID ODBC C è:  
  
 SQL_C_GUID  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati GUID C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Lunghezza byte colonna >|n/d|  
|SQL_VARCHAR|Lunghezza byte colonna < 36|22001|  
|SQL_LONGVARCHAR|Il valore dei dati non è un GUID valido|22018|  
|SQL_WCHAR|Lunghezza dei caratteri di colonna >- 36|n/d|  
|SQL_WVARCHAR|Lunghezza carattere colonna < 36|22001|  
|SQL_WLONGVARCHAR|Il valore dei dati non è un GUID valido|22018|  
|SQL_GUID|Nessuno[a]|n/d|  
  
 Tutti i valori esadecimali sono validi come GUID.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati GUID C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati GUID C. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
