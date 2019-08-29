---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 9b7ce2b7a9374579255974ae110f4d9167fc8fa8
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123198"
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Restituisce un valore formattato con il formato specificato e impostazioni cultura facoltative. Utilizzare la funzione FORMAT per formattare in base alle impostazioni locali i valori numerici e di data/ora come stringhe. Per le conversioni di tipi di dati generali, utilizzare CAST o CONVERT.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argomenti

 *Valore*  
 Espressione di un tipo di dati supportato da formattare. Per un elenco di tipi validi, vedere la tabella nella sezione Osservazioni indicata di seguito.  
  
 *format*  
 Schema di formattazione **nvarchar**.  
  
 L'argomento *format* deve contenere una stringa di formato .NET Framework valida, ovvero una stringa di formato standard (ad esempio "C" o "D") o uno schema di caratteri personalizzati per date e valori numerici (ad esempio "MMMM GG, aaaa (gggg)"). La formattazione composta non è supportata. Per una spiegazione completa di questi schemi di formattazione, vedere la documentazione di .NET Framework sulla formattazione di stringhe in formati di data e ora generali e personalizzati e in formati di numero personalizzati. È consigliabile iniziare con l'argomento "[Formattazione di tipi](https://go.microsoft.com/fwlink/?LinkId=211776)."  
  
 *culture*  
 Argomento **nvarchar** facoltativo che specifica le impostazioni cultura.  
  
 Se l'argomento *culture* non è specificato, viene usata la lingua della sessione corrente. Tale lingua viene impostata in modo implicito o in modo esplicito tramite l'istruzione SET LANGUAGE. *culture* accetta come argomento qualsiasi impostazione cultura supportata da .NET Framework e non è limitato alle lingue supportate in modo esplicito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'argomento *culture* non è valido, FORMAT genera un errore.  
  
## <a name="return-types"></a>Tipi restituiti

 **nvarchar** o Null  
  
 La lunghezza del valore restituito viene determinata da *format*.  
  
## <a name="remarks"></a>Remarks

 FORMAT restituisce Null per errori diversi da un valore di *culture* non *valido*. Ad esempio, viene restituito Null se il valore specificato in *format* non è valido.  

 La funzione FORMAT è di tipo non deterministico.
  
 FORMAT è basato sulla presenza di CLR (Common Language Runtime) di .NET Framework.  
  
 Questa funzione non può essere eseguita in modalità remota poiché dipende dalla presenza di CLR. L'esecuzione in modalità remota di una funzione che richiede CLR potrebbe provocare un errore sul server remoto.  
  
 FORMAT si basa sulle regole di formattazione di CLR, che indicano che i due punti e le virgole devono essere preceduti dal carattere di escape. Di conseguenza, quando la stringa di formato (secondo parametro) contiene un carattere due punti o virgola, tale carattere deve essere preceduto dalla barra rovesciata quando un valore di input (il primo parametro) è del tipo di dati **time**. Vedere [D. FORMAT con tipi di dati ora](#ExampleD).  
  
 Nella tabella seguente vengono elencati i tipi di dati accettabili per l'argomento *value*, insieme con i tipi equivalenti di mapping per .NET Framework.  
  
|Category|Tipo|Tipo .NET|  
|--------------|----------|---------------|  
|Numeric|BIGINT|Int64|  
|Numeric|INT|Int32|  
|Numeric|SMALLINT|Int16|  
|Numeric|TINYINT|Byte|  
|Numeric|Decimal|SqlDecimal|  
|Numeric|NUMERIC|SqlDecimal|  
|Numeric|FLOAT|Double|  
|Numeric|REAL|Single|  
|Numeric|SMALLMONEY|Decimal|  
|Numeric|money|Decimal|  
|Data e ora|Data|DateTime|  
|Data e ora|time|TimeSpan|  
|Data e ora|DATETIME|DateTime|  
|Data e ora|smalldatetime|DateTime|  
|Data e ora|datetime2|DateTime|  
|Data e ora|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-simple-format-example"></a>A. Esempio semplice di FORMAT

 Nell'esempio seguente viene restituita una data semplice nel formato per impostazioni cultura diverse.  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. FORMAT con stringhe di formattazione personalizzate

 Nell'esempio seguente vengono illustrati i valori numerici di formattazione specificando un formato personalizzato. Nell'esempio si presuppone che la data corrente sia il 27 settembre 2012. Per altre informazioni su questi e altri formati personalizzati, vedere [Stringhe di formato numerico personalizzato](https://msdn.microsoft.com/library/0c899ak8.aspx).  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. FORMAT con tipi numerici

 Nell'esempio seguente vengono restituite 5 righe della tabella **Sales.CurrencyRate** del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. La colonna **EndOfDateRate** viene archiviata come tipo **money** nella tabella. In questo esempio, la colonna viene restituita senza formattazione e viene quindi formattata specificando i tipi di formato di numero, valuta e generico di .NET. Per altre informazioni su questi e altri formati numerici, vedere [Stringhe di formato numerico standard](https://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 In questo esempio vengono specificate le impostazioni cultura tedesche (de-de).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
### <a name="ExampleD"></a> D. D. FORMAT con tipi di dati ora

 FORMAT restituisce Null in questi casi, perché `.` e `:` non sono preceduti dal carattere di escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format restituisce una stringa formattata in quanto `.` e `:` sono preceduti dal carattere di escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  

Format restituisce un'ora corrente formattata con l'indicazione AM o PM

```sql
SELECT FORMAT(SYSDATETIME(), N'hh:mm tt'); -- returns 03:46 PM
SELECT FORMAT(SYSDATETIME(), N'hh:mm t'); -- returns 03:46 P
```

Format restituisce l'ora specificata, con AM

```sql
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm tt') -- returns 01:00 AM
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm t')  -- returns 01:00 A
```

Format restituisce l'ora specificata, con PM

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm tt') -- returns 02:00 PM
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm t') -- returns 02:00 P
```
  
Format restituisce l'ora specificata nel formato 24 ore

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'HH:mm') -- returns 14:00
```
  
## <a name="see-also"></a>Vedere anche

 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
