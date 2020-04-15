---
title: 'Da C a SQL: Numerico Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbc0a994ef95f2deca29c8a4cbb06f3167b0433f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304732"
---
# <a name="c-to-sql-numeric"></a>Da C a SQL: dati numerici
Gli identificatori per i tipi di dati C ODBC numerici sono:  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui possono essere convertiti dati Numeric C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Numero di cifre <- Lunghezza byte colonna<br /><br /> Numero di cifre > lunghezza byte colonna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Numero di caratteri <- Lunghezza carattere colonna<br /><br /> Numero di caratteri > lunghezza dei caratteri di colonna|n/d<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|Dati convertiti senza troncamento o con troncamenti di cifre frazionarie<br /><br /> Dati convertiti con troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|I dati rientrano nell'intervallo del tipo di dati in cui viene convertito il numero<br /><br /> I dati non rientrano nell'intervallo del tipo di dati in cui viene convertito il numero|n/d<br /><br /> 22003|  
|SQL_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, minori di 2 e non uguali a 1<br /><br /> I dati sono minori di 0 o maggiori o uguali a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|Dati non troncati.<br /><br /> Dati troncati.|n/d<br /><br /> 22015|  
  
 Queste conversioni sono supportate solo per i tipi di dati numerici esatti (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC). Non sono supportati per i tipi di dati numerici approssimativi (SQL_C_FLOAT o SQL_C_DOUBLE). I tipi di dati numerici C non possono essere convertiti in un tipo SQL a intervalli la cui precisione di intervallo non è un singolo campo.  
  
 [b] Per il caso "n/a", un driver può facoltativamente restituire SQL_SUCCESS_WITH_INFO e 01S07 quando è presente un troncamento frazionario.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dai tipi di dati Numeric C e presuppone che la dimensione del buffer di dati sia la dimensione del tipo di dati C numerico. Il valore di lunghezza/indicatore viene passato nel *StrLen_or_Ind* argomento in **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
