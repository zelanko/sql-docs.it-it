---
title: '[^] (carattere jolly per la mancata corrispondenza dei caratteri) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
author: rothja
ms.author: jroth
ms.openlocfilehash: eedf1db97477788489dd9b7c9c1789804ca064a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086095"
---
# <a name="-wildcard---characters-not-to-match-transact-sql"></a>\[^\] (carattere jolly per la mancata corrispondenza dei caratteri) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Corrisponde a un qualsiasi singolo carattere non compreso nell'intervallo o nel set specificato tra le parentesi quadre.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato l'operatore [^] per individuare tutte le persone nella tabella `Contact` il cui nome inizia con `Al` e non contiene la lettera `a` come terzo carattere.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [% &#40;caratteri jolly per la corrispondenza&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; &#40;caratteri jolly per la corrispondenza&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [\_ &#40;carattere jolly per corrispondenze di singoli caratteri&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  
