---
title: Funzioni di ora, data e intervallo Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302822"
---
# <a name="time-date-and-interval-functions"></a>Funzioni di data, ora e intervallo
Nella tabella seguente sono elencate le funzioni di data e ora incluse nel set di funzioni scalare ODBC. Un'applicazione può determinare quali funzioni di data e ora sono supportate da un driver chiamando **SQLGetInfo** con un tipo di *informazioni* di SQL_TIMEDATE_FUNCTIONS.  
  
 Gli argomenti indicati come *timestamp_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un escape di *tempo ODBC*, un escape di data *ODBC*o *ODBC-timestamp-escape*, in cui il tipo di dati sottostante potrebbe essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *date_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o un *escape di data ODBC* o *un'escape timestamp ODBC*, in cui il tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *time_exp* possono essere il nome di una colonna, il risultato di un'altra funzione scalare o *un'escape* ora ODBC o *un'escape timestamp ODBC*, in cui il tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 Le funzioni scalari CURRENT_DATE, CURRENT_TIME e CURRENT_TIMESTAMP timedate sono state aggiunte in ODBC 3.0 per allinearsi a SQL-92.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**CURRENT_DATE( )** (ODBC 3.0)|Restituisce la data corrente.|  
|**CURRENT_TIME[(** *precisione temporale* **)** (ODBC 3.0)|Restituisce l'ora locale corrente. L'argomento *time-precision* determina la precisione dei secondi del valore restituito.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp-precision* **)]** (ODBC 3.0)|Restituisce la data locale corrente e l'ora locale come valore timestamp. L'argomento *timestamp-precision* determina la precisione dei secondi del timestamp restituito.|  
|**CURDATE( )** (ODBC 1.0)|Restituisce la data corrente.|  
|**CURTIME( )** (ODBC 1.0)|Restituisce l'ora locale corrente.|  
|**DAYNAME(** *date_exp* **)** (ODBC 2.0)|Restituisce una stringa di caratteri contenente il nome specifico dell'origine dati del giorno, ad esempio da domenica a sabato o domenica. a Sat per un'origine dati che utilizza l'inglese o Sonntag tramite Samstag per un'origine dati che utilizza il tedesco) per la parte relativa al giorno di *date_exp*.|  
|**DAYOFMONTH(** *date_exp* **)** (ODBC 1.0)|Restituisce il giorno del mese in base al campo del mese in *date_exp* come valore intero nell'intervallo 1-31.|  
|**DAYOFWEEK(** *date_exp* **)** (ODBC 1.0)|Restituisce il giorno della settimana in base al campo settimana nella *date_exp* come valore intero nell'intervallo 1-7, dove 1 rappresenta la domenica.|  
|**DAYOFYEAR(** *date_exp* **)** (ODBC 1.0)|Restituisce il giorno dell'anno in base al campo dell'anno in *date_exp* come valore intero compreso tra 1 e 366.|  
|**EXTRACT(** *campo estratto DA* *origine-origine* **)** (ODBC 3.0)|Restituisce la parte del *campo di estrazione* dell'origine di *estrazione.* L'argomento *extract-source* è un'espressione datetime o interval. L'argomento *del campo di estrazione* può essere una delle seguenti parole chiave:<br /><br /> ANNO MESE MESE GIORNO ORA MINUTI SECONDO<br /><br /> La precisione del valore restituito è definita dall'implementazione. La scala è 0 a meno che non venga specificato SECOND, nel qual caso la scala non è inferiore alla precisione dei secondi frazionari del campo *extract-source.*|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|Restituisce l'ora in base al campo dell'ora in *time_exp* come valore intero nell'intervallo compreso tra 0 e 23.|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|Restituisce il minuto in base al campo dei minuti in *time_exp* come valore intero nell'intervallo compreso tra 0 e 59.|  
|**MESE(** *date_exp* **)** (ODBC 1.0)|Restituisce il mese in base al campo del mese *nelldate_exp* come valore intero compreso tra 1 e 12.|  
|**MONTHNAME(** *date_exp* **)** (ODBC 2.0)|Restituisce una stringa di caratteri contenente il nome specifico dell'origine dati del mese (ad esempio, da gennaio a gennaio o da gennaio a dicembre per un'origine dati che utilizza l'inglese o da gennaio a Dezember per un'origine dati che utilizza il tedesco) per la parte del mese di *date_exp*.|  
|**ORA( )** (ODBC 1.0)|Restituisce la data e l'ora correnti come valore timestamp.|  
|**QUARTIle(** *date_exp* **)** (ODBC 1.0)|Restituisce il trimestre *in date_exp* come valore intero compreso tra 1 e 4, dove 1 rappresenta dal 1 gennaio al 31 marzo.|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|Restituisce il secondo in base al secondo campo *di time_exp* come valore intero nell'intervallo compreso tra 0 e 59.|
|**TIMESTAMPADD(** *intervallo*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Restituisce il timestamp calcolato aggiungendo *integer_exp* intervalli di *intervallo* di a *timestamp_exp.* I valori validi di *interval* sono le seguenti parole chiave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> dove i secondi frazionari sono espressi in miliardesimi di secondo. Ad esempio, l'istruzione SQL seguente restituisce il nome di ogni dipendente e la data dell'anniversario di un anno:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* è un valore di tempo e *l'intervallo* specifica giorni, settimane, mesi, trimestri o anni, la parte relativa alla data di *timestamp_exp* viene impostata sulla data corrente prima di calcolare il timestamp risultante.<br /><br /> Se *timestamp_exp* è un valore di data e *intervallo* specifica secondi frazionari, secondi, minuti o ore, la parte relativa all'ora di *timestamp_exp* viene impostata su 0 prima di calcolare il timestamp risultante.<br /><br /> Un'applicazione determina gli intervalli supportati da un'origine dati chiamando **SQLGetInfo** con l'opzione SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF(** *intervallo*, *timestamp_exp1* *, timestamp_exp2* **)** (ODBC 2.0)|Restituisce il numero intero di intervalli di *tipo intervallo* in base al quale *timestamp_exp2* è maggiore di *timestamp_exp1.* I valori validi di *interval* sono le seguenti parole chiave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> dove i secondi frazionari sono espressi in miliardesimi di secondo. Ad esempio, l'istruzione SQL seguente restituisce il nome di ogni dipendente e il numero di anni impiegati:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se una delle due espressioni timestamp è un valore temporale e *intervallo* specifica giorni, settimane, mesi, trimestri o anni, la parte relativa alla data di tale timestamp viene impostata sulla data corrente prima di calcolare la differenza tra i timestamp.<br /><br /> Se una delle due espressioni timestamp è un valore di data e *intervallo* specifica secondi frazionari, secondi, minuti o ore, la parte relativa all'ora di tale timestamp viene impostata su 0 prima di calcolare la differenza tra i timestamp.<br /><br /> Un'applicazione determina gli intervalli supportati da un'origine dati chiamando **SQLGetInfo** con l'opzione SQL_TIMEDATE_DIFF_INTERVALS.|  
|**SETTIMANA(** *date_exp* **)** (ODBC 1.0)|Restituisce la settimana dell'anno in base al campo settimana nella *date_exp* come valore intero compreso tra 1 e 53.|  
|**ANNO(** *date_exp* **)** (ODBC 1.0)|Restituisce l'anno in base al campo dell'anno in *date_exp* come valore intero. L'intervallo dipende dall'origine dati.|
