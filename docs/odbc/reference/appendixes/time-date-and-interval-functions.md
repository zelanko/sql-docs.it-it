---
title: Funzioni di intervallo, ora e data | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509267"
---
# <a name="time-date-and-interval-functions"></a>Funzioni di data, ora e intervallo
Nella tabella seguente elenca le funzioni di data e ora sono inclusi nel set di funzioni scalari ODBC. Un'applicazione può determinare quali funzioni di data e ora sono supportate da un driver chiamando **SQLGetInfo** con un *tipo di informazioni* di SQL_TIMEDATE_FUNCTIONS.  
  
 Gli argomenti indicati come *timestamp_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare, o un' *ODBC-tempo-escape*, *ODBC-Data-escape*, oppure *ODBC-timestamp-escape*, in cui il tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *date_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare, o un' *ODBC-Data-escape* o *ODBC-timestamp-escape*, dove la tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Gli argomenti indicati come *time_exp* può essere il nome di una colonna, il risultato di un'altra funzione scalare, o un' *ODBC-tempo-escape* o *ODBC-timestamp-escape*, dove la tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.  
  
 La funzione CURRENT_DATE CURRENT_TIME e CURRENT_TIMESTAMP timedate funzioni scalari sono stati aggiunti nella versione 3.0 di ODBC per la compatibilità con SQL-92.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**FUNZIONE CURRENT_DATE ()** (ODBC 3.0)|Restituisce la data corrente.|  
|**CURRENT_TIME [(** *precisione temporale* **)]** (ODBC 3.0)|Restituisce l'ora locale corrente. Il *precisione temporale* argomento determina la precisione dei secondi del valore restituito.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp con precisione* **)]** (ODBC 3.0)|Restituisce la data locale corrente e l'ora locale come un valore di timestamp. Il *timestamp precisione* argomento determina la precisione dei secondi del timestamp restituito.|  
|**CURDATE ()** (ODBC 1.0)|Restituisce la data corrente.|  
|**FUNZIONE CURTIME ()** (ODBC 1.0)|Restituisce l'ora locale corrente.|  
|**Funzione DAYNAME (** *date_exp* **)** (ODBC 2.0)|Restituisce una stringa di caratteri contenente il nome di specifiche dell'origine dati del giorno (ad esempio, Sunday a Saturday o da Sun. a Sat per un'origine dati che utilizza l'inglese o da lunedì a domenica per un'origine dati che utilizza l'italiano) per la parte del giorno *date_exp*.|  
|**DAYOFMONTH (** *date_exp* **)** (1.0 ODBC)|Restituisce il giorno del mese in base al campo mese nel *date_exp* come valore intero compreso tra 1 e 31.|  
|**DAYOFWEEK (** *date_exp* **)** (1.0 ODBC)|Restituisce il giorno della settimana in base al campo della settimana in *date_exp* come valore intero compreso nell'intervallo da 1 a 7, dove 1 corrisponde a domenica.|  
|**DAYOFYEAR (** *date_exp* **)** (1.0 ODBC)|Restituisce il giorno dell'anno di base il campo year *date_exp* come valore intero compreso tra 1 e 366.|  
|**ESTRARRE (** *Estrai campo FROM* *extract source* **)** (ODBC 3.0)|Restituisce il *Estrai campo* parte del *Estrai source*. Il *extract source* argomento è un'espressione datetime o intervallo. Il *Estrai campo* argomento può essere una delle parole chiave seguenti:<br /><br /> ANNO MESE GIORNO ORA MINUTO, SECONDO<br /><br /> La precisione del valore restituito è definito dall'implementazione. La scala è 0 se non viene specificato in secondo luogo, nel qual caso la scala specificata non è minore di precisione dei secondi frazionari di *extract source* campo.|  
|**ORA (** *time_exp* **)** (1.0 ODBC)|Restituisce l'ora in base al campo dell'ora nelle *time_exp* come valore intero nell'intervallo compreso tra 0 e 23.|  
|**MINUTI (** *time_exp* **)** (1.0 ODBC)|Vengono restituiti i minuti in base al campo al minuto nelle *time_exp* come valore intero nell'intervallo compreso tra 0 e 59.|  
|**MESE (** *date_exp* **)** (1.0 ODBC)|Restituisce il mese in base al campo mese nel *date_exp* come valore intero nell'intervallo di 1 a 12.|  
|**NOMEMESE (** *date_exp* **)** (ODBC 2.0)|Restituisce una stringa di caratteri contenente il nome del mese (ad esempio, da gennaio a dicembre o December a DEC per un'origine dati che utilizza l'inglese o da gennaio a dicembre per un'origine dati che utilizza l'italiano) specifiche dell'origine dati per la parte del mese *date_exp*.|  
|**A QUESTO PUNTO (.)** (ODBC 1.0)|Restituisce una data e ora come valore timestamp corrente.|  
|**TRIMESTRE (** *date_exp* **)** (1.0 ODBC)|Restituisce il trimestre *date_exp* come valore intero compreso nell'intervallo da 1 a 4, dove 1 rappresenta il 1 ° gennaio al 31 marzo.|  
|**SECONDO (** *time_exp* **)** (1.0 ODBC)|Restituisce i secondi in base al campo nelle *time_exp* come valore intero nell'intervallo compreso tra 0 e 59.|
|**Timestampadd non (** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Restituisce il timestamp calcolato sommando *integer_exp* intervalli typu *intervallo* al *timestamp_exp*. I valori validi del *intervallo* sono parole chiave seguenti:<br /><br /> ARGOMENTI<br /><br /> SEGUENTI<br /><br /> : SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> in cui i secondi frazionari sono espressi in miliardesimi di secondo. Ad esempio, l'istruzione SQL seguente restituisce il nome di ogni dipendente e la propria data di ricorrenza annuale:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Se *timestamp_exp* è un valore di ora e *intervallo* specifica giorni, settimane, mesi, trimestri o anni, la parte relativa alla data del *timestamp_exp* è impostato sulla data corrente prima di calcolo del timestamp risulta.<br /><br /> Se *timestamp_exp* è un valore di data e *intervallo* specifica frazionari secondi, secondi, minuti o ore, la porzione dell'ora *timestamp_exp* è impostato su 0 prima calcolo del timestamp risulta.<br /><br /> Un'applicazione determina quali intervalli di un'origine dati supporta chiamando **SQLGetInfo** con l'opzione SQL_TIMEDATE_ADD_INTERVALS.|  
|**Timestampdiff non (** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Restituisce il numero intero di intervalli di tipo *interval* mediante il quale *timestamp_exp2* è maggiore di quella *timestamp_exp1*. I valori validi del *intervallo* sono parole chiave seguenti:<br /><br /> ARGOMENTI<br /><br /> SEGUENTI<br /><br /> : SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> in cui i secondi frazionari sono espressi in miliardesimi di secondo. Ad esempio, l'istruzione SQL seguente restituisce il nome di ogni dipendente e il numero di anni che è stata impiegata direste:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Se due espressioni di timestamp è un valore di ora e *intervallo* specifica giorni, settimane, mesi, trimestri o anni, la parte relativa alla data di tale timestamp è impostato sulla data corrente prima di calcolare la differenza tra i timestamp.<br /><br /> Se due espressioni di timestamp è un valore di data e *intervallo* specifica frazionari secondi, secondi, minuti o ore, la parte relativa all'ora di tale timestamp è impostato su 0 prima di calcolare la differenza tra i timestamp.<br /><br /> Un'applicazione determina quali intervalli di un'origine dati supporta chiamando **SQLGetInfo** con l'opzione SQL_TIMEDATE_DIFF_INTERVALS.|  
|**SETTIMANA (** *date_exp* **)** (1.0 ODBC)|Restituisce la settimana dell'anno in base al campo della settimana in *date_exp* come valore intero compreso nell'intervallo da 1 a 53.|  
|**ANNO (** *date_exp* **)** (1.0 ODBC)|Restituisce l'anno in base al campo year nella *date_exp* come valore intero. L'intervallo è dipendente dall'origine dati.|
