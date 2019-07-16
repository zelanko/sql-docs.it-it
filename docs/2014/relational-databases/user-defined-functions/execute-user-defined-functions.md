---
title: Eseguire funzioni definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e9c170a187fc3ccf28301a2ee1c9ee7b626169f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196437"
---
# <a name="execute-user-defined-functions"></a>Eseguire funzioni definite dall'utente
  È possibile eseguire una funzione definita dall'utente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per eseguire definito dall'utente funziona, utilizzando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 In Transact-SQL è possibile specificare parametri tramite *valore* o*parameter_name*=*valore.* Un parametro non fa parte di una transazione. Se un parametro viene modificato in una transazione per la quale verrà eseguito il rollback, il valore del parametro non viene ripristinato al suo valore precedente. Il valore restituito al chiamante corrisponde sempre al valore specificato al termine del modulo.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per eseguire l'istruzione EXECUTE, non è necessario disporre di autorizzazioni specifiche. Sono tuttavia richieste autorizzazioni per le entità a protezione diretta a cui viene fatto riferimento all'interno della stringa EXECUTE. Se, ad esempio, la stringa include un'istruzione INSERT, il chiamante dell'istruzione EXECUTE deve disporre dell'autorizzazione INSERT per la tabella di destinazione. Le autorizzazioni vengono verificate non appena viene rilevata l'istruzione EXECUTE, anche se l'istruzione è inclusa in un modulo. Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-execute-a-user-defined-function"></a>Per eseguire una funzione definita dall'utente  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
  
