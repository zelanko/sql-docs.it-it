---
title: 'Da C a SQL: Timestamp | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a738712a8fb1b032ef8244f579b10fdcc22becee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241425"
---
# <a name="c-to-sql-timestamp"></a>Da C a SQL: Timestamp
L'identificatore per il tipo di dati C ODBC timestamp è:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 La tabella seguente illustra il codice SQL ODBC i tipi di dati a cui possono essere convertiti i dati C di timestamp. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte di colonna > = lunghezza in byte di caratteri<br /><br /> 19 < = lunghezza in byte colonna < lunghezza in byte di caratteri<br /><br /> Colonna di lunghezza < 19 byte<br /><br /> Valore di dati non è un timestamp valido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza in caratteri colonna > = lunghezza in caratteri di dati<br /><br /> 19 < = lunghezza in caratteri colonna < lunghezza dei dati in caratteri<br /><br /> Colonna carattere a lunghezza < 19<br /><br /> Valore di dati non è un timestamp valido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|I campi dell'ora sono pari a zero<br /><br /> I campi dell'ora sono diversi da zero<br /><br /> Valore di dati non contiene una data valida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|I campi i secondi frazionari sono pari a zero [a]<br /><br /> I campi i secondi frazionari sono diversi da zero [a]<br /><br /> Valore di dati non contiene un'ora valida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|I campi i secondi frazionari non vengono troncati<br /><br /> I campi i secondi frazionari vengono troncati<br /><br /> Valore di dati non è un timestamp valido|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [a] data i campi della struttura di timestamp vengono ignorati.  
  
 Per informazioni su quali valori sono validi in una struttura SQL_C_TIMESTAMP, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md), più indietro in questa appendice.  
  
 Quando i dati di timestamp C viene convertiti in dati SQL di tipo carattere, i dati di tipo carattere risultante sono nel "*yyyy*-*mm*-*gg* *hh*:*mm*:*ss*[.*f...*] "formato.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal tipo di dati timestamp C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati timestamp C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
