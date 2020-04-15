---
title: 'Da C a SQL: Timestamp Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283751"
---
# <a name="c-to-sql-timestamp"></a>Da C a SQL: timestamp
L'identificatore per il tipo di dati ODBC C timestamp è:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati timestamp C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza byte colonna >: lunghezza byte carattere<br /><br /> 19 <- Lunghezza byte colonna < Lunghezza byte carattere<br /><br /> Lunghezza byte colonna < 19<br /><br /> Il valore dei dati non è un timestamp valido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza carattere colonna >: lunghezza dei caratteri dei dati<br /><br /> 19 <- Lunghezza dei caratteri di colonna < Lunghezza dei caratteri dei dati<br /><br /> Lunghezza carattere colonna < 19<br /><br /> Il valore dei dati non è un timestamp valido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|I campi Ora sono pari a zero<br /><br /> I campi Ora sono diversi da zero<br /><br /> Il valore dei dati non contiene una data valida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|I campi dei secondi frazionari sono zero[a]<br /><br /> I campi dei secondi frazionari sono diversi da zero[a]<br /><br /> Il valore dei dati non contiene un'ora valida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|I campi dei secondi frazionari non vengono troncati<br /><br /> I campi dei secondi frazionari vengono troncati<br /><br /> Il valore dei dati non è un timestamp valido|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [a] I campi data della struttura timestamp vengono ignorati.  
  
 Per informazioni sui valori validi in una struttura SQL_C_TIMESTAMP, vedere [Tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md), più indietro in questa appendice.  
  
 Quando i dati di timestamp C vengono convertiti in dati SQL di tipo carattere, i dati di tipo carattere risultante si trova nel "*aaaa*-*mm*-*gg* *hh*:*mm*:*ss*[.* f...*]" Formato.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati timestamp C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati timestamp C. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
