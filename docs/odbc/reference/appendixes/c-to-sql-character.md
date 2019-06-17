---
title: 'Da C a SQL: Carattere | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0158da62ed360e926cdb5382b89b1491c0723550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201631"
---
# <a name="c-to-sql-character"></a>Da C a SQL: Carattere
Gli identificatori per il carattere di tipo di dati ODBC C sono:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 La tabella seguente illustra il codice SQL ODBC dei tipi di dati a cui possono essere convertiti i dati di tipo carattere C. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Quando i dati di caratteri C viene convertiti in dati Unicode SQL, la lunghezza dei dati Unicode deve essere un numero pari.  
  
|Identificatore di tipo SQL|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Lunghezza in byte dei dati < = lunghezza della colonna.<br /><br /> Lunghezza in byte di dati > lunghezza della colonna.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Lunghezza dei dati in caratteri < = lunghezza della colonna.<br /><br /> Lunghezza dei dati in caratteri > lunghezza della colonna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Dati convertiti senza troncamenti<br /><br /> I dati convertiti con troncamento delle cifre frazionarie [e]<br /><br /> Conversione dei dati comporta la perdita di cifre intero (in contrapposizione frazionari) [e]<br /><br /> Valore dati non è un *letterali numerici*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Data è compreso nell'intervallo del tipo di dati a cui il numero viene convertito<br /><br /> I dati non rientra nell'intervallo del tipo di dati a cui il numero viene convertito<br /><br /> Valore dati non è un *letterali numerici*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|I dati sono 0 o 1<br /><br /> I dati sono maggiori di 0, inferiore a 2 e non è uguale a 1<br /><br /> I dati sono minore di 0 oppure maggiore o uguale a 2<br /><br /> I dati non sono un *letterali numerici*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Lunghezza in byte dei dati) / 2 < = lunghezza di colonna in byte<br /><br /> (Lunghezza in byte dei dati) / 2 > lunghezza di colonna in byte<br /><br /> Valore di dati non è un valore esadecimale|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Valore dei dati è un valido *valore letterale di data ODBC*<br /><br /> Valore dei dati è un valido *ODBC-timestamp-literal*; la parte dell'ora è uguale a zero<br /><br /> Valore dei dati è un valido *ODBC-timestamp-literal*; la parte dell'ora è diverso da zero [a]<br /><br /> Valore di dati non valido *ODBC-Data-literal* o *ODBC-timestamp-literal*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Valore dei dati è un valido *valore letterale di ora ODBC*<br /><br /> Valore dei dati è un valido *ODBC-timestamp-literal*; frazionari parte relativa ai secondi è pari a zero [b]<br /><br /> Valore dei dati è un valido *ODBC-timestamp-literal*; frazionari parte relativa ai secondi sia diverso da zero [b]<br /><br /> Valore di dati non valido *ODBC-tempo-literal* o *ODBC-timestamp-literal*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Valore dei dati è un valido *ODBC-timestamp-literal*; frazionari parte relativa ai secondi non troncato<br /><br /> Valore dei dati è un valido *ODBC-timestamp-literal*; frazionaria troncata parte relativa ai secondi<br /><br /> Valore dei dati è un valido *valore letterale di data ODBC*[c]<br /><br /> Valore dei dati è un valido *valore letterale di ora ODBC*[d]<br /><br /> Valore di dati non valido *ODBC-Data-literal*, *valore letterale di ora ODBC*, o *ODBC-timestamp-literal*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Tutti i tipi di intervallo SQL|Valore dei dati è un valido *valore dell'intervallo*; nessun troncamento si verifica<br /><br /> Valore dei dati è un valido *valore dell'intervallo*; viene troncato il valore in uno dei campi<br /><br /> Il valore dei dati non è un intervallo valido di valore letterale|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] parte relativa all'ora del timestamp viene troncato.  
  
 [b] la parte relativa alla data del timestamp viene ignorato.  
  
 [c] la parte relativa all'ora del timestamp è impostato su zero.  
  
 [d] la parte relativa alla data del timestamp è impostato sulla data corrente.  
  
 [e] l'origine dati/driver attende in modo efficace fino a quando non è stata ricevuta l'intera stringa (anche se i dati di carattere vengono inviati in parti dalle chiamate a **SQLPutData**) prima di provare a eseguire la conversione.  
  
 Quando i dati di tipo carattere C viene convertito in numerico, data, ora o timestamp dei dati SQL, iniziali e gli spazi vuoti finali vengono ignorati.  
  
 Quando i dati di caratteri C viene convertiti in dati binari SQL, ogni due byte di dati di tipo carattere vengono convertiti in un singolo byte (8 bit) di dati binari. Ogni due byte di dati di tipo carattere rappresenta un numero in formato esadecimale. Ad esempio, "01" viene convertito in un binario 00000001 e "FF" viene convertito in un binario 11111111.  
  
 Il driver sempre converte le coppie di cifre esadecimali a byte singoli e ignora il byte di terminazione null. Per questo motivo, se la lunghezza della stringa di caratteri è dispari, l'ultimo byte della stringa (escluso il byte di terminazione null, se presente) non viene convertito.  
  
> [!NOTE]  
>  Gli sviluppatori di applicazioni sono sconsigliati dall'associazione di dati carattere C a un tipo di dati binario di SQL. Questa conversione è in genere lenti e poco efficiente.
