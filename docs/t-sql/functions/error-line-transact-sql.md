---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 569486f5806ac6f0d62f32fa9ac17efc1d43a85a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67904376"
---
# <a name="error_line-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Questa funzione restituisce il numero di riga dell'occorrenza di un errore che ha causato l'esecuzione del blocco CATCH di un costrutto TRY...CATCH.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>Tipo restituito  
**int**  
  
## <a name="return-value"></a>Valore restituito  
Quando chiamata in un blocco CATCH, `ERROR_LINE` restituisce  
  
-   Numero di riga in cui si è verificato l'errore    
-   numero di riga in una routine, se l'errore si è verificato all'interno di una stored procedure o di un trigger  
-   NULL, se chiamata all'esterno dell'ambito di un blocco CATCH.  
  
## <a name="remarks"></a>Osservazioni  
Una chiamata a `ERROR_LINE` può verificarsi da un qualsiasi punto nell'ambito di un blocco CATCH.  
  
`ERROR_LINE` restituisce il numero di riga in cui si è verificato un errore, indipendentemente dalla posizione della chiamata a `ERROR_LINE` nell'ambito del blocco CATCH e dal numero di chiamate a `ERROR_LINE`. Questo tipo di comportamento è in contrasto con funzioni come @@ERROR. @@ERROR restituisce un numero di errore nell'istruzione immediatamente successiva a quella che ha provocato un errore o nella prima istruzione di un blocco CATCH.  
  
Nei blocchi CATCH nidificati `ERROR_LINE` restituisce il numero di riga dell'errore specifico dell'ambito del blocco CATCH che vi fa riferimento. Ad esempio, il blocco CATCH di un costrutto TRY...CATCH potrebbe contenere un costrutto TRY...CATCH nidificato. All'interno del blocco CATCH nidificato `ERROR_LINE` restituisce il numero di riga per l'errore che ha richiamato il blocco CATCH nidificato. Se `ERROR_LINE` viene eseguita nel blocco CATCH esterno, restituisce il numero di riga per l'errore che ha richiamato il blocco CATCH specifico.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-error_line-in-a-catch-block"></a>R. Utilizzo di ERROR_LINE in un blocco CATCH  
In questo esempio viene illustrata un'istruzione `SELECT` che genera un errore di divisione per zero. `ERROR_LINE` restituisce il numero di riga in cui si è verificato l'errore.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
Result 
-----------

(0 row(s) affected)

ErrorLine
-----------
4

(1 row(s) affected)
```  
  
### <a name="b-using-error_line-in-a-catch-block-with-a-stored-procedure"></a>B. Utilizzo di ERROR_LINE in un blocco CATCH con una stored procedure  
In questo esempio viene illustrata una stored procedure che genera un errore di divisione per zero. `ERROR_LINE` restituisce il numero di riga in cui si è verificato l'errore.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that  
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorLine
-----------
7

(1 row(s) affected)  
   
```

### <a name="c-using-error_line-in-a-catch-block-with-other-error-handling-tools"></a>C. Utilizzo di ERROR_LINE in un blocco CATCH con altri strumenti per la gestione degli errori  
In questo esempio viene illustrata un'istruzione `SELECT` che genera un errore di divisione per zero. `ERROR_LINE` restituisce il numero di riga in cui si è verificato l'errore e le informazioni relative all'errore stesso.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState ErrorProcedure ErrorLine ErrorMessage
----------- ------------- ---------- -------------- --------- ---------------------------------
8134        16            1          NULL           3         Divide by zero error encountered.

(1 row(s) affected)
  
```
  
## <a name="see-also"></a>Vedere anche  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
