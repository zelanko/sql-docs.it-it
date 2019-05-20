---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9dc713f54c9383b240a392304c5c938cdea210b1
ms.sourcegitcommit: 179ab0e55f918f58a18c43af076130f4ac3decd6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875216"
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce la posizione di inizio della prima occorrenza di un modello in un'espressione specificata, oppure zero se il modello non viene trovato, in tutti i dati di tipo carattere e testo validi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *pattern*  
 Espressione di caratteri che contiene la sequenza da cercare. È possibile usare i caratteri jolly. Il carattere %, tuttavia, deve precedere e seguire *pattern*, tranne nelle ricerche del primo o dell'ultimo carattere. *pattern* è un'espressione appartenente alla categoria di tipi di dati per stringhe di caratteri. La lunghezza massima di *pattern* è 8000 caratteri.  
  
 *expression*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) che in genere indica una colonna in cui viene cercato il modello specificato. *expression* appartiene alla categoria di tipi di dati per stringhe di caratteri.  
  
## <a name="return-types"></a>Tipi restituiti  
 **bigint** se *expression* è del tipo di dati **varchar(max)** o **nvarchar(max)**, in caso contrario **int**.  
  
## <a name="remarks"></a>Remarks  
 Se *pattern* o *expression* è NULL, PATINDEX restituisce NULL.  
 
 La posizione di inizio restituita è in base 1 e non in base 0.
 
 L'istruzione PATINDEX consente di eseguire i confronti in base alle regole di confronto dell'input. Per eseguire un confronto in base a regole di confronto specifiche, è possibile utilizzare COLLATE per applicare regole di confronto esplicite all'input.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caratteri supplementari (coppie di surrogati)  
 Quando si usano le regole di confronto SC, qualsiasi coppia di surrogati UTF-16 nel parametro *expression* viene considerata come un singolo carattere dal valore restituito. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 0x0000 (**char(0)**) è un carattere non definito nelle regole di confronto di Windows e non può essere incluso in PATINDEX.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-simple-patindex-example"></a>A. Esempio semplice di PATINDEX  
 L'esempio seguente verifica in una stringa di caratteri breve (`interesting data`) la posizione iniziale dei caratteri `ter`.  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Utilizzo di un modello con PATINDEX  
 Nell'esempio seguente viene individuata la posizione in cui il modello `ensure` ha inizio in una riga specifica della colonna `DocumentSummary` nella tabella `Document` del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 Se non si imposta una limitazione per le righe in cui eseguire la ricerca tramite la clausola `WHERE`, la query restituisce tutte le righe della tabella, indicando valori diversi da zero per le righe in cui il modello è stato trovato e zero per tutte le righe in cui la ricerca ha avuto esito negativo.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Utilizzo di caratteri jolly con PATINDEX  
 Nell'esempio seguente vengono utilizzati i caratteri jolly % e _ per individuare la posizione iniziale del modello `'en'`, seguito da un carattere qualsiasi e `'ure'` nella stringa specificata (l'indice comincia col valore 1):  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 Il funzionamento di `PATINDEX` è uguale a quello di `LIKE`, pertanto è possibile utilizzare qualsiasi carattere jolly. Non è necessario racchiudere il modello tra percentuali. `PATINDEX('a%', 'abc')` restituisce 1 e `PATINDEX('%a', 'cba')` restituisce 3.  
  
 A differenza di `LIKE`, `PATINDEX` restituisce una posizione, analogamente a `CHARINDEX`.  
  
### <a name="d-using-collate-with-patindex"></a>D. Utilizzo di COLLATE con PATINDEX  
 Nell'esempio seguente viene utilizzata la funzione `COLLATE` per specificare in modo esplicito le regole di confronto dell'espressione indicante il contesto della ricerca.  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. Utilizzo di una variabile per specificare il modello  
 L'esempio usa una variabile per passare un valore al parametro *pattern*. In questo esempio viene usato il database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>Vedere anche  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; (Carattere jolly - Corrispondente/i) &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; (Carattere jolly - Non corrispondente/i) &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;Carattere jolly per corrispondenze di singoli caratteri&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [Carattere di percentuale &#40;Caratteri jolly per la corrispondenza&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


