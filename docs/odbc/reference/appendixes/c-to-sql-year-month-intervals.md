---
title: 'Da C a SQL: Intervalli anno-mese Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306612"
---
# <a name="c-to-sql-year-month-intervals"></a>Da C a SQL: intervalli anno-mese
Gli identificatori per i tipi di dati ODBC C dell'intervallo anno-mese sono:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati dell'intervallo C dell'anno-mese. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[aa]<br /><br /> SQL_LONGVARCHAR[a]|Lunghezza byte colonna >: lunghezza byte carattere<br /><br /> Lunghezza byte colonna < Lunghezza byte carattere[a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo validoData value is not a valid interval literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Lunghezza carattere colonna >: lunghezza dei caratteri dei dati<br /><br /> Lunghezza carattere colonna < Lunghezza del carattere dei dati[a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo validoData value is not a valid interval literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|La conversione di un intervallo a campo singolo non ha comportato il troncamento di cifre intere<br /><br /> La conversione ha comportato il troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Il valore dei dati è stato convertito senza troncamento dei campi<br /><br /> Uno o più campi del valore di dati sono stati troncati durante la conversione|n/d<br /><br /> 22015|  
  
 [a] Tutti i tipi di dati dell'intervallo C possono essere convertiti in un tipo di dati carattere.  
  
 [b] Se il campo type nella struttura dell'intervallo è tale che l'intervallo è un singolo campo (SQL_YEAR o SQL_MONTH), il tipo di intervallo C può essere convertito in qualsiasi numero esatto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversione predefinita di un tipo di intervallo C è nel tipo SQL di intervallo anno-mese corrispondente.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati di intervallo C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati dell'intervallo C. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
