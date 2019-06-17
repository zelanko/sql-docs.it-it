---
title: Tipo di dati Dwloader le regole di conversione - Parallel Data Warehouse | Microsoft Docs
description: In questo argomento descrive i formati di dati di input e conversioni di tipi di dati implicite che dwloader che caricatore della riga di comando supporta al momento del caricamento dei dati in Parallel Data Warehouse (PDW)."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 46d092ee5d3b981c60d7bd5bde49f9994dab4b08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042572"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Tipo di dati per dwloader - Parallel Data Warehouse, le regole di conversione
In questo argomento descrive i formati di dati di input e conversioni di tipi di dati implicite che [caricatore della riga di comando dwloader](dwloader.md) supporta al momento del caricamento dei dati in PDW. Le conversioni implicite dei dati si verificano quando i dati di input non corrisponde al tipo di dati nella tabella di destinazione di SQL Server PDW. Usare queste informazioni quando si progetta il processo di caricamento per verificare che i dati sarà caricati correttamente in SQL Server PDW.  
   
  
## <a name="InsertBinaryTypes"></a>Inserimento di valori letterali in tipi binari  
Nella tabella seguente definisce i tipi letterali accettati, formato e le regole di conversione per il caricamento di un valore letterale in una colonna di SQL Server PDW typu **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in binary o varbinary tipo di dati|  
|-------------------|-----------------------|-----------------------------------------------|  
|Valore letterale binario|[0x]*hexidecimal_string*<br /><br />Esempio: 12Ef o 0x12Ef|Il prefisso 0x è facoltativo.<br /><br />La lunghezza di origine dei dati non può superare il numero di byte specificati per il tipo di dati.<br /><br />Se la lunghezza di origine dati è inferiore alle dimensioni dei **binario** tipo di dati, i dati vengano applicato un riempimento a destra con zeri per raggiungere le dimensioni di tipo di dati.|  
  
## <a name="InsertDateTimeTypes"></a>Inserimento di valori letterali in tipi data e ora  
Valori letterali di data e ora vengono rappresentati tramite valori letterali stringa in formati specifici, racchiusi tra virgolette singole. Nelle tabelle seguenti definiscono i tipi letterali consentiti, formato e le regole di conversione per il caricamento di una data o ora letterale in una colonna di tipo **data/ora**, **smalldatetime**, **data**, **tempo**, **datetimeoffset**, o **datetime2**. Le tabelle di definiscono il formato predefinito per il tipo di dati specificato. Altri formati che è possibile specificare sono definiti nella sezione [formati Datetime](#DateFormats). Valori letterali di data e ora non possono includere spazi iniziali o finali. **Data**, **smalldatetime**, e i valori null non possono essere caricati in modalità di larghezza fissa.  
  
### <a name="datetime-data-type"></a>Tipi di dati datetime  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **datetime**. Una stringa vuota (") viene convertita il valore predefinito ' 12:00:00.000 1900-01-01'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati datetime|  
|-------------------|-----------------------|------------------------------------|  
|Valore letterale stringa nel **datetime** formato|'aaaa-MM-gg hh.mm.ss [. fff]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|Cifre frazionarie mancante vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35 ' viene inserito come ' 2007-05-08 12:35:00.000'.|  
|Valore letterale stringa nel **smalldatetime** formato|'aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12:35'|Cifra frazionaria rimanente e secondi viene impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'aaaa-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) sono impostati 12:00:00.000 quando viene inserito il valore.|  
|Valore letterale stringa nel **datetime2** formato|'aaaa-MM-GG: 'ss. fffffff<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|I dati di origine non possono superare tre cifre frazionarie. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' verrà inserito, tranne il valore ' 12:35:29.1234567 2007-05-8' viene generato un errore.|  
  
### <a name="smalldatetime-data-type"></a>Tipo di dati smalldatetime  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **smalldatetime**. Una stringa vuota (") viene convertita il valore predefinito ' 1900-01-01 GMT+12.00 '. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Valore letterale stringa nel **smalldatetime** formato|'aaaa-MM-gg hh: mm' o 'aaaa-MM-gg hh.mm.ss'<br /><br />Esempio: ' 2007-05-08 GMT+12.00 ' o ' 2007-05-08 12:00:15 '|I dati di origine devono avere i valori per anno, mese, data, ora e minuto. Secondi sono facoltativi e, se presente, devono essere impostati su 00 il valore. Qualsiasi altro valore genera un errore.<br /><br />I secondi sono facoltativi. Quando si caricano in una colonna di tipo smalldatetime, dwloader verranno arrotondate per eccesso secondi e frazioni di secondo. Ad esempio, si caricherà 1999 01 05 20:10:35.123 come 01 05 20:11.|  
|Valore letterale stringa nel **data** formato|'aaaa-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore.|  
  
### <a name="date-data-type"></a>Tipo di dati date  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **data**. Una stringa vuota (") viene convertita il valore predefinito ' 1900-01-01'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione a tipo di dati date|  
|-------------------|-----------------------|--------------------------------|  
|Valore letterale stringa nel **data** formato|'aaaa-MM-GG'<br /><br />Esempio: '2007-05-08'||  
  
### <a name="time-data-type"></a>Tipo di dati temporali  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **ora**. Una stringa vuota (") viene convertita il valore predefinito '00:00:00.0000'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati ora|  
|-------------------|-----------------------|--------------------------------|  
|Valore letterale stringa nel **ora** formato|'hh:mm:ss.fffffff'<br /><br />Esempio: '12:35:29.1234567'|Se l'origine dati ha una precisione minore o uguale (numero di cifre frazionarie) quella del **ora** tipo di dati, i dati vengano applicato un riempimento a destra con zeri. Ad esempio, viene inserito un valore letterale '12:35:29.123' come '12:35:29.1230000'.|  
  
### <a name="datetimeoffset-data-type"></a>Tipo di dati DateTimeOffset  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **datetimeoffset** (*n*). Il formato predefinito è ' aaaa-MM-GG: ss. fffffff {+ |-} hh: mm '. Una stringa vuota (") viene convertita il valore predefinito ' 12:00:00.0000000 1900-01-01 + 00:00 '. Le stringhe che contengono solo spazi vuoti (' ') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Ad esempio, una colonna definita come **datetimeoffset** (2) avranno due cifre frazionarie.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati datetimeoffset|  
|-------------------|-----------------------|------------------------------------------|  
|Valore letterale stringa nel **datetime** formato|'aaaa-MM-gg hh.mm.ss [. fff]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|Cifre frazionarie mancante e valori di offset sono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' viene inserito come ' 12:35:29.1230000 2007-05-08 + 00:00 '.|  
|Valore letterale stringa nel **smalldatetime** formato|'aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12:35'|Valori di offset, cifra frazionaria rimanente e secondi vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'aaaa-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08' viene inserito come ' 00.00.00.0000000 2007-05-08 + 00:00 '.|  
|Valore letterale stringa nel **datetime2** formato|'aaaa-MM-GG: 'ss. fffffff<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|I dati di origine non possono superare il numero specificato di secondi frazionari nella colonna datetimeoffset. Se l'origine dati contiene un numero minore o uguale di frazioni di secondo, i dati vengono anteposti a destra con zeri. Ad esempio, se il tipo di dati datetimeoffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15 ' viene inserito come ' 12:35:29.12300 + 12:15 '.|  
|Valore letterale stringa nel **datetimeoffset** formato|' aaaa-MM-GG: ss. fffffff {+&#124;-} hh: mm '<br /><br />Esempio: '2007-05-08 12:35:29.1234567 +12:15'|I dati di origine non possono superare il numero specificato di secondi frazionari nella colonna datetimeoffset. Se l'origine dati contiene un numero minore o uguale di frazioni di secondo, i dati vengono anteposti a destra con zeri. Ad esempio, se il tipo di dati datetimeoffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15 ' viene inserito come ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipi di dati datetime2  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **datetime2** (*n*). Il formato predefinito è 'aaaa-MM-GG: ' ss. fffffff. Una stringa vuota (") viene convertita il valore predefinito ' 1900-01-01-12:00:00". Le stringhe che contengono solo spazi vuoti (' ') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Ad esempio, una colonna definita come **datetime2** (2) avranno due cifre frazionarie.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Valore letterale stringa nel **datetime** formato|'aaaa-MM-gg hh.mm.ss [. fff]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|I secondi frazionari sono facoltativi e vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **smalldatetime** formato|'aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12'|Secondi facoltativi e cifra frazionaria rimanente viene impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'aaaa-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08' viene inserito come ' 2007-05-08 12:00:00.0000000'.|  
|Valore letterale stringa nel **datetime2** formato|'aaaa-MM-gg hh:mm:ss:fffffff'<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|Se l'origine dati contiene i componenti di data e ora che sono minore o uguale al valore specificato **datetime2**(*n*), vengono inseriti i dati; in caso contrario, viene generato un errore.|  
  
### <a name="DateFormats"></a>Formati di data/ora  
Dwloader supporta i seguenti formati di dati per i dati di input che il caricamento in SQL Server PDW. Altri dettagli sono elencati sotto la tabella.  
  
|datetime|smalldatetime|Data|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
Dettagli:  
  
-   Per separare i valori di mese, giorno e anno, è possibile usare '-', '/' o '. '. Per semplicità, nella tabella viene usato solo il separatore "-".  
  
-   Per specificare il mese come testo usare tre o più caratteri. Mesi con caratteri di 1 o 2 verranno interpretati come un numero.  
  
-   Per separare i valori di ora, usare i ': ' simbolo.  
  
-   Le lettere tra parentesi quadre sono facoltative.  
  
-   Le lettere "tt" designano [AM|PM|am|pm]. AM è l'impostazione predefinita. Se si specifica "tt", il valore dell'ora (hh) deve essere compreso nell'intervallo da 0 a 12.  
  
-   Le lettere "zzz" designano la differenza di fuso orario per il fuso orario corrente del sistema nel formato {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Inserimento di valori letterali in tipi numerici  
Nelle tabelle seguenti definiscono le regole di conversione e formato predefinito per il caricamento di un valore letterale in una colonna di SQL Server PDW che utilizza un tipo numerico.  
  
### <a name="bit-data-type"></a>Tipo di dati bit  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **bit**. Una stringa vuota (") o una stringa che contiene solo spazi vuoti (' ') viene convertito in 0.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati di tipo bit|  
|-------------------|-----------------------|-------------------------------|  
|Valore letterale stringa nel **integer** formato|'ffffffffff'<br /><br />Esempio: '321' o '1'|Un valore intero formattato come valore letterale stringa non può contenere un valore negativo. Ad esempio, il valore '-123' genera un errore.<br /><br />Un valore maggiore di 1 viene convertito in 1. Il valore "123", ad esempio, viene convertito in 1.|  
|Valore letterale stringa|'TRUE' o 'FALSE'<br /><br />Esempio: 'true'|Il valore 'TRUE' viene convertito in 1. il valore 'FALSE' viene convertita in 0.|  
|Valore letterale integer|fffffffn<br /><br />Esempio: 1 o 321|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori -123 e 123 sono convertiti in 1.|  
|Valore letterale decimale|fffnn.fffn<br /><br />Esempio: 1234.5678|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123,45 e -123.45 vengono convertiti in 1.|  
  
### <a name="decimal-data-type"></a>Tipo di dati Decimal  
Nella tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **decimale** (*p, s*). Le regole di conversione dei dati sono identico a quello di SQL Server. Per altre informazioni, vedere [conversione di tipi di dati (motore di Database)](https://go.microsoft.com/fwlink/?LinkId=202128) su MSDN.  
  
|Tipo di dati di input|Esempi di dati di input|  
|-------------------|-----------------------|  
|Valore letterale integer|321312313123|  
|Valore letterale decimale|123344.34455|  
  
### <a name="float-and-real-data-types"></a>Tipi di dati float e real  
Nella tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **float** oppure **reale**. Le regole di conversione dei dati sono identico a quello di SQL Server. Per altre informazioni, vedere [conversione di tipi di dati (motore di Database)](../t-sql/data-types/data-type-conversion-database-engine.md) su MSDN.  
  
|Tipo di dati di input|Esempi di dati di input|  
|-------------------|-----------------------|  
|Valore letterale integer|321312313123|  
|Valore letterale decimale|123344.34455|  
|Valore letterale mobile punto|3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint i tipi di dati  
Nella tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **int**, **bigint**, **tinyint**, oppure **smallint**. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **tinyint** è compreso tra 0 e 255 e l'intervallo per **int** è compreso tra -2.147.483.648 e 2.147.483.647.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipi di dati Integer|  
|-------------------|-----------------------|------------------------------------|  
|Valore letterale integer|321312313123||  
|Valore letterale decimale|123344.34455|I valori a destra del separatore decimale vengono troncati.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipi di dati Money e smallmoney  
Valori letterali di denaro sono rappresentati sotto forma di stringa di numeri con separatore decimale facoltativo e un simbolo di valuta facoltativo come prefisso. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **smallmoney** è-214.748,3648 e 214.748,3647 e l'intervallo per **denaro** è-922.337.203.685.477,5808 e 922.337.203.685.477,5807. Nella tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **denaro** oppure **smallmoney**.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione di denaro o tipo di dati smallmoney|  
|-------------------|-----------------------|-----------------------------------------------|  
|Valore letterale integer|321312|Le cifre mancante dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale 12345 viene inserito come 12345.0000|  
|Valore letterale decimale|123344.34455|Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123344.34455 viene inserito come 123344.3446.|  
|Valore letterale Money|$123456.7890|Il simbolo di valuta non verrà inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino.|  
  
## <a name="InsertStringTypes"></a>Inserimento di valori letterali in tipi di stringa  
Nelle tabelle seguenti definiscono le regole di conversione e formato predefinito per il caricamento di un valore letterale in una colonna di SQL Server PDW che utilizza un tipo stringa.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipi di dati char, varchar, nchar e nvarchar  
Nella tabella seguente definisce il formato predefinito e le regole per il caricamento di valori letterali in una colonna di tipo **char**, **varchar**, **nchar** e **nvarchar** . La lunghezza di origine dei dati non può superare le dimensioni specificate per il tipo di dati. Se la lunghezza di origine dati è inferiore alle dimensioni dei **char** oppure **nchar** tipo di dati, i dati vengano applicato un riempimento a destra con spazi vuoti per raggiungere le dimensioni di tipo di dati.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipi di dati carattere|  
|---------------|-------------------|----------------------------------|  
|Valore letterale stringa|Formato: "carattere stringa'<br /><br />Esempio: 'abc'| ND |  
|Valore letterale stringa Unicode|Formato: Stringa N'character'<br /><br />Esempio: N'abc'| ND |  
|Valore letterale integer|Formato: ffffffffffn<br /><br />Esempio: 321312313123| ND |  
|Valore letterale decimale|Formato: ffffff.fffffff<br /><br />Esempio: 12344.34455| ND |  
|Valore letterale Money|Format: $ffffff.fffnn<br /><br />Esempio: $123456.99|Il simbolo di valuta facoltativo non viene inserito con il valore. Per inserire il simbolo di valuta, inserire il valore come valore letterale stringa. Ciò corrisponderà il formato del caricatore, che considera ogni valore letterale come valore letterale stringa.<br /><br />Le virgole non sono consentite.<br /><br />Se il numero di cifre dopo il separatore decimale è superiore a 2, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123.946789 viene inserito come 123.95.<br /><br />Quando si usa la funzione CONVERT per inserire valori letterali di denaro, è consentito solo lo stile predefinito 0 (Nessun separatore delle migliaia e 2 cifre dopo il separatore decimale).|  
  
### <a name="general-remarks"></a>Osservazioni generali  
**dwloader** esegue le stesse conversioni implicite che esegue SQL Server SMP, ma non supporta tutte le conversioni implicite supportati da SQL Server SMP.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
