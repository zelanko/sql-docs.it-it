---
title: Caricare dati con INSERT - Parallel Data Warehouse | Microsoft Docs
description: Tramite l'istruzione T-SQL INSERT per caricare i dati in un Parallel Data Warehouse (PDW) distribuite o tabella replicata.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b13daf2d32cc41d63deea6c612dde247d541e4d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128560"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Caricare dati con l'istruzione INSERT in Parallel Data Warehouse

È possibile utilizzare l'istruzione t-SQL INSERT per caricare dati in un SQL Server Parallel Data Warehouse (PDW) distribuite o tabella replicata. Per altre informazioni sull'inserimento, vedere [Inserisci](../t-sql/statements/insert-transact-sql.md). Per le tabelle replicate e tutte le colonne non distribuzione in una tabella distribuita, usano PDW SQL Server da convertire in modo implicito i valori di dati specificati nell'istruzione per il tipo di dati della colonna di destinazione. Per altre informazioni sulle regole di conversione dei dati di SQL Server, vedere [conversione SQL del tipo di dati](../t-sql/data-types/data-type-conversion-database-engine.md). Tuttavia, per le colonne di distribuzione, PDW supporta solo un subset delle conversioni implicite che supporta SQL Server. Pertanto, quando si utilizza l'istruzione INSERT per caricare dati in una colonna di distribuzione, i dati di origine devono essere specificati in uno dei formati definiti nelle tabelle seguenti.  
  
  
## <a name="InsertingLiteralsBinary"></a>Inserire i valori letterali in tipi binari  
Nella tabella seguente definisce le regole di conversione per l'inserimento di un valore letterale in una colonna di distribuzione di tipo, formato e tipi letterali accettati **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale binario|0x*hexidecimal_string*<br /><br />Esempio: 0x12Ef|I valori letterali binari devono essere preceduti da 0x.<br /><br />La lunghezza di origine dei dati non può superare il numero di byte specificati per il tipo di dati.<br /><br />Se la lunghezza di origine dati è inferiore alle dimensioni dei **binario** tipo di dati, i dati vengano applicato un riempimento a destra con zeri per raggiungere le dimensioni di tipo di dati.|  
  
## <a name="InsertingLiteralsDateTime"></a>Inserire i valori letterali in tipi di data e ora  
Valori letterali di data e ora sono rappresentati tramite valori di tipo carattere in formati specifici, racchiusi tra virgolette singole. Nelle tabelle seguenti definiscono i tipi letterali consentiti, formato e le regole di conversione per l'inserimento di una data o ora letterale in una colonna di distribuzione di SQL Server PDW typu **data/ora**, **smalldatetime**, **data**, **ora**, **datetimeoffset**, oppure **datetime2**.  
  
### <a name="datetime-data-type"></a>tipo di dati DateTime  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **datetime**. Qualsiasi stringa vuota (") viene convertito il valore predefinito ' 12:00:00.000 1900-01-01'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **datetime** formato|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|Cifre frazionarie mancante vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35 ' viene inserito come ' 2007-05-08 12:35:00.000'.|  
|Valore letterale stringa nel **smalldatetime** formato|'Aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12:35'|Cifra frazionaria rimanente e secondi viene impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'AAAA-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) sono impostati 12:00:00.000 quando viene inserito il valore.|  
|Valore letterale stringa nel **datetime2** formato|'YYYY-MM-DD hh:mm:ss.nnnnnnn'<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|I dati di origine non possono superare tre cifre frazionarie. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' verrà inserito, tranne il valore ' 2007-05-08 12:35:29.1234567' viene generato un errore.|  
  
### <a name="smalldatetime-data-type"></a>tipo di dati smalldatetime  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **smalldatetime**. Qualsiasi stringa vuota (") viene convertito il valore predefinito ' 1900-01-01 GMT+12.00 '. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **smalldatetime** formato|'Aaaa-MM-gg hh: mm' o 'Aaaa-MM-gg hh:mm:00'<br /><br />Esempio: ' 2007-05-08 GMT+12.00 ' o ' 2007-05-08 12:00:00 '|I dati di origine devono avere i valori per anno, mese, data, ora e minuto. Secondi sono facoltativi e, se presente, devono essere impostati su 00 il valore. Qualsiasi altro valore genera un errore.|  
|Valore letterale stringa nel **data** formato|'AAAA-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore.|  
  
### <a name="date-data-type"></a>Tipo di dati date  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **data**. Qualsiasi stringa vuota (") viene convertito il valore predefinito ' 1900-01-01'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **data** formato|'AAAA-MM-GG'<br /><br />Esempio: '2007-05-08'|Questo è l'unico formato accettato.|  
  
### <a name="time-data-type"></a>tipo di dati time  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **ora**. Qualsiasi stringa vuota (") viene convertito il valore predefinito '00:00:00.0000'. Le stringhe che contengono solo spazi vuoti (' ') generano un errore.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **ora** formato|'hh:mm:ss.nnnnnnn'<br /><br />Esempio: '12:35:29.1234567'|Se l'origine dati ha una precisione minore o uguale (numero di cifre frazionarie) quella del **ora** tipo di dati, i dati vengano applicato un riempimento a destra con zeri. Ad esempio, viene inserito un valore letterale '12:35:29.123' come '12:35:29.1230000'.<br /><br />Un valore con una precisione maggiore rispetto al tipo di dati di destinazione viene rifiutato.|  
  
### <a name="datetimeoffset-data-type"></a>tipo di dati DateTimeOffset  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **datetimeoffset** (*n*). Il formato predefinito è ' aaaa-MM-GG nnnnnnn {+ |-} hh: mm '. Una stringa vuota (") viene convertita il valore predefinito ' 12:00:00.0000000 1900-01-01 + 00:00 '. Le stringhe che contengono solo spazi vuoti (' ') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Ad esempio, una colonna definita come **datetimeoffset** (2) avranno due cifre frazionarie.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **datetime** formato|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|Cifre frazionarie mancante e valori di offset sono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08 12:35:29.123' viene inserito come ' 12:35:29.1230000 2007-05-08 + 00:00 '.|  
|Valore letterale stringa nel **smalldatetime** formato|'Aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12:35'|Valori di offset, cifra frazionaria rimanente e secondi vengono impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'AAAA-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08' viene inserito come ' 00.00.00.0000000 2007-05-08 + 00:00 '.|  
|Valore letterale stringa nel **datetime2** formato|'YYYY-MM-DD hh:mm:ss.nnnnnnn'<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|I dati di origine non possono superare il numero specificato di secondi frazionari nella colonna datetimeoffset. Se l'origine dati contiene un numero minore o uguale di frazioni di secondo, i dati vengono anteposti a destra con zeri. Ad esempio, se il tipo di dati datetimeoffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15 ' viene inserito come ' 12:35:29.12300 + 12:15 '.|  
|Valore letterale stringa nel **datetimeoffset** formato|'YYYY-MM-DD hh:mm:ss.nnnnnnn {+&#124;-} hh:mm'<br /><br />Esempio: '2007-05-08 12:35:29.1234567 +12:15'|I dati di origine non possono superare il numero specificato di secondi frazionari nella colonna datetimeoffset. Se l'origine dati contiene un numero minore o uguale di frazioni di secondo, i dati vengono anteposti a destra con zeri. Ad esempio, se il tipo di dati datetimeoffset (5), il valore letterale ' 2007-05-08 12:35:29.123 + 12:15 ' viene inserito come ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>tipo di dati datetime2  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **datetime2** (*n*). Il formato predefinito è 'Aaaa-MM-GG nnnnnnn'. Una stringa vuota (") viene convertita il valore predefinito ' 1900-01-01-12:00:00". Le stringhe che contengono solo spazi vuoti (' ') generano un errore. Il numero di cifre frazionarie dipende dalla definizione della colonna. Ad esempio, una colonna definita come **datetime2** (2) avranno due cifre frazionarie.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **datetime** formato|'YYYY-MM-DD hh:mm:ss[.nnn]'<br /><br />Esempio: '2007-05-08 12:35:29.123'|I secondi frazionari sono facoltativi e vengono impostati su 0 quando viene inserito il valore.<br /><br />Un valore che ha più cifre frazionarie che il tipo di dati di destinazione viene rifiutato.|  
|Valore letterale stringa nel **smalldatetime** formato|'Aaaa-MM-gg hh: mm'<br /><br />Esempio: '2007-05-08 12'|Secondi facoltativi e cifra frazionaria rimanente viene impostati su 0 quando viene inserito il valore.|  
|Valore letterale stringa nel **data** formato|'AAAA-MM-GG'<br /><br />Esempio: '2007-05-08'|I valori di tempo (ore, minuti, secondi e frazioni) vengono impostati su 0 quando viene inserito il valore. Ad esempio, il valore letterale ' 2007-05-08' viene inserito come ' 2007-05-08 12:00:00.0000000'.|  
|Valore letterale stringa nel **datetime2** formato|'Aaaa-MM-gg hh:mm:ss:nnnnnnn'<br /><br />Esempio: '2007-05-08 12:35:29.1234567'|Se l'origine dati contiene i componenti di data e ora che sono minore o uguale al valore specificato **datetime2**(*n*), vengono inseriti i dati; in caso contrario, viene generato un errore.|  
  
## <a name="InsertLiteralsNumeric"></a>Inserire i valori letterali in tipi numerici  
Nelle tabelle seguenti definiscono i formati accettati e le regole di conversione per l'inserimento di un valore letterale in una colonna di distribuzione di SQL Server PDW che utilizza un tipo numerico.  
  
### <a name="bit-data-type"></a>bit - tipo di dati  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **bit**. Una stringa vuota (") o una stringa che contiene solo spazi vuoti (' ') viene convertito in 0.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **integer** formato|'nnnnnnnnnn'<br /><br />Esempio: '321' o '1'|Un valore intero formattato come valore letterale stringa non può contenere un valore negativo. Ad esempio, il valore '-123' genera un errore.<br /><br />Un valore maggiore di 1 viene convertito in 1. Il valore "123", ad esempio, viene convertito in 1.|  
|Valore letterale stringa|'TRUE' o 'FALSE'<br /><br />Esempio: 'true'|Il valore 'TRUE' viene convertito in 1. il valore 'FALSE' viene convertita in 0.|  
|Valore letterale integer|nnnnnnnn<br /><br />Esempio: 1 o 321|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori -123 e 123 sono convertiti in 1.|  
|Valore letterale decimale|nnnnn.nnnn<br /><br />Esempio: 1234.5678|Un valore maggiore di 1 o minore di 0 viene convertito in 1. Ad esempio, i valori 123,45 e -123.45 vengono convertiti in 1.|  
  
### <a name="decimal-data-type"></a>decimal - tipo di dati  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **decimale** (*p, s*). Le regole di conversione dei dati sono identico a quello di SQL Server. Per altre informazioni, vedere [conversione del tipo di dati](../t-sql/data-types/data-type-conversion-database-engine.md) su MSDN.  
  
|Tipo di valore letterale|Formato|  
|----------------|----------|  
|Valore letterale stringa nel **integer** formato|'nnnnnnnnnnnn'<br /><br />Esempio: '321312313123'|  
|Valore letterale stringa nel **decimale** formato|'nnnnnn.nnnnn'<br /><br />Esempio: '123344.34455'|  
|Valore letterale integer|nnnnnnnnnnnn<br /><br />Esempio: 321312313123|  
|Valore letterale decimale|nnnnnn.nnnnn<br /><br />Esempio: '123344.34455'|  
  
### <a name="float-and-real-data-types"></a>tipi di dati float e real  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **float** oppure **reale**. Le regole di conversione dei dati sono identico a quello di SQL Server. Per altre informazioni, vedere [conversione del tipo di dati](../t-sql/data-types/data-type-conversion-database-engine.md) su MSDN.  
  
|Tipo di valore letterale|Formato|  
|----------------|----------|  
|Valore letterale stringa nel **integer** formato|'nnnnnnnnnnnn'<br /><br />Esempio: '321312313123'|  
|Valore letterale stringa nel **decimale** formato|'nnnnnn.nnnnn'<br /><br />Esempio: '123344.34455'|  
|Valore letterale stringa nel **a virgola mobile** formato|'n.nnnnnE+nn'<br /><br />Esempio: '3.12323E + 14'|  
|Valore letterale integer|nnnnnnnnnnnn<br /><br />Esempio: 321312313123|  
|Valore letterale decimale|nnnnnn.nnnnn<br /><br />Esempio: 123344.34455|  
|Valore letterale mobile punto|n.nnnnnE+nn<br /><br />Esempio: 3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint i tipi di dati  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **int**, **bigint**, **tinyint**, oppure **smallint**. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **tinyint** è compreso tra 0 e 255 e l'intervallo per **int** è compreso tra -2.147.483.648 e 2.147.483.647.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|------------|------|----------------|
|Valore letterale stringa nel **integer** formato|'nnnnnnnnnnnnnn'<br /><br />Esempio: '321312313123'| None |  
|Valore letterale integer|nnnnnnnnnnnnnn<br /><br />Esempio: 321312313123| None|  
|Valore letterale decimale|nnnnnn.nnnnn<br /><br />Esempio: 123344.34455|I valori a destra del separatore decimale vengono troncati.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipi di dati Money e smallmoney  
Valori letterali di tipo Money vengono rappresentati come numeri con un separatore decimale facoltativo e il simbolo di valuta come prefisso. L'origine dati non può superare l'intervallo consentito per il tipo di dati specificato. Ad esempio, l'intervallo per **smallmoney** è-214.748,3648 e 214.748,3647 e l'intervallo per **denaro** è-922.337.203.685.477,5808 e 922.337.203.685.477,5807. Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **denaro** oppure **smallmoney**.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa nel **integer** formato|'nnnnnnnn'<br /><br />Esempio: '123433'|Le cifre mancante dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale '12345' viene inserito come 12345.0000.|  
|Valore letterale stringa nel **decimale** formato|'nnnnnn.nnnnn'<br /><br />Esempio: '123344.34455'|Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore '123344.34455' viene inserito come 123344.3446.|  
|Valore letterale stringa nel **denaro** formato|'$nnnnnn.nnnn'<br /><br />Esempio: '$123456.7890'|Il simbolo di valuta facoltativo non viene inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino.|  
|Valore letterale integer|nnnnnnnn<br /><br />Esempio: 123433|Le cifre mancante dopo il separatore decimale vengono impostate su 0 quando viene inserito il valore. Ad esempio, il valore letterale 12345 viene inserito come 12345.0000.|  
|Valore letterale decimale|nnnnnn.nnnnn<br /><br />Esempio: 123344.34455|Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123344.34455 viene inserito come 123344.3446.|  
|Valore letterale Money|$nnnnnn.nnnn<br /><br />Esempio: $123456.7890|Il simbolo di valuta facoltativo non viene inserito con il valore.<br /><br />Se il numero di cifre dopo il separatore decimale è superiore a 4, il valore viene arrotondato per eccesso al valore più vicino.|  
  
## <a name="InsertLiteralsString"></a>Inserimento di valori letterali in tipi di stringa  
Nelle tabelle seguenti definiscono i formati accettati e le regole di conversione per l'inserimento di un valore letterale in una colonna di SQL Server PDW che utilizza un tipo stringa.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipi di dati char, varchar, nchar e nvarchar  
Nella tabella seguente definisce i formati accettati e le regole per l'inserimento di valori letterali in una colonna di distribuzione di tipo **char**, **varchar**, **nchar** e**nvarchar**. La lunghezza di origine dei dati non può superare le dimensioni specificate per il tipo di dati. Se la lunghezza di origine dati è inferiore alle dimensioni dei **char** oppure **nchar** tipo di dati, i dati vengano applicato un riempimento a destra con spazi vuoti per raggiungere le dimensioni di tipo di dati.  
  
|Tipo di valore letterale|Formato|Regole di conversione|  
|----------------|----------|--------------------|  
|Valore letterale stringa|Formato: "carattere stringa'<br /><br />Esempio: 'abc'| None|  
|Valore letterale stringa Unicode|Formato: Stringa N'character'<br /><br />Esempio: N'abc'|  None |  
|Valore letterale integer|Formato: nnnnnnnnnnn<br /><br />Esempio: 321312313123| None |  
|Valore letterale decimale|Formato: nnnnnn.nnnnnnn<br /><br />Esempio: 12344.34455| None |  
|Valore letterale Money|Formato: $nnnnnn.nnnnn<br /><br />Esempio: $123456.99|Il simbolo di valuta non verrà inserito con il valore. Per inserire il simbolo di valuta, inserire il valore come valore letterale stringa. Questo corrisponde il formato del **dwloader** strumento che considera ogni valore letterale come valore letterale stringa.<br /><br />Le virgole non sono consentite.<br /><br />Se il numero di cifre dopo il separatore decimale è superiore a 2, il valore viene arrotondato per eccesso al valore più vicino. Ad esempio, il valore 123.946789 viene inserito come 123.95.<br /><br />Quando si usa la funzione CONVERT per inserire valori letterali di denaro, è consentito solo lo stile predefinito 0 (Nessun separatore delle migliaia e 2 cifre dopo il separatore decimale).|  

  
## <a name="see-also"></a>Vedere anche  
 
[Dati distribuiti](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
