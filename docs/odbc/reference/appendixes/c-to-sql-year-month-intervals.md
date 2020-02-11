---
title: 'Da C a SQL: intervalli anno-mese | Microsoft Docs'
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
ms.openlocfilehash: 3db8d61bacefa8588db4c0081c6be591d7ffdacf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019281"
---
# <a name="c-to-sql-year-month-intervals"></a>Da C a SQL: intervalli anno-mese
Gli identificatori per i tipi di dati ODBC C con intervallo year-month sono:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC SQL per i quali è possibile convertire i dati dell'intervallo di anno mese C. Per una spiegazione delle colonne e dei termini della tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificatore del tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|Lunghezza byte colonna >= lunghezza byte carattere<br /><br /> Lunghezza in byte di colonna < lunghezza in byte carattere [a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo valido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|Lunghezza carattere colonna >= Lunghezza caratteri dei dati<br /><br /> Lunghezza carattere colonna < lunghezza di caratteri dei dati [a]<br /><br /> Il valore dei dati non è un valore letterale di intervallo valido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|La conversione di un intervallo a campo singolo non ha causato il troncamento di cifre intere<br /><br /> La conversione ha causato il troncamento di cifre intere|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Il valore dei dati è stato convertito senza troncamento dei campi<br /><br /> Uno o più campi del valore di dati sono stati troncati durante la conversione|n/d<br /><br /> 22015|  
  
 [a] tutti i tipi di dati intervallo C possono essere convertiti in un tipo di dati character.  
  
 [b] se il campo tipo nella struttura dell'intervallo è tale che l'intervallo è un singolo campo (SQL_YEAR o SQL_MONTH), il tipo intervallo C può essere convertito in un valore numerico esatto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversione predefinita di un tipo di intervallo C corrisponde al tipo SQL dell'intervallo anno mese corrispondente.  
  
 Il driver ignora il valore di lunghezza/indicatore durante la conversione dei dati dal tipo di dati interval C e presuppone che le dimensioni del buffer dei dati siano le dimensioni del tipo di dati interval C. Il valore di lunghezza/indicatore viene passato nell'argomento *StrLen_Or_Ind* in **SQLPutData** e nel buffer specificato con l'argomento *StrLen_or_IndPtr* in **SQLBindParameter**. Il buffer di dati viene specificato con l'argomento *DataPtr* in **SQLPutData** e l'argomento *ParameterValuePtr* in **SQLBindParameter**.
