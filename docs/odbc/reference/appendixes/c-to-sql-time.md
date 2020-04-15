---
title: 'Da C a SQL: Tempo Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 264ce7751072b79163923f0c141542680f7b02bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304763"
---
# <a name="c-to-sql-time"></a>Da C a SQL: ora
L'identificatore per il tipo di dati ODBC C è:  
  
 SQL_C_TYPE_TIME  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza byte colonna >: 8<br /><br /> Lunghezza byte colonna < 8<br /><br /> Il valore dei dati non è un'ora validaData value is not a valid time|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza dei caratteri della colonna >- 8<br /><br /> Lunghezza carattere colonna < 8<br /><br /> Il valore dei dati non è un'ora validaData value is not a valid time|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Il valore dei dati è un'ora validaData value is a valid time<br /><br /> Il valore dei dati non è un'ora validaData value is not a valid time|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Il valore dei dati è un'ora valida[a]<br /><br /> Il valore dei dati non è un'ora validaData value is not a valid time|n/d<br /><br /> 22007|  
  
 [a] La parte relativa alla data del timestamp è impostata sulla data corrente e la parte dei secondi frazionari del timestamp è impostata su zero.  
  
 Per informazioni sui valori validi in una struttura SQL_C_TYPE_TIME, vedere [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md), più indietro in questa appendice.  
  
 Quando il tempo In cui i dati C vengono convertiti in dati SQL di tipo carattere, i dati di tipo carattere risultante sono nel formato "*hh*:*mm*:*ss*".  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati C. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
