---
title: 'Da C a SQL: Intervalli anno-mese | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d12727f9298eb63fe10b44c48b9d3b7996a839d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159283"
---
# <a name="c-to-sql-year-month-intervals"></a>Da C a SQL: intervalli anno-mese
Gli identificatori per i tipi di dati ODBC C intervallo anno-mese sono:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 La tabella seguente illustra il codice SQL ODBC i tipi di dati per anno-mese in cui i dati di intervallo C possono essere convertiti. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Lunghezza in byte di colonna > = lunghezza in byte di caratteri<br /><br /> Lunghezza in byte colonna < [a] lunghezza in byte di caratteri<br /><br /> Valore di dati non è un intervallo valido di valore letterale|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Lunghezza in caratteri colonna > = lunghezza in caratteri di dati<br /><br /> Lunghezza in caratteri colonna < lunghezza dei dati [a] in caratteri<br /><br /> Valore di dati non è un intervallo valido di valore letterale|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|Conversione di un intervallo di un solo campo non ha restituito il troncamento di cifre intere<br /><br /> Conversione comportato il troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Valore dei dati è stato convertito senza troncamento di tutti i campi<br /><br /> Uno o più campi del valore dei dati sono stati troncati durante la conversione|n/d<br /><br /> 22015|  
  
 [a] tipi di dati di intervallo C tutto possono essere convertito in un tipo di dati carattere.  
  
 [b] se il campo di tipo nella struttura di intervallo è tale che l'intervallo è un singolo campo (SQL_YEAR o SQL_MONTH), il tipo di intervallo C può essere convertito in qualsiasi numerico esatto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversione predefinita di un intervallo di tipo C è l'intervallo anno-mese corrispondente tipo SQL.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dal tipo di dati di intervallo C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati di intervallo C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
