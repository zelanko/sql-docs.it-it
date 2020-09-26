---
title: Regole di conversione del tipo di dati Dwloader
description: Questo argomento descrive i formati di dati di input e le conversioni implicite dei tipi di dati che il caricatore della riga di comando di dwloader supporta quando carica i dati in Parallel data warehouse (PDW). "
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c1ce48c3352ffbd0a1c112f7fd60db2f0d85c6e6
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379560"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Regole di conversione del tipo di dati per dwloader-Parallel data warehouse
Questo argomento descrive i formati di dati di input e le conversioni implicite dei tipi di dati che il [caricatore da riga di comando di dwloader](dwloader.md) supporta quando carica i dati in PDW. Le conversioni di dati implicite si verificano quando i dati di input non corrispondono al tipo di dati nella tabella di destinazione SQL Server PDW. Usare queste informazioni quando si progetta il processo di caricamento per assicurarsi che i dati vengano caricati correttamente in SQL Server PDW.  
   
  
## <a name="inserting-literals-into-binary-types"></a><a name="InsertBinaryTypes"></a>Inserimento di valori letterali in tipi binari  
Nella tabella seguente vengono definiti i tipi letterali accettati, il formato e le regole di conversione per il caricamento di un valore letterale in una colonna SQL Server PDW di tipo **Binary** (*n*) o **varbinary**(*n*).  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati binary o varbinary|  
|-------------------|-----------------------|-----------------------------------------------|  
|Valore letterale binario|0x *hexidecimal_string*<br /><br />Esempio: 12Ef o 0x12Ef|Il prefisso 0x è facoltativo.<br /><br />La lunghezza dell'origine dati non può superare il numero di byte specificato per il tipo di dati.<br /><br />Se la lunghezza dell'origine dati è inferiore alla dimensione del tipo di dati **binario** , i dati vengono riempiti a destra con zeri per raggiungere le dimensioni del tipo di dati.|  
  
## <a name="inserting-literals-into-date-and-time-types"></a><a name="InsertDateTimeTypes"></a>Inserimento di valori letterali in tipi di data e ora  
I valori letterali di data e ora vengono rappresentati usando valori letterali stringa in formati specifici, racchiusi tra virgolette singole. Nelle tabelle seguenti vengono definiti i tipi letterali consentiti, il formato e le regole di conversione per il caricamento di un valore letterale di data o ora in una colonna di tipo **DateTime**, **smalldatetime**, **date**, **Time**, **DateTimeOffset**o **datetime2**. Le tabelle definiscono il formato predefinito per il tipo di dati specificato. Altri formati che è possibile specificare sono definiti nella sezione [formati DateTime](#DateFormats). I valori letterali di data e ora non possono includere spazi iniziali o finali. i valori **date**, **smalldatetime**e null non possono essere caricati in modalità a larghezza fissa.  
  
### <a name="datetime-data-type"></a>Tipi di dati datetime  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **DateTime**. Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00.000'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione nel tipo di dati DateTime|  
|-------------------|-----------------------|------------------------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. fff]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|Le cifre frazionarie mancanti sono impostate su 0 quando il valore viene inserito. Il valore letterale "2007-05-08 12:35", ad esempio, viene inserito come "2007-05-08 12:35:00.000".|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12:35'|I secondi e le cifre frazionarie rimanenti vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) sono impostati su 12:00:00.000 quando viene inserito il valore.|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS. fffffff '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|I dati di origine non possono superare tre cifre frazionarie. Ad esempio, verrà inserito il valore letterale "2007-05-08 12:35:29.123", ma il valore "2007-05-8 12:35:29.1234567" genera un errore.|  
  
### <a name="smalldatetime-data-type"></a>Tipo di dati smalldatetime  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **smalldatetime**. Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm ' o ' AAAA-MM-GG HH: mm: SS '<br /><br />Esempio: "2007-05-08 12:00" o "2007-05-08 12:00:15"|I dati di origine devono contenere valori per anno, mese, data, ora e minuto. I secondi sono facoltativi e, se presenti, devono essere impostati sul valore 00. Qualsiasi altro valore genera un errore.<br /><br />I secondi sono facoltativi. Quando si esegue il caricamento in una colonna smalldatetime, dwloader arrotonda i secondi e i secondi frazionari. Ad esempio, 1999-01-05 20:10:35.123 viene caricato come 01-05 20:11.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore.|  
  
### <a name="date-data-type"></a>Tipo di dati date  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **date**. Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati date|  
|-------------------|-----------------------|--------------------------------|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'||  
  
### <a name="time-data-type"></a>Tipo di dati time  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **Time**. Una stringa vuota ('') viene convertita nel valore predefinito ' 00:00:00.0000'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati time|  
|-------------------|-----------------------|--------------------------------|  
|Valore letterale stringa nel formato **Time**|' HH: mm: SS. fffffff '<br /><br />Esempio:' 12:35:29.1234567'|Se l'origine dati ha una precisione minore o uguale (numero di cifre frazionarie) rispetto alla precisione del tipo di dati **Time** , i dati vengono riempiti a destra con zeri. Ad esempio, un valore letterale ' 12:35:29.123' viene inserito come ' 12:35:29.1230000'.|  
  
### <a name="datetimeoffset-data-type"></a>DateTimeOffset-tipo di dati  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **DateTimeOffset** (*n*). Il formato predefinito è "AAAA-MM-GG HH: mm: SS. fffffff {+ |-} HH: mm". Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00.0000000 + 00:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Una colonna definita come **DateTimeOffset** (2), ad esempio, avrà due cifre frazionarie.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione nel tipo di dati DateTimeOffset|  
|-------------------|-----------------------|------------------------------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. fff]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|Le cifre frazionarie mancanti e i valori di offset vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' viene inserito come ' 2007-05-08 12:35:29.1230000 + 00:00'.|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12:35'|Secondi, le cifre frazionarie rimanenti e i valori di offset vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Il valore letterale "2007-05-08", ad esempio, viene inserito come "2007-05-08 00:00:00.0000000 + 00:00".|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS. fffffff '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|I dati di origine non possono superare il numero di secondi frazionari specificato nella colonna DateTimeOffset. Se l'origine dati ha un numero minore o uguale di secondi frazionari, i dati vengono riempiti a destra con zeri. Se, ad esempio, il tipo di dati è DateTimeOffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15' viene inserito come ' 12:35:29.12300 + 12:15'.|  
|Valore letterale stringa in formato **DateTimeOffset**|' AAAA-MM-GG HH: mm: SS. fffffff {+&#124;-} HH: mm '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567 + 12:15'|I dati di origine non possono superare il numero di secondi frazionari specificato nella colonna DateTimeOffset. Se l'origine dati ha un numero minore o uguale di secondi frazionari, i dati vengono riempiti a destra con zeri. Se, ad esempio, il tipo di dati è DateTimeOffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15' viene inserito come ' 12:35:29.12300 + 12:15'.|  
  
### <a name="datetime2-data-type"></a>Tipi di dati datetime2  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **datetime2** (*n*). Il formato predefinito è "AAAA-MM-GG HH: mm: SS. fffffff". Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Una colonna definita come **datetime2** (2), ad esempio, avrà due cifre frazionarie.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione al tipo di dati datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. fff]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|I secondi frazionari sono facoltativi e vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12'|I secondi facoltativi e le cifre frazionarie rimanenti vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Il valore letterale "2007-05-08", ad esempio, viene inserito come "2007-05-08 12:00:00.0000000".|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS: fffffff '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|Se l'origine dati contiene componenti di data e ora che sono minori o uguali al valore specificato in **datetime2**(*n*), i dati vengono inseriti. in caso contrario, viene generato un errore.|  
  
### <a name="datetime-formats"></a><a name="DateFormats"></a>Formati DateTime  
Dwloader supporta i formati di dati seguenti per i dati di input che sta caricando in SQL Server PDW. Ulteriori dettagli sono elencati dopo la tabella.  
  
|Datetime|smalldatetime|Data|datetime2|datetimeoffset|  
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
  
-   Per separare i valori di mese, giorno e anno, è possibile usare '-','/' o '. '. Per semplicità, nella tabella viene usato solo il separatore "-".  
  
-   Per specificare il mese come testo usare tre o più caratteri. I mesi con 1 o 2 caratteri verranno interpretati come un numero.  
  
-   Per separare i valori temporali, usare il simbolo ':'.  
  
-   Le lettere tra parentesi quadre sono facoltative.  
  
-   Le lettere "tt" designano [AM|PM|am|pm]. AM è l'impostazione predefinita. Se si specifica "tt", il valore dell'ora (hh) deve essere compreso nell'intervallo da 0 a 12.  
  
-   Le lettere "zzz" designano la differenza di fuso orario per il fuso orario corrente del sistema nel formato {+|-}HH:ss].  
  
## <a name="inserting-literals-into-numeric-types"></a><a name="InsertNumerictypes"></a>Inserimento di valori letterali in tipi numerici  
Nelle tabelle seguenti vengono definiti il formato predefinito e le regole di conversione per il caricamento di un valore letterale in una colonna SQL Server PDW che utilizza un tipo numerico.  
  
### <a name="bit-data-type"></a>bit-tipo di dati  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **bit**. Una stringa vuota ('') o una stringa che contiene solo spazi vuoti ('') viene convertita in 0.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati bit|  
|-------------------|-----------------------|-------------------------------|  
|Valore letterale stringa in formato **Integer**|ffffffffff<br /><br />Esempio: "1" o "321"|Un valore integer formattato come valore letterale stringa non può contenere un valore negativo. Il valore "-123", ad esempio, genera un errore.<br /><br />Un valore maggiore di 1 viene convertito in 1. Il valore "123", ad esempio, viene convertito in 1.|  
|Valore letterale stringa|' TRUE ' o ' FALSE '<br /><br />Esempio:' true '|Il valore ' TRUE ' viene convertito in 1. il valore ' FALSE ' viene convertito in 0.|  
|Valore letterale integer|fffffffn<br /><br />Esempio: 1 o 321|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123 e-123 vengono convertiti in 1.|  
|Valore letterale decimale|fffnn.fffn<br /><br />Esempio: 1234,5678|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123,45 e-123,45 vengono convertiti in 1.|  
  
### <a name="decimal-data-type"></a>Tipo di dati Decimal  
La tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **Decimal** (*p, s*). Le regole di conversione dei dati sono uguali a quelle per SQL Server. Per ulteriori informazioni, vedere [conversione del tipo di dati (motore di database)](/previous-versions/sql/sql-server-2008-r2/ms191530(v=sql.105)) su MSDN.  
  
|Tipo di dati di input|Esempi di dati di input|  
|-------------------|-----------------------|  
|Valore letterale integer|321312313123|  
|Valore letterale decimale|123344,34455|  
  
### <a name="float-and-real-data-types"></a>Tipi di dati float e Real  
La tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **float** o **Real**. Le regole di conversione dei dati sono uguali a quelle per SQL Server. Per ulteriori informazioni, vedere [conversione del tipo di dati (motore di database)](../t-sql/data-types/data-type-conversion-database-engine.md) su MSDN.  
  
|Tipo di dati di input|Esempi di dati di input|  
|-------------------|-----------------------|  
|Valore letterale integer|321312313123|  
|Valore letterale decimale|123344,34455|  
|Valore letterale a virgola mobile|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>Tipi di dati int, bigint, tinyint, smallint  
La tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **int**, **bigint**, **tinyint**o **smallint**. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **tinyint** è compreso tra 0 e 255 e l'intervallo per **int** è-2.147.483.648 a 2.147.483.647.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipi di dati Integer|  
|-------------------|-----------------------|------------------------------------|  
|Valore letterale integer|321312313123||  
|Valore letterale decimale|123344,34455|I valori a destra del separatore decimale vengono troncati.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipi di dati Money e smallmoney  
I valori letterali Money sono rappresentati come una stringa di numeri con un separatore decimale facoltativo e un simbolo di valuta facoltativo come prefisso. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **smallmoney** è da-214.748,3648 a 214.748,3647 e l'intervallo per **money** è-922.337.203.685.477,5808 a 922.337.203.685.477,5807. La tabella seguente definisce le regole per il caricamento di valori letterali in una colonna di tipo **Money** o **smallmoney**.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipo di dati Money o smallmoney|  
|-------------------|-----------------------|-----------------------------------------------|  
|Valore letterale integer|321312|Le cifre mancanti dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale 12345 viene inserito come 12345,0000|  
|Valore letterale decimale|123344,34455|Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123344,34455 viene inserito come 123344,3446.|  
|Valore letterale money|$123456,7890|Il simbolo di valuta non viene inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino.|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertStringTypes"></a>Inserimento di valori letterali in tipi stringa  
Nelle tabelle seguenti vengono definiti il formato predefinito e le regole di conversione per il caricamento di un valore letterale in una colonna SQL Server PDW che utilizza un tipo stringa.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipi di dati char, varchar, nchar e nvarchar  
La tabella seguente definisce il formato e le regole predefinite per il caricamento di valori letterali in una colonna di tipo **char**, **varchar**, **nchar** e **nvarchar**. La lunghezza dell'origine dati non può superare la dimensione specificata per il tipo di dati. Se la lunghezza dell'origine dati è inferiore alla dimensione del tipo di dati **char** o **nchar** , i dati vengono riempiti a destra con spazi vuoti per raggiungere le dimensioni del tipo di dati.  
  
|Tipo di dati di input|Esempi di dati di input|Conversione in tipi di dati character|  
|---------------|-------------------|----------------------------------|  
|Valore letterale stringa|Formato:' stringa di caratteri '<br /><br />Esempio:' ABC '| N/D |  
|Valore letterale stringa Unicode|Formato: N'character String '<br /><br />Esempio: N'ABC '| N/D |  
|Valore letterale integer|Formato: ffffffffffn<br /><br />Esempio: 321312313123| N/D |  
|Valore letterale decimale|Formato: FFFFFF. fffffff<br /><br />Esempio: 12344,34455| N/D |  
|Valore letterale money|Formato: $ffffff. fffnn<br /><br />Esempio: $123456,99|Il simbolo di valuta facoltativo non viene inserito con il valore. Per inserire il simbolo di valuta, inserire il valore come valore letterale stringa. Questo corrisponde al formato del caricatore, che considera ogni valore letterale come valore letterale stringa.<br /><br />Virgole non consentite.<br /><br />Se il numero di cifre dopo il separatore decimale è maggiore di 2, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123,946789 viene inserito come 123,95.<br /><br />Quando si usa la funzione CONVERT per inserire valori letterali Money, è consentito solo lo stile predefinito 0 (nessuna virgola e 2 cifre dopo il separatore decimale).|  
  
### <a name="general-remarks"></a>Osservazioni generali  
**dwloader** esegue le stesse conversioni implicite eseguite da SMP SQL Server, ma non supporta tutte le conversioni implicite supportate da SMP SQL Server.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
