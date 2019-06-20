---
title: 'Da C a SQL: Data | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8edb075be1bf64dad8f4ef18924a6396b7c64e80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294364"
---
# <a name="c-to-sql-date"></a>Da C a SQL: Date
L'identificatore per il tipo di dati C ODBC Data è:  
  
 SQL_C_TYPE_DATE  
  
 La tabella seguente illustra il codice SQL ODBC i tipi di dati a cui data di dati C può essere convertito. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte di colonna > = 10<br /><br /> Colonna di lunghezza < 10 byte<br /><br /> Valore di dati non è una data valida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza in caratteri colonna > = 10<br /><br /> Colonna carattere a lunghezza < 10<br /><br /> Valore di dati non è una data valida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Valore dei dati è una data valida<br /><br /> Valore di dati non è una data valida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valore dei dati è una data valida [a]<br /><br /> Valore di dati non è una data valida|n/d<br /><br /> 22007|  
  
 [a] parte relativa all'ora del timestamp è impostato su zero.  
  
 Per informazioni su quali valori sono validi in una struttura SQL_C_TYPE_DATE, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md), più indietro in questa appendice.  
  
 Quando i dati di data C viene convertiti in dati di SQL di tipo carattere, i dati di tipo carattere risultante sono nel "*yyyy*-*mm*-*gg*" formato.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal tipo di dati date C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati Data C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
