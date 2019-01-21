---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7854b2419b3644c2f3c76cd96cccc06bfae2902
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299618"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Condividi il feedback sul sommario della documentazione SQL](https://aka.ms/sqldocsurvey)

Rimuove il carattere spazio `char(32)` o altri caratteri specificati dall'inizio o dalla fine di una stringa.  
 
## <a name="syntax"></a>Sintassi   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[ BOTH | LEADING | TRAILING ] non ancora disponibile."

## <a name="arguments"></a>Argomenti   

caratteri   
Valore letterale, variabile o chiamata di funzione di qualsiasi tipo di carattere non LOB (`nvarchar`, `varchar`, `nchar` o `char`) contenente i caratteri che devono essere rimossi. I tipi `nvarchar(max)` e `varchar(max)` non sono consentiti.

string   
Espressione di qualsiasi tipo di carattere (`nvarchar`, `varchar`, `nchar` o `char`) in cui è necessario rimuovere caratteri.

## <a name="return-types"></a>Tipi restituiti   
Restituisce un'espressione carattere con un tipo di argomento stringa in cui il carattere spazio `char(32)` o altri caratteri specificati vengono rimossi a entrambe le estremità. Restituisce `NULL` se la stringa di input è `NULL`.

## <a name="remarks"></a>Remarks   
Per impostazione predefinita la funzione `TRIM` rimuove il carattere spazio `char(32)` a entrambe le estremità che equivale a `LTRIM(RTRIM(@string))`. Il comportamento della funzione `TRIM ` con i caratteri specificati è identico al comportamento della funzione `REPLACE` in cui i caratteri iniziali o finali sono sostituiti da stringhe vuote.


## <a name="examples"></a>Esempi
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Rimuove il carattere spazio a entrambe le estremità della stringa   
L'esempio seguente rimuove gli spazi prima e dopo la parola `test`.   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>b.  Rimuove i caratteri specificati a entrambe le estremità della stringa   
L'esempio seguente rimuove un punto finale e spazi finali.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>Vedere anche
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
