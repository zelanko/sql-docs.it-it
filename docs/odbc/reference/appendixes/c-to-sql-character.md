---
title: 'Da C a SQL: Carattere Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292032"
---
# <a name="c-to-sql-character"></a>Da C a SQL: carattere
Gli identificatori per il tipo di dati C ODBC carattere sono:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 Nella tabella seguente vengono illustrati i tipi di dati SQL ODBC in cui è possibile convertire i dati di tipo carattere C. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da C a tipi](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)di dati SQL .  
  
> [!NOTE]  
>  Quando i dati di tipo carattere C vengono convertiti in dati SQL Unicode, la lunghezza dei dati Unicode deve essere un numero pari.  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte dei dati <- Lunghezza colonna.<br /><br /> Lunghezza in byte dei dati > Lunghezza colonna.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza di carattere dei dati <- Lunghezza colonna.<br /><br /> Lunghezza di caratteri dei dati > Lunghezza colonna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Dati convertiti senza troncamento<br /><br /> Dati convertiti con troncamento delle cifre frazionarie[e]<br /><br /> La conversione dei dati comporterebbe la perdita di cifre intere (anziché frazionarie)[e]<br /><br /> Il valore dei dati non è un *valore numerico*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|I dati rientrano nell'intervallo del tipo di dati in cui viene convertito il numero<br /><br /> I dati non rientrano nell'intervallo del tipo di dati in cui viene convertito il numero<br /><br /> Il valore dei dati non è un *valore numerico*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, minori di 2 e non uguali a 1<br /><br /> I dati sono minori di 0 o maggiori o uguali a 2<br /><br /> I dati non sono valori *numerici*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Lunghezza in byte dei dati) / 2 <- lunghezza byte colonna<br /><br /> (Lunghezza byte di dati) / 2 > lunghezza byte colonna<br /><br /> Il valore dei dati non è un valore esadecimale|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Il valore dei dati è un *valore letterale* di data ODBC valido<br /><br /> Il valore dei dati è un *valore letterale ODBC-timestamp valido*; parte ora è zero<br /><br /> Il valore dei dati è un *valore letterale ODBC-timestamp valido*; time portion è diverso da zero[a]<br /><br /> Valore di dati non è un *valore letterale di data ODBC* valido o *ODBC-timestamp-letterale*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Il valore dei dati è un *valore letterale di tempo ODBC* valido<br /><br /> Il valore dei dati è un *valore letterale ODBC-timestamp valido*; la parte dei secondi frazionari è zero[b]<br /><br /> Il valore dei dati è un *valore letterale ODBC-timestamp valido*; la parte dei secondi frazionari è diversa da zero[b]<br /><br /> Valore di dati non è un *valore letterale di ora ODBC* valido o *ODBC-timestamp-valore letterale*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Il valore dei dati è un *valore letterale ODBC-timestamp valido*; parte dei secondi frazionari non troncata<br /><br /> Il valore dei dati è un *valore letterale ODBC-timestamp valido*; parte frazionaria dei secondi troncata<br /><br /> Il valore di dati è un *valore letterale di data ODBC*valido [c]<br /><br /> Il valore dei dati è un *valore letterale di ora ODBC*valido [d]<br /><br /> Il valore dei dati non è un *valore letterale di data ODBC*valido , *ODBC-time-literal*o *ODBC-timestamp-literal*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Tutti i tipi di intervallo SQLAll SQL interval types|Il valore dei dati è un valore di *intervallo*valido; non si verifica alcun troncamento<br /><br /> Il valore dei dati è un valore di *intervallo*valido; il valore in uno dei campi viene troncato<br /><br /> Il valore dei dati non è un valore letterale di intervallo validoThe data value is not a valid interval literal|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] La parte relativa all'ora del timestamp viene troncata.  
  
 [b] La parte relativa alla data del timestamp viene ignorata.  
  
 [c] La parte relativa all'ora del timestamp è impostata su zero.  
  
 [d] La parte relativa alla data del timestamp è impostata sulla data corrente.  
  
 [e] Il driver/origine dati attende in modo efficace fino a quando non viene ricevuta l'intera stringa (anche se i dati di tipo carattere vengono inviati in pezzi da chiamate a **SQLPutData**) prima di tentare di eseguire la conversione.  
  
 Quando i dati di tipo carattere C vengono convertiti in dati SQL numerici, di data, ora o timestamp, gli spazi vuoti iniziali e finali vengono ignorati.  
  
 Quando i dati di tipo carattere C vengono convertiti in dati SQL binari, ogni due byte di dati di tipo carattere vengono convertiti in un singolo byte (8 bit) di dati binari. Ogni due byte di dati di tipo carattere rappresentano un numero in formato esadecimale. Ad esempio, "01" viene convertito in un file binario 00000001 e "FF" in un file binario 11111111.  
  
 Il driver converte sempre coppie di cifre esadecimali in singoli byte e ignora il byte di terminazione null. Per questo motivo, se la lunghezza della stringa di caratteri è dispari, l'ultimo byte della stringa (escluso il byte di terminazione null, se presente) non viene convertito.  
  
> [!NOTE]  
>  Gli sviluppatori di applicazioni sono sconsigliati dall'associazione di dati di tipo carattere C a un tipo di dati SQL binario. Questa conversione è solitamente inefficiente e lenta.
