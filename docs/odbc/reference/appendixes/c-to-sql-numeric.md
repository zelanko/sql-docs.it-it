---
title: 'Da C a SQL: Numerico | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816394bb8469148504c1b2b416e77fec814bef8f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191741"
---
# <a name="c-to-sql-numeric"></a>Da C a SQL: Numeric
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
  
 La tabella seguente illustra il codice SQL ODBC dei tipi di dati a cui possono essere convertiti i dati numerici di C. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Numero di cifre < = lunghezza di colonna in byte<br /><br /> Numero di cifre > lunghezza di colonna in byte|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Numero di caratteri < = lunghezza in caratteri colonna<br /><br /> Numero di caratteri > lunghezza in caratteri colonna|n/d<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|Conversione senza troncamento o con troncamento delle cifre frazionarie dei dati<br /><br /> I dati convertiti con troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Data è compreso nell'intervallo del tipo di dati a cui il numero viene convertito<br /><br /> I dati non rientra nell'intervallo del tipo di dati a cui il numero viene convertito|n/d<br /><br /> 22003|  
|SQL_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, inferiore a 2 e non è uguale a 1<br /><br /> I dati sono minore di 0 oppure maggiore o uguale a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|Dati non è stati troncati.<br /><br /> Dati troncati.|n/d<br /><br /> 22015|  
  
 [a] queste conversioni sono supportate solo per i tipi di dati numerici esatti (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC). Non sono supportati per i tipi di dati numerico approssimato (SQL_C_FLOAT o SQL_C_DOUBLE). Tipi di dati C numerici esatti Impossibile convertire in un intervallo di tipo SQL il cui intervallo di precisione non è un singolo campo.  
  
 [b] per il caso di "n/d", un driver facoltativamente restituiscono SQL_SUCCESS_WITH_INFO e 01S07 quando si verifica un troncamento frazionario.  
  
 Il driver ignora il valore di lunghezza/indicatore quando si convertono i dati dai tipi di dati numerici di C e si presuppone che la dimensione del buffer di dati è la dimensione del tipo di dati numerico di C. Viene passato il valore di lunghezza/indicatore il *StrLen_or_Ind* nell'argomento **SQLPutData** e nel buffer specificato con il *StrLen_or_IndPtr* argomento in **SQLBindParameter**. Il buffer dei dati è specificato con il *DataPtr* nell'argomento **SQLPutData** e il *ParameterValuePtr* argomento in **SQLBindParameter**.
