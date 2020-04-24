---
title: COMMIT WORK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMMIT_WORK_TSQL
- WORK_TSQL
- WORK
- COMMIT WORK
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- COMMIT WORK statement
ms.assetid: 4de76f33-399e-4912-a617-6eb6c560a058
author: rothja
ms.author: jroth
ms.openlocfilehash: 01199ad96dfc5ef34188e95afc3cd3707eaf57fb
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635816"
---
# <a name="commit-work-transact-sql"></a>COMMIT WORK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contrassegna il termine della transazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
  
COMMIT [ WORK ]  
[ ; ]  
```  
  
## <a name="remarks"></a>Osservazioni  
 Questa istruzione funziona esattamente come l'istruzione COMMIT TRANSACTION, ad eccezione del fatto che COMMIT TRANSACTION accetta un nome di transazione definito dall'utente. La sintassi di COMMIT, con o senza la parola chiave facoltativa WORK, è compatibile con SQL-92.  
  
## <a name="see-also"></a>Vedere anche  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
