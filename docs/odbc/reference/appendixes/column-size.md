---
title: Proprietà Column Size (Dimensioni colonne) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306582"
---
# <a name="column-size"></a>Dimensioni della colonna
La dimensione della colonna (o del parametro) dei tipi di dati numerici è definita come il numero massimo di cifre utilizzate dal tipo di dati della colonna o del parametro o la precisione dei dati. Per i tipi di carattere, questa è la lunghezza in caratteri dei dati; per i tipi di dati binari, la dimensione della colonna è definita come la lunghezza in byte dei dati. Per i tipi di dati time, timestamp e tutti i tipi di dati interval, questo è il numero di caratteri nella rappresentazione di caratteri di questi dati. Nella tabella seguente viene illustrata la dimensione della colonna definita per ogni tipo di dati SQL conciso.  
  
|Identificatore di tipo SQL|Dimensioni colonna|  
|-------------------------|-----------------|  
|Tutti i tipi di carattere[a],[b]|Dimensione della colonna definita o massima in caratteri della colonna o del parametro (come contenuto nel campo descrittore SQL_DESC_LENGTH). Ad esempio, la dimensione della colonna di una colonna di caratteri a byte singolo definita come CHAR(10) è 10.|  
|SQL_DECIMAL SQL_NUMERIC|Numero definito di cifre. Ad esempio, la precisione di una colonna definita come NUMERIC(10,3) è 10.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (se firmato) o 20 (se senza segno)|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|Tutti i tipi binari[a],[b]|Lunghezza definita o massima in byte della colonna o del parametro. Ad esempio, la lunghezza di una colonna definita come BINARIO(10) è 10.|  
|SQL_TYPE_DATE[c]|10 (il numero di caratteri nel formato *aaaa-mm-gg).*|  
|SQL_TYPE_TIME[c]|8 (il numero di caratteri nel formato *hh-mm-ss)* o 9 *s* (il numero di caratteri nel formato *hh:mm:ss*[.fff...], dove *s* è la precisione dei secondi).|  
|SQL_TYPE_TIMESTAMP|16 (il numero di caratteri nel formato *aaaa-mm-gg hh:mm)*<br /><br /> 19 (il numero di caratteri nel formato *aaaa-mm-gg* *hh:mm:ss)*<br /><br /> o<br /><br /> 20 *s* (il numero di caratteri nel formato *aaaa-mm-gg hh:mm:ss*[.fff...], dove *s* è la precisione dei secondi).|  
|SQL_INTERVAL_SECOND|Dove *p* è la precisione di interlinea intervallo e *s* è la precisione dei secondi, *p* (se *s*s s s) o *p*+*s*s 1 (se *s*>0). [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Where *p* is the interval leading precision and *s* is the seconds precision, 9+*p* (if *s*=0) or 10+*p*+*s* (if *s*>0). [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Where *p* is the interval leading precision and *s* is the seconds precision, 6+*p* (if *s*=0) or 7+*p*+*s* (if *s*>0). [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Where *p* is the interval leading precision and *s* is the seconds precision, 3+*p* (if *s*=0) or 4+*p*+*s* (if *s*>0). [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, dove *p* è la precisione di interlinea dell'intervallo. [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|,*p*dove *p* è la precisione di interlinea dell'intervallo. [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|,*p*dove *p* è la precisione di interlinea dell'intervallo. [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|,*p*dove *p* è la precisione di interlinea dell'intervallo. [d]|  
|SQL_GUID|36 (il numero di caratteri nel formato *aaaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeeeee)*|  
  
 [a] Per un'applicazione ODBC 1.0 che chiama **SQLSetParam** in un driver ODBC 2.0 e per un'applicazione \*ODBC 2.0 che chiama **SQLBindParameter** in un driver ODBC 1.0, quando *StrLen_or_IndPtr* è SQL_DATA_AT_EXEC per un tipo di SQL_LONGVARCHAR o SQL_LONGVARBINARY, *ColumnSize* deve essere impostato sulla lunghezza totale dei dati da inviare, non sulla precisione definita in questa tabella.  
  
 [b] Se il driver non è in grado di determinare la lunghezza della colonna o del parametro per un tipo di variabile, restituisce SQL_NO_TOTAL.  
  
 [c] *L'argomento ColumnSize* di **SQLBindParameter** viene ignorato per questo tipo di dati.  
  
 [d] Per le regole generali sulla lunghezza delle colonne nei tipi di dati intervallo, vedere [Interval Data Type Length](../../../odbc/reference/appendixes/interval-data-type-length.md), più indietro in questa appendice.  
  
 I valori restituiti per la dimensione della colonna (o del parametro) non corrispondono ai valori in un campo descrittore. I valori possono provenire dal campo SQL_DESC_PRECISION o SQL_DESC_LENGTH, a seconda del tipo di dati, come illustrato nella tabella seguente.  
  
|Tipo SQL|Campo descrittore corrispondente a<br /><br /> dimensione di colonna o parametro|  
|--------------|--------------------------------------------------------------------|  
|Tutti i tipi di caratteri e binari|LENGTH|  
|Tutti i tipi numerici|PRECISION|  
|Tutti i tipi di datetime e intervallo|LENGTH|  
|SQL_BIT|LENGTH|
