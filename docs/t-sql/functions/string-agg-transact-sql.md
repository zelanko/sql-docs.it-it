---
title: STRING_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e368b005eaa1f5729f177356f3e06ea5effbd417
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947535"
---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena i valori delle espressioni della stringa e inserisce i valori dei separatori tra di essi. Il separatore non viene aggiunto alla fine della stringa.
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>Argomenti 
*expression*  
[Espressione](../../t-sql/language-elements/expressions-transact-sql.md) di qualsiasi tipo. Le espressioni vengono convertite in tipi `NVARCHAR` o `VARCHAR` durante la concatenazione. I tipi non stringa vengono convertiti nel tipo `NVARCHAR`.

*separator*  
È un'[espressione](../../t-sql/language-elements/expressions-transact-sql.md) di tipo `NVARCHAR` o `VARCHAR` usata come separatore per stringhe concatenate. Può essere un valore letterale o una variabile. 

<order_clause>   
Facoltativamente è possibile specificare l'ordine dei risultati concatenati mediante la clausola `WITHIN GROUP`:

```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  Elenco di [espressioni](../../t-sql/language-elements/expressions-transact-sql.md) non costanti che può essere usato per l'ordinamento dei risultati. È consentito un solo valore `order_by_expression` per query. Per impostazione predefinita, l'ordinamento è crescente.   
  

## <a name="return-types"></a>Tipi restituiti 

Il tipo restituito dipende dal primo argomento (espressione). Se l'argomento di input è di tipo stringa (`NVARCHAR`, `VARCHAR`), il tipo di risultato sarà uguale al tipo dell'input. Nella tabella seguente sono elencate le conversioni automatiche:  

|Tipo di espressione di input |Risultato | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1...4000) |NVARCHAR(4000) |
|VARCHAR(1...8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numeric, float, real, bit, decimal, smallmoney, money, datetime, datetime2, |NVARCHAR(4000) |


## <a name="remarks"></a>Remarks  
`STRING_AGG` è una funzione di aggregazione che accetta tutte le espressioni dalle righe e le concatena in una stringa singola. I valori delle espressioni vengono convertiti in modo implicito nei tipi di stringa e successivamente concatenati. Per la conversione implicita in stringhe vengono seguite le regole esistenti per le conversioni dei tipi di dati. Per altre informazioni sulle conversioni dei tipi di dati, vedere [CAST e CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Se l'espressione di input è di tipo `VARCHAR`, il separatore non può essere di tipo `NVARCHAR`. 

I valori Null vengono ignorati e il separatore corrispondente non viene aggiunto. Per restituire un segnaposto per i valori Null, usare la funzione `ISNULL` come illustrato nell'esempio B.

`STRING_AGG` è disponibile in qualsiasi livello di compatibilità.

## <a name="examples"></a>Esempi 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. Generare l'elenco di nomi separati in nuove righe 
Nell'esempio seguente viene generato un elenco di nomi in una cella di risultato singola, separati con ritorno a capo.
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

I valori `NULL` presenti nelle celle `name` non vengono restituiti nel risultato.   
> [!NOTE]  
>  Se si usa l'editor di query di Management Studio, l'opzione **Risultati in formato griglia** non può implementare il ritorno a capo. Passare a **Risultati in formato testo** per visualizzare il risultato impostato correttamente.   

### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. Generare l'elenco di nomi delimitati da virgola senza valori NULL   
Nell'esempio seguente i valori Null vengono sostituiti con "N/A" e i nomi delimitati da virgole vengono restituiti in una cella di risultato singola.  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Csv | 
|--- |
|John,N/A,Mike,Peter,N/A,N/A,Alice,Bob |  

### <a name="c-generate-comma-separated-values"></a>C. Generare valori delimitati da virgole 
```sql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|nomi | 
|--- |
|Davide Sánchez (8 febbraio 2003 12:00) <br />Terri Duffy (24 febbraio 2002 12:00) <br />Roberto Tamburello (5 dicembre 2001 12:00) <br />Rob Walters (29 dicembre 2001 12:00) <br />... |

> [!NOTE]  
>  Se si usa l'editor di query di Management Studio, l'opzione **Risultati in formato griglia** non può implementare il ritorno a capo. Passare a **Risultati in formato testo** per visualizzare il risultato impostato correttamente.   

### <a name="d-return-news-articles-with-related-tags"></a>D. Restituire articoli di giornale con tag correlati 
Gli articoli e i tag correlati vengono suddivisi in tabelle diverse. Lo sviluppatore vuole che venga restituita una riga per ogni articolo con tutti i tag associati. Usare la query seguente: 
```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |tags |
|--- |--- |--- |
|172 |I sondaggi indicano risultati delle elezioni molto vicini |politica, sondaggi, municipio | 
|176 |La nuova autostrada dovrebbe ridurre il traffico |NULL |
|177 |I cani continuano a essere preferiti ai gatti |sondaggi, animali| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. Generare un elenco di messaggi di posta elettronica per città
La query seguente consente di trovare gli indirizzi di posta elettronica dei dipendenti e di raggrupparli in base alla città: 
```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|città |messaggi di posta elettronica |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

I messaggi di posta elettronica restituiti nella colonna relativa possono essere usati per inviare messaggi di posta elettronica a un gruppo di persone che lavorano tutte nella stessa città. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. Generare un elenco di messaggi di posta elettronica ordinato per città   
La query seguente è simile alla precedente e consente di trovare gli indirizzi di posta elettronica dei dipendenti, di raggrupparli in base alla città e di metterli in ordine alfabetico:   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|città |messaggi di posta elettronica |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |

## <a name="see-also"></a>Vedere anche  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funzioni di aggregazione &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [Funzioni per i valori stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

