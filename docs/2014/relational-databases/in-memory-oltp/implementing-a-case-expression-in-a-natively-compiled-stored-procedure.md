---
title: Implementazione di un'istruzione CASE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f034eaea1faeb1547a3697bec4dab50090864d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157942"
---
# <a name="implementing-a-case-statement"></a>Implementazione di un'istruzione CASE
  Le istruzioni CASE non sono supportate nelle stored procedure compilate in modo nativo. Nell'esempio seguente viene illustrata una modalità per implementare la funzionalità di un'istruzione CASE in una stored procedure compilata in modo nativo.  
  
 Negli esempi viene utilizzata una variabile di tabella per costruire un unico set di risultati, vale a dire l'unico appropriato per l'elaborazione di un numero limitato di righe in quanto comporta la creazione di una copia aggiuntiva delle righe di dati.  
  
 È necessario eseguire il test delle prestazioni di questa soluzione alternativa, per assicurarsi che venga eseguita come previsto nell'applicazione.  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
