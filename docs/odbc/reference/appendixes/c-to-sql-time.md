---
title: 'Da C a SQL: Tempo | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4a3734ff8d9f0cb120e1d33433ee3a301bb59ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019297"
---
# <a name="c-to-sql-time"></a>Da C a SQL: Time
È l'identificatore per il tipo di dati ODBC C fase:  
  
 SQL_C_TYPE_TIME  
  
 La tabella seguente illustra il codice SQL ODBC dei tipi di dati a cui possono essere convertiti i dati della fase C. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte di colonna > = 8<br /><br /> Colonna di lunghezza < 8 byte<br /><br /> Valore di dati non è valida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza in caratteri colonna > = 8<br /><br /> Colonna carattere a lunghezza < 8<br /><br /> Valore di dati non è valida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Valore dei dati è un'ora valida<br /><br /> Valore di dati non è valida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valore dei dati è un'ora valida [a]<br /><br /> Valore di dati non è valida|n/d<br /><br /> 22007|  
  
 [a] la data della parte del timestamp è impostata la data corrente e i secondi frazionari parte del timestamp è impostato su zero.  
  
 Per informazioni su quali valori sono validi in una struttura SQL_C_TYPE_TIME, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md), più indietro in questa appendice.  
  
 Quando i dati ora C viene convertiti in dati SQL di tipo carattere, i dati di tipo carattere risultante sono nel "*hh*:*mm*:*ss*" formato.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal momento in cui tipo di dati C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati ora C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
