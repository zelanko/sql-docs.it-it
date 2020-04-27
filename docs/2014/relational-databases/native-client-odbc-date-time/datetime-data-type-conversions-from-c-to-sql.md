---
title: Conversioni da C a SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8179b9452852777bb6d2a06018d0bf86598a5bf8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63207011"
---
# <a name="conversions-from-c-to-sql"></a>Conversioni da tipi di dati C a tipi di dati SQL
  Questo argomento elenca i problemi da considerare quando si esegue la conversione da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi C a tipi di data/ora.  
  
 Le conversioni descritte nella tabella seguente sono valide se effettuate sul client. Nei casi in cui il client specifica la precisione in secondi frazionari per un parametro che differisce da quello definito sul server, la conversione client potrebbe riuscire ma il server restituirà un errore durante la chiamata di `SQLExecute` o `SQLExecuteDirect`. In particolare, ODBC considera errore qualsiasi troncamento dei secondi frazionari, mentre il comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prevede l'arrotondamento, utilizzato, ad esempio, quando si va da `datetime2(6)` a `datetime2(2)`. I valori della colonna di tipo datetime vengono arrotondati a 1/300° di un secondo e le colonne smalldatetime contengono secondi impostati su zero dal server.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1, 5, 7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1, 5, 7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|N/D|N/D|1,10,11|N/D|N/D|N/D|N/D|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/D|N/D|N/D|N/D|1,10,11|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9, 3|9,10|9,7,10|9,5,7,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9, 3, 4|9,4,10|9,10|9,5,10|N/D|N/D|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9, 3, 4, 8|9,4,8,10|9,8,10|9,10|N/D|N/D|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/D|N/D|N/D|N/D|N/D|N/D|N/D|  
  
## <a name="key-to-symbols"></a>Descrizione dei simboli  
  
|Simbolo|Significato|  
|------------|-------------|  
|-|Non viene supportata alcuna conversione. Viene generato un record di diagnostica con SQLSTATE 07006 e il messaggio "Violazione dell'attributo del tipo di dati".|  
|1|Se i dati forniti non sono validi, viene generato un record di diagnostica con SQLSTATE 22007 e il messaggio "Formato di datetime non valido".|  
|2|I campi dell'ora devono essere zero o viene generato un record di diagnostica con SQLSTATE 22008 e il messaggio "Troncamento frazionario".|  
|3|I secondi frazionari devono essere zero o viene generato un record di diagnostica con SQLSTATE 22008 e il messaggio "Troncamento frazionario".|  
|4|Il componente relativo alla data viene ignorato.|  
|5|Il fuso orario viene impostato sul fuso orario del client.|  
|6|L'ora è impostata su zero.|  
|7|La data viene impostata sulla data corrente.|  
|8|L'ora viene convertita dal fuso orario del client all'ora UTC. Se si verifica un errore durante questa conversione, viene generato un record di diagnostica con l'identificativo SQLSTATE 22008 e il messaggio "Overflow del campo Datetime".|  
|9|La stringa viene analizzata e convertita in un valore date, datetime, datetimeoffset o time, in base al primo carattere di punteggiatura rilevato e alla presenza di componenti rimanenti. La stringa viene quindi convertita nel tipo di destinazione, seguendo le regole nella tabella precedente per il tipo di origine individuato da questo processo. Se durante l'analisi dei dati viene rilevato un errore, viene generato un record di diagnostica con SQLSTATE 22018 e il messaggio "Carattere non valido per la specifica del cast". Per i parametri datetime e smalldatetime, se l'anno non è compreso nell'intervallo supportato da questi tipi, viene generato un record di diagnostica con SQLSTATE 22007 e il messaggio "Formato di datetime non valido".<br /><br /> Per datetimeoffset, il valore deve essere compreso nell'intervallo supportato in seguito alla conversione in UTC, anche se non è necessaria alcuna conversione in UTC. Ciò è dovuto al fatto che TDS e il server normalizzano sempre l'ora in valori datetimeoffset per UTC. Il client deve pertanto verificare che i componenti relativi all'ora siano compresi nell'intervallo supportato in seguito alla conversione in UTC. Se il valore non è compreso nell'intervallo UTC supportato, viene generato un record di diagnostica con SQLSTATE 22007 e il messaggio "Formato di datetime non valido".|  
|10|Se si verifica un troncamento con perdita di dati, viene generato un record di diagnostica con SQLSTATE 22008 e il messaggio "Formato ora non valido". Questo errore si verifica anche se il valore non è incluso nell'intervallo che può essere rappresentato dall'intervallo UTC utilizzato dal server.|  
|11|Se la lunghezza in byte dei dati non equivale alla dimensione della struttura richiesta dal tipo SQL, viene generato un record di diagnostica con SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo".|  
|12|Se la lunghezza in byte dei dati è 4 o 8, i dati vengono inviati al server in formato smalldatetime o datetime TDS non elaborato. Se la lunghezza in byte dei dati corrisponde esattamente alla dimensione di SQL_TIMESTAMP_STRUCT, i dati vengono convertiti nel formato TDS per datetime2.|  
|13|Se si verifica un troncamento con perdita di dati, viene generato un record di diagnostica con SQLSTATE 22001 e il messaggio "Troncamento a destra della stringa di dati".<br /><br /> Il numero di cifre per i secondi frazionari (scala) è determinato dalla dimensione della colonna di destinazione in base a quanto segue:<br /><br /> **Tipo:** SQL_C_TYPE_TIMESTAMP<br /><br /> Scala implicita<br /><br /> 0<br /><br /> 19<br /><br /> Scala implicita<br /><br /> 1.. 9<br /><br /> 21..29<br /><br /> Per SQL_C_TYPE_TIMESTAMP, tuttavia, se i secondi frazionari possono essere rappresentati con tre cifre senza perdita di dati e la dimensione della colonna è almeno 23, vengono generate esattamente tre cifre di secondi frazionari. Questo comportamento assicura la compatibilità con le versioni precedenti per le applicazioni sviluppate utilizzando driver ODBC meno recenti.<br /><br /> Per dimensioni di colonna maggiori dell'intervallo specificato nella tabella, si presuppone una scala 9. Questa conversione deve consentire fino a nove cifre per i secondi frazionari, il massimo consentito da ODBC.<br /><br /> Una dimensione della colonna pari a zero implica una dimensione illimitata per i tipi di carattere a lunghezza variabile in ODBC (9 cifre, a meno che non si applichi la regola delle 3 cifre per SQL_C_TYPE_TIMESTAMP). La specifica di una dimensione della colonna pari a zero con un tipo di carattere a lunghezza fissa è un errore.|  
|N/D|Viene mantenuto il comportamento di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni precedenti.|  
  
## <a name="see-also"></a>Vedi anche  
 [Miglioramenti di data e ora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
