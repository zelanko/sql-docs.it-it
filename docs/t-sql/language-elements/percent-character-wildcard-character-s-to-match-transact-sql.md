---
title: Carattere di percentuale (carattere jolly) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
ms.openlocfilehash: af956b153aadc660de4a0b440bc07467888e136b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121856"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>Carattere di percentuale (carattere jolly) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Corrisponde a qualsiasi stringa composta da zero o più caratteri. Questo carattere jolly può essere utilizzato come prefisso o suffisso.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i nomi delle persone elencate nella tabella `Person` del database `AdventureWorks2012` che iniziano con `Dan`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Espressioni &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (carattere jolly)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93; (carattere jolly per la mancata corrispondenza)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (carattere jolly per corrispondenze di singoli caratteri)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
