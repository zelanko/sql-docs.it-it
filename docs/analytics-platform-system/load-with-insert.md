---
title: Caricare i dati con INSERT
description: Usare l'istruzione T-SQL INSERT per caricare i dati in una tabella distribuita o replicata in parallelo data warehouse (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bbcf1a8bd16d7446841bb6d7dd86bd1ad350280d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401025"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Caricare i dati con INSERT in Parallel data warehouse

È possibile utilizzare l'istruzione TSQL INSERT per caricare dati in una tabella distribuita o replicata SQL Server Parallel data warehouse (PDW). Per ulteriori informazioni su INSERT, vedere [Insert](../t-sql/statements/insert-transact-sql.md). Per le tabelle replicate e tutte le colonne non di distribuzione in una tabella distribuita, PDW utilizza SQL Server per convertire in modo implicito i valori dei dati specificati nell'istruzione nel tipo di dati della colonna di destinazione. Per ulteriori informazioni sulle regole di conversione dei dati SQL Server, vedere [conversione del tipo di dati per SQL](../t-sql/data-types/data-type-conversion-database-engine.md). Per le colonne di distribuzione, tuttavia, PDW supporta solo un subset di conversioni implicite supportate da SQL Server. Pertanto, quando si utilizza l'istruzione INSERT per caricare dati in una colonna di distribuzione, è necessario specificare i dati di origine in uno dei formati definiti nelle tabelle seguenti.  
  
  
## <a name="insert-literals-into-binary-types"></a><a name="InsertingLiteralsBinary"></a>Inserire valori letterali in tipi binari  
Nella tabella seguente vengono definiti i tipi letterali accettati, il formato e le regole di conversione per l'inserimento di un valore letterale in una colonna di distribuzione di tipo **Binary** (*n*) o **varbinary**(*n*).  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale binario|0x*hexidecimal_string*<br /><br />Esempio: 0x12Ef|I valori letterali binari devono essere preceduti da 0x.<br /><br />La lunghezza dell'origine dati non può superare il numero di byte specificato per il tipo di dati.<br /><br />Se la lunghezza dell'origine dati è inferiore alla dimensione del tipo di dati **binario** , i dati vengono riempiti a destra con zeri per raggiungere le dimensioni del tipo di dati.|  
  
## <a name="insert-literals-into-date-and-time-types"></a><a name="InsertingLiteralsDateTime"></a>Inserire valori letterali in tipi di data e ora  
I valori letterali di data e ora vengono rappresentati utilizzando valori di carattere in formati specifici, racchiusi tra virgolette singole. Nelle tabelle seguenti vengono definiti i tipi letterali consentiti, il formato e le regole di conversione per l'inserimento di un valore letterale di data o ora in una colonna di distribuzione SQL Server PDW di tipo **DateTime**, **smalldatetime**, **date**, **Time**, **DateTimeOffset**o **datetime2**.  
  
### <a name="datetime-data-type"></a>datetime (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **DateTime**. Qualsiasi stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00.000'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. nnn]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|Le cifre frazionarie mancanti sono impostate su 0 quando il valore viene inserito. Il valore letterale "2007-05-08 12:35", ad esempio, viene inserito come "2007-05-08 12:35:00.000".|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12:35'|I secondi e le cifre frazionarie rimanenti vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) sono impostati su 12:00:00.000 quando viene inserito il valore.|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS. nnnnnnn '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|I dati di origine non possono superare tre cifre frazionarie. Ad esempio, verrà inserito il valore letterale "2007-05-08 12:35:29.123", ma il valore "2007-05-08 12:35:29.1234567" genera un errore.|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **smalldatetime**. Qualsiasi stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **smalldatetime**|"AAAA-MM-GG HH: mm" o "AAAA-MM-GG HH: mm: 00"<br /><br />Esempio: "2007-05-08 12:00" o "2007-05-08 12:00:00"|I dati di origine devono contenere valori per anno, mese, data, ora e minuto. I secondi sono facoltativi e, se presenti, devono essere impostati sul valore 00. Qualsiasi altro valore genera un errore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore.|  
  
### <a name="date-data-type"></a>date (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **date**. Qualsiasi stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|Si tratta dell'unico formato accettato.|  
  
### <a name="time-data-type"></a>time (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **Time**. Qualsiasi stringa vuota ('') viene convertita nel valore predefinito ' 00:00:00.0000'. Le stringhe che contengono solo spazi vuoti ('') generano un errore.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel formato **Time**|' HH: mm: SS. nnnnnnn '<br /><br />Esempio:' 12:35:29.1234567'|Se l'origine dati ha una precisione minore o uguale (numero di cifre frazionarie) rispetto alla precisione del tipo di dati **Time** , i dati vengono riempiti a destra con zeri. Ad esempio, un valore letterale ' 12:35:29.123' viene inserito come ' 12:35:29.1230000'.<br /><br />Valore con una precisione maggiore rispetto al tipo di dati di destinazione rifiutato.|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **DateTimeOffset** (*n*). Il formato predefinito è "AAAA-MM-GG HH: mm: SS. nnnnnnn {+ |-} hh: mm". Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00.0000000 + 00:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Una colonna definita come **DateTimeOffset** (2), ad esempio, avrà due cifre frazionarie.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. nnn]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|Le cifre frazionarie mancanti e i valori di offset vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' viene inserito come ' 2007-05-08 12:35:29.1230000 + 00:00'.|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12:35'|Secondi, le cifre frazionarie rimanenti e i valori di offset vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Il valore letterale "2007-05-08", ad esempio, viene inserito come "2007-05-08 00:00:00.0000000 + 00:00".|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS. nnnnnnn '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|I dati di origine non possono superare il numero di secondi frazionari specificato nella colonna DateTimeOffset. Se l'origine dati ha un numero minore o uguale di secondi frazionari, i dati vengono riempiti a destra con zeri. Se, ad esempio, il tipo di dati è DateTimeOffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15' viene inserito come ' 12:35:29.12300 + 12:15'.|  
|Valore letterale stringa in formato **DateTimeOffset**|' AAAA-MM-GG HH: mm: SS. nnnnnnn {+&#124;-} HH: mm '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567 + 12:15'|I dati di origine non possono superare il numero di secondi frazionari specificato nella colonna DateTimeOffset. Se l'origine dati ha un numero minore o uguale di secondi frazionari, i dati vengono riempiti a destra con zeri. Se, ad esempio, il tipo di dati è DateTimeOffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15' viene inserito come ' 12:35:29.12300 + 12:15'.|  
  
### <a name="datetime2-data-type"></a>datetime2 (tipo di dati)  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **datetime2** (*n*). Il formato predefinito è "AAAA-MM-GG HH: mm: SS. nnnnnnn". Una stringa vuota ('') viene convertita nel valore predefinito ' 1900-01-01 12:00:00'. Le stringhe che contengono solo spazi vuoti ('') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Una colonna definita come **datetime2** (2), ad esempio, avrà due cifre frazionarie.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **DateTime**|' AAAA-MM-GG HH: mm: SS [. nnn]'<br /><br />Esempio:' 2007-05-08 12:35:29.123'|I secondi frazionari sono facoltativi e vengono impostati su 0 quando viene inserito il valore.<br /><br />Valore con più cifre frazionarie rispetto al tipo di dati di destinazione rifiutato.|  
|Valore letterale stringa in formato **smalldatetime**|' AAAA-MM-GG HH: mm '<br /><br />Esempio:' 2007-05-08 12'|I secondi facoltativi e le cifre frazionarie rimanenti vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel formato **Data**|' AAAA-MM-GG '<br /><br />Esempio:' 2007-05-08'|I valori di ora (ora, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Il valore letterale "2007-05-08", ad esempio, viene inserito come "2007-05-08 12:00:00.0000000".|  
|Valore letterale stringa in formato **datetime2**|' AAAA-MM-GG HH: mm: SS: nnnnnnn '<br /><br />Esempio:' 2007-05-08 12:35:29.1234567'|Se l'origine dati contiene componenti di data e ora che sono minori o uguali al valore specificato in **datetime2**(*n*), i dati vengono inseriti. in caso contrario, viene generato un errore.|  
  
## <a name="insert-literals-into-numeric-types"></a><a name="InsertLiteralsNumeric"></a>Inserire valori letterali in tipi numerici  
Nelle tabelle seguenti vengono definiti i formati accettati e le regole di conversione per l'inserimento di un valore letterale in una colonna di distribuzione SQL Server PDW che utilizza un tipo numerico.  
  
### <a name="bit-data-type"></a>bit - tipo di dati  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **bit**. Una stringa vuota ('') o una stringa che contiene solo spazi vuoti ('') viene convertita in 0.  
  
|Tipo letterale|format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **Integer**|'nnnnnnnnnn'<br /><br />Esempio: "1" o "321"|Un valore integer formattato come valore letterale stringa non può contenere un valore negativo. Il valore "-123", ad esempio, genera un errore.<br /><br />Un valore maggiore di 1 viene convertito in 1. Il valore "123", ad esempio, viene convertito in 1.|  
|Valore letterale stringa|' TRUE ' o ' FALSE '<br /><br />Esempio:' true '|Il valore ' TRUE ' viene convertito in 1. il valore ' FALSE ' viene convertito in 0.|  
|Valore letterale integer|nnnnnnnn<br /><br />Esempio: 1 o 321|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123 e-123 vengono convertiti in 1.|  
|Valore letterale decimale|nnnnn. nnnn<br /><br />Esempio: 1234,5678|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123,45 e-123,45 vengono convertiti in 1.|  
  
### <a name="decimal-data-type"></a>decimal - tipo di dati  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **Decimal** (*p, s*). Le regole di conversione dei dati sono uguali a quelle per SQL Server. Per ulteriori informazioni, vedere [conversione di tipi di dati](../t-sql/data-types/data-type-conversion-database-engine.md) in MSDN.  
  
|Tipo letterale|Format|  
|----------------|----------|  
|Valore letterale stringa in formato **Integer**|nnnnnnnnnnnn<br /><br />Esempio:' 321312313123'|  
|Valore letterale stringa in formato **decimale**|' nnnnnn. nnnnn '<br /><br />Esempio:' 123344,34455'|  
|Valore letterale integer|nnnnnnnnnnnn<br /><br />Esempio: 321312313123|  
|Valore letterale decimale|nnnnnn. nnnnn<br /><br />Esempio:' 123344,34455'|  
  
### <a name="float-and-real-data-types"></a>tipi di dati float e Real  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **float** o **Real**. Le regole di conversione dei dati sono uguali a quelle per SQL Server. Per ulteriori informazioni, vedere [conversione di tipi di dati](../t-sql/data-types/data-type-conversion-database-engine.md) in MSDN.  
  
|Tipo letterale|Format|  
|----------------|----------|  
|Valore letterale stringa in formato **Integer**|nnnnnnnnnnnn<br /><br />Esempio:' 321312313123'|  
|Valore letterale stringa in formato **decimale**|' nnnnnn. nnnnn '<br /><br />Esempio:' 123344,34455'|  
|Valore letterale stringa nel formato a **virgola mobile**|' n. nnnnnE + nn '<br /><br />Esempio:' 3.12323 E + 14'|  
|Valore letterale integer|nnnnnnnnnnnn<br /><br />Esempio: 321312313123|  
|Valore letterale decimale|nnnnnn. nnnnn<br /><br />Esempio: 123344,34455|  
|Valore letterale a virgola mobile|n. nnnnnE + nn<br /><br />Esempio: 3.12323 E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>tipi di dati int, bigint, tinyint, smallint  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **int**, **bigint**, **tinyint**o **smallint**. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **tinyint** è compreso tra 0 e 255 e l'intervallo per **int** è-2.147.483.648 a 2.147.483.647.  
  
|Tipo di valore letterale|Format|Regole di conversione|  
|------------|------|----------------|
|Valore letterale stringa in formato **Integer**|'nnnnnnnnnnnnnn'<br /><br />Esempio:' 321312313123'| nessuno |  
|Valore letterale integer|nnnnnnnnnnnnnn<br /><br />Esempio: 321312313123| nessuno|  
|Valore letterale decimale|nnnnnn. nnnnn<br /><br />Esempio: 123344,34455|I valori a destra del separatore decimale vengono troncati.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipi di dati Money e smallmoney  
I valori letterali Money sono rappresentati come numeri con un separatore decimale facoltativo e un simbolo di valuta come prefisso. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **smallmoney** è da-214.748,3648 a 214.748,3647 e l'intervallo per **money** è-922.337.203.685.477,5808 a 922.337.203.685.477,5807. Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **Money** o **smallmoney**.  
  
|Tipo letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa in formato **Integer**|nnnnnnnn<br /><br />Esempio:' 123433'|Le cifre mancanti dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 12345' viene inserito come 12345,0000.|  
|Valore letterale stringa in formato **decimale**|' nnnnnn. nnnnn '<br /><br />Esempio:' 123344,34455'|Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino. Il valore "123344,34455", ad esempio, viene inserito come 123344,3446.|  
|Valore letterale stringa in formato **Money**|' $nnnnnn. nnnn '<br /><br />Esempio:' $123456,7890'|Il simbolo di valuta facoltativo non viene inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino.|  
|Valore letterale integer|nnnnnnnn<br /><br />Esempio: 123433|Le cifre mancanti dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Il valore letterale 12345, ad esempio, viene inserito come 12345,0000.|  
|Valore letterale decimale|nnnnnn. nnnnn<br /><br />Esempio: 123344,34455|Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123344,34455 viene inserito come 123344,3446.|  
|Valore letterale money|$nnnnnn. nnnn<br /><br />Esempio: $123456,7890|Il simbolo di valuta facoltativo non viene inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è maggiore di 4, il valore viene arrotondato per eccesso al valore più vicino.|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertLiteralsString"></a>Inserimento di valori letterali in tipi stringa  
Nelle tabelle seguenti vengono definiti i formati accettati e le regole di conversione per l'inserimento di un valore letterale in una colonna SQL Server PDW che utilizza un tipo stringa.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipi di dati char, varchar, nchar e nvarchar  
Nella tabella seguente vengono definiti i formati e le regole accettati per l'inserimento di valori letterali in una colonna di distribuzione di tipo **char**, **varchar**, **nchar** e **nvarchar**. La lunghezza dell'origine dati non può superare la dimensione specificata per il tipo di dati. Se la lunghezza dell'origine dati è inferiore alla dimensione del tipo di dati **char** o **nchar** , i dati vengono riempiti a destra con spazi vuoti per raggiungere le dimensioni del tipo di dati.  
  
|Tipo di valore letterale|Format|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa|Formato:' stringa di caratteri '<br /><br />Esempio:' ABC '| nessuno|  
|Valore letterale stringa Unicode|Formato: N'character String '<br /><br />Esempio: N'ABC '|  nessuno |  
|Valore letterale integer|Formato: nnnnnnnnnnn<br /><br />Esempio: 321312313123| nessuno |  
|Valore letterale decimale|Formato: nnnnnn. nnnnnnn<br /><br />Esempio: 12344,34455| nessuno |  
|Valore letterale money|Formato: $nnnnnn. nnnnn<br /><br />Esempio: $123456,99|Il simbolo di valuta non viene inserito con il valore. Per inserire il simbolo di valuta, inserire il valore come valore letterale stringa. Questo corrisponde al formato dello strumento **dwloader** , che considera ogni valore letterale come valore letterale stringa.<br /><br />Virgole non consentite.<br /><br />Se il numero di cifre dopo il separatore decimale è maggiore di 2, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123,946789 viene inserito come 123,95.<br /><br />Quando si usa la funzione CONVERT per inserire valori letterali Money, è consentito solo lo stile predefinito 0 (nessuna virgola e 2 cifre dopo il separatore decimale).|  

  
## <a name="see-also"></a>Vedere anche  
 
[Dati distribuiti](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERIRE](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
