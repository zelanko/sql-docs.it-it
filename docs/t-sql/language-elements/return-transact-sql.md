---
title: RETURN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs:
- TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e16193e0bf6a9596a17f767b157fc825ff3e0a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68072375"
---
# <a name="return-transact-sql"></a>RETURN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esce senza condizioni da una query o da una procedura. RETURN è un'istruzione immediata e completa e può essere utilizzata in qualsiasi momento per uscire da una procedura, un batch o un blocco di istruzioni. Le istruzioni che seguono RETURN non vengono eseguite.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression*  
 Valore intero restituito. Le stored procedure possono restituire un valore intero a una procedura o applicazione chiamante.  
  
## <a name="return-types"></a>Tipi restituiti  
 Restituisce facoltativamente **int**.  
  
> [!NOTE]  
>  Se non indicato diversamente, tutte le stored procedure di sistema restituiscono il valore 0 ad indicare l'esito positivo e un valore diverso da zero per indicare l'errore.  
  
## <a name="remarks"></a>Osservazioni  
 Quando viene utilizzata con una stored procedure, l'istruzione RETURN non può restituire un valore Null. Se una procedura tenta di restituire un valore Null, ad esempio quando si utilizza RETURN @status e il parametro @status è NULL, viene visualizzato un messaggio di avviso e restituito il valore 0.  
  
 Il valore di stato restituito può essere incluso in istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] successive nel batch o nella procedura che ha eseguito la procedura corrente, ma deve essere immesso nel formato seguente: `EXECUTE @return_status = <procedure_name>`.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-from-a-procedure"></a>R. Uscita da una procedura  
 Nell'esempio seguente viene illustrato come utilizzare `findjobs` per uscire da una procedura dopo la visualizzazione di un messaggio all'utente, se viene omesso il parametro del nome utente durante l'esecuzione di `RETURN`. Se il nome utente viene specificato, i nomi di tutti gli oggetti creati dall'utente nel database corrente vengono recuperati dalle tabelle di sistema appropriate.  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>B. Restituzione di codici di stato  
 Nell'esempio seguente viene controllato lo stato dell'ID di un contatto specificato. Se lo stato è Washington (`WA`), viene restituito il codice di stato `1`. In tutti gli altri casi viene restituito `2`, ad esempio quando il valore di `WA` è diverso da `StateProvince` oppure un valore `ContactID` non corrisponde a una riga.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 Negli esempi seguenti viene illustrato lo stato restituito dall'esecuzione di `checkstate`. Nel primo esempio viene illustrato il caso di un contatto di Washington, nel secondo il caso di un contatto che non risiede a Washington e nel terzo il caso di un contatto non valido. Per poter utilizzare la variabile locale `@return_status`, è prima necessario dichiararla.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 Rieseguire la query, specificando un numero di contatto diverso.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 Rieseguire la query, specificando un altro numero di contatto.  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  
