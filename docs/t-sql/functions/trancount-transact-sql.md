---
title: '@@TRANCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 142762514f9bdbd7c7984dff218e5ea665d1d4d4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "73843312"
---
# <a name="x40x40trancount-transact-sql"></a>&#x40;&#x40;TRANCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce il numero di istruzioni BEGIN TRANSACTION che si sono verificate nella connessione corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **integer**  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione BEGIN TRANSACTION incrementa @@TRANCOUNT di 1. L'istruzione ROLLBACK TRANSACTION decrementa @@TRANCOUNT fino al valore 0, tranne nel caso dell'istruzione ROLLBACK TRANSACTION *savepoint_name* che non ha alcun effetto su @@TRANCOUNT. L'istruzione COMMIT TRANSACTION o COMMIT WORK decrementa @@TRANCOUNT di 1.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>R. Effetti delle istruzioni BEGIN e COMMIT  
 Nell'esempio seguente vengono illustrati gli effetti delle istruzioni nidificate `BEGIN` e `COMMIT` sulla variabile `@@TRANCOUNT`.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>B. Effetti delle istruzioni BEGIN e ROLLBACK  
 Nell'esempio seguente vengono illustrati gli effetti delle istruzioni nidificate `BEGIN TRAN` e `ROLLBACK` sulla variabile `@@TRANCOUNT`.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
