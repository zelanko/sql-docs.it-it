---
description: Eseguire funzioni definite dall'utente
title: Eseguire funzioni definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc0904609ba680ae25c26e529fb49d328d310a77
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484393"
---
# <a name="execute-user-defined-functions"></a>Eseguire funzioni definite dall'utente
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Eseguire una funzione definita dall'utente con Transact-SQL.
  

> **Nota:** per altre informazioni, vedere l'argomento sulle  [funzioni definite dall'utente](user-defined-functions.md) e [Create Function (Transact SQL)](../../t-sql/statements/create-function-transact-sql.md) . 
  
 
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 In Transact-SQL è possibile specificare parametri tramite *valore* o *parameter_name*=*valore.* Un parametro non fa parte di una transazione. Se un parametro viene modificato in una transazione per la quale verrà eseguito il rollback, il valore del parametro non viene ripristinato al suo valore precedente. Il valore restituito al chiamante corrisponde sempre al valore specificato al termine del modulo.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
 Per eseguire l'istruzione [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) non sono necessarie autorizzazioni specifiche. Sono tuttavia **obbligatorie** autorizzazioni per le entità a protezione diretta a cui si fa riferimento all'interno della stringa EXECUTE. Se, ad esempio, la stringa include un'istruzione [INSERT](../../t-sql/statements/insert-transact-sql.md) , il chiamante dell'istruzione EXECUTE deve avere l'autorizzazione INSERT per la tabella di destinazione. Le autorizzazioni vengono verificate non appena viene rilevata l'istruzione EXECUTE, anche se l'istruzione è inclusa in un modulo. Per altre informazioni, vedere [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
### <a name="example"></a>Esempio 
  
Questo esempio usa la funzione a valori scalari `ufnGetSalesOrderStatusText` disponibile nella maggior parte delle edizioni di `AdventureWorks`.  Lo scopo della funzione è di restituire un valore di testo per lo stato delle vendite da un numero intero specificato.  Modificare l'esempio passando i numeri interi da 1 a 7 al parametro **\@Status** .
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
