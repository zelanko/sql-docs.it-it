---
title: Le conversioni da SQL a C | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd19cb92f2d2f333954adeb97229feb718c4b592
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399554"
---
# <a name="conversions-from-sql-to-c"></a>Conversioni dai tipi di dati SQL ai tipi di dati C
  Nella tabella seguente sono elencati i problemi da prendere in considerazione durante le conversioni dai tipi date/time di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai tipi C.  
  
## <a name="conversions"></a>Conversioni  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_TYPE_DATE|OK|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|OK|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|OK|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|OK|21|16|16|  
  
## <a name="key-to-symbols"></a>Descrizione dei simboli  
  
|Simbolo|Significato|  
|------------|-------------|  
|OK|Nessun problema di conversione.|  
|1|Si applicano le regole precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|2|Gli spazi iniziali e finali vengono ignorati.|  
|3|Il valore stringa viene analizzato in un tipo date, time, timezone o timezoneoffset e consente un massimo di 9 cifre per i secondi frazionari. Se viene analizzato un tipo di dati timezoneoffset, il tipo time viene convertito al tipo timezone del client. Se si verifica un errore durante questa conversione, viene generato un record di diagnostica con SQLSTATE 22018 e il messaggio "Overflow del campo Datetime".|  
|4|Se il valore non è di un tipo date, timestamp o timestampoffset valido, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22018 e il messaggio "Carattere non valido per la specifica del cast".|  
|5|Se il valore time è diverso da zero, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 01S07 e il messaggio "Troncamento frazionario".|  
|6|Se il valore non è un tipo time, timestamp o timestampoffset valido, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22018 e il messaggio "Carattere non valido per la specifica del cast".|  
|7|Il componente relativo alla data viene ignorato.|  
|8|Se i secondi frazionari sono diversi da zero, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 01S07 e il messaggio "Troncamento frazionario".|  
|9|Se il valore non è un tipo date, time, timestamp o timestampoffset valido, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22018 e il messaggio "Carattere non valido per la specifica del cast".|  
|10|Se il valore è un tipo time valido, il componente date viene impostato sul valore date del client corrente.|  
|11|Se il valore è un tipo date valido, il componente time viene impostato su zero.|  
|12|Viene generato un record di diagnostica con SQLSTATE 07006 e il messaggio "Violazione dell'attributo del tipo di dati".|  
|13|L'ora è impostata su zero.|  
|14|Se il buffer non è grande abbastanza da contenere un valore SQL_DATE_STRUCT, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo".|  
|15|Il valore date viene impostato sul valore date del client corrente.|  
|16|Se il buffer non è grande abbastanza da contenere il valore stringa convertito, ma solo i secondi frazionari, si verifica il troncamento, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 01004 e il messaggio "Troncamento a destra della stringa di dati". Se il buffer non presenta dimensioni sufficienti a contenere il valore stringa senza troncamento dei componenti date, time o offset, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo". Si noti che per i tipi date e timestampoffset, non è possibile che si verifichi l'errore con identificativo SQLSTATE 01004 perché la parte all'estrema destra della stringa convertita non contiene secondi frazionari. Un eventuale troncamento determinerà pertanto una perdita dei dati.|  
|17|Se il buffer non presenta dimensioni sufficienti a contenere un valore SQL_SS_TIME2_STRUCT, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo".|  
|18|Se il valore time è diverso da zero, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 01S07 e il messaggio "Troncamento frazionario".|  
|19|Se il tipo di dati del server è datetime o smalldatetime, il valore corrisponde al formato wire TDS sotto forma di valore a 4 byte per smalldatetime e a 8 byte per datetime.<br /><br /> Se il tipo di dati del server è datetime2, il valore viene restituito come SQL_TIMESTAMP_STRUCT. Se il buffer non è di dimensioni sufficienti a contenere il valore restituito, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo".|  
|20|Viene effettuata la conversione dell'ora nel fuso orario del client. Se si verifica un errore durante questa conversione, viene generato un record di diagnostica con l'identificativo SQLSTATE 22008 e il messaggio "Overflow del campo Datetime".|  
|21|Se il buffer è grande abbastanza da contenere un valore SQL_SS_TIMESTAMPOFFSET_STRUCT, il valore viene restituito come tale. In caso contrario, viene generato un record di diagnostica con l'identificativo di errore SQLSTATE 22003 e il messaggio "Valore numerico non compreso nell'intervallo".|  
|22|Il valore viene convertito al tipo timezone del client prima che il tipo date venga estratto. Ciò garantisce coerenza con le altre conversioni con tipi di dati timestampoffset. Se si verifica un errore durante questa conversione, viene generato un record di diagnostica con l'identificativo SQLSTATE 22008 e il messaggio "Overflow del campo Datetime". Ciò potrebbe avere come conseguenza un valore date diverso da quello ottenuto dal semplice troncamento.|  
  
 Nella tabella riportata in questo argomento sono descritte le conversioni tra il tipo restituito al client e il tipo presente nell'associazione. Per i parametri di output, se il tipo di server specificato in SQLBindParameter non corrisponde al tipo effettivo nel server, verrà eseguita una conversione implicita dal server e il tipo restituito al client corrisponderà al tipo specificato tramite la funzione SQLBindParameter. Questo può causare risultati di conversione imprevisti quando le regole di conversione del server sono diverse da quelli elencati nella tabella precedente. Quando è ad esempio necessario specificare un valore date predefinito, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza 1900-1-1, anziché il valore date corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Data e miglioramenti per la fase &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
