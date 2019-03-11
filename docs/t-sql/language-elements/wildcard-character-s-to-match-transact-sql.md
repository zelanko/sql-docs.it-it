---
title: '[ ] (Caratteri jolly per la corrispondenza) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4620f38c01f1bd7c4158387a607da12fbb95b865
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425816"
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \] (Caratteri jolly per la corrispondenza) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Rileva la corrispondenza con uno dei caratteri inclusi nell'intervallo o set racchiuso tra parentesi quadre `[ ]`. È possibile usare i caratteri jolly nei confronti di stringhe che prevedono l'uso di criteri di ricerca, ad esempio `LIKE` e `PATINDEX`.  
  
## <a name="examples"></a>Esempi  
### <a name="a-simple-example"></a>A: Esempio semplice   
L'esempio seguente restituisce i nomi che iniziano con la lettera `m`. `[n-z]` specifica che la seconda lettera deve essere inclusa nell'intervallo tra `n` e `z`. Il carattere jolly percentuale `%` indica che il terzo carattere può essere qualsiasi o nessuno. I database `model` e `msdb` soddisfano questi criteri. Il database `master` non soddisfa i criteri e viene escluso dal set di risultati.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 È possibile che siano installati altri database che soddisfano i criteri.


### <a name="b-more-complex-example"></a>B: Esempio più complesso   
 Nell'esempio seguente viene utilizzato l'operatore [] per trovare gli ID e i nomi di tutti i dipendenti inclusi in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] il cui indirizzo è associato a un C.A.P. a quattro cifre.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 Di seguito viene indicato il set di risultati:  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>Vedere anche  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40;Wildcard - Character&#40;s&#41; to Match&#41; (Carattere jolly - Corrispondente/i a) &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; &#40;Wildcard - Character&#40;s&#41; Not to Match&#41; (Carattere jolly - Non corrispondente/i a) &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_ &#40;Carattere jolly per corrispondenze di singoli caratteri&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
