---
title: Implementazione dell'operatore OR operatore in Natively Compiled Stored Procedures | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64de082cd12c967f3f3c90ca3cb99c51985ed41a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62778912"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>Implementazione dell'operatore OR in stored procedure compilate in modalità nativa
  Gli operatori OR non sono supportati nei predicati di query in stored procedure compilate in modo nativo. Dal momento che anche gli operatori NOT non sono supportati nei predicati di query in stored procedure compilate in modo nativo, gli effetti degli operatori OR non possono essere simulati da soli tramite l'utilizzo degli operatori logici equivalenti. Tuttavia, gli effetti di un operatore OR possono essere simulati con variabili di tabella ottimizzata per la memoria.  
  
## <a name="or-operator-in-where-clause"></a>Operatore OR nella clausola WHERE  
 Se si dispone di un operatore OR in una clausola WHERE, è possibile utilizzare l'approccio seguente per simularne il comportamento:  
  
1.  Creare una variabile di tabella ottimizzata per la memoria con lo schema appropriato. Per questa operazione è necessario un tipo di tabella ottimizzata per la memoria predefinito.  
  
2.  A partire dall'operatore OR di livello principale, separare la clausola WHERE in due parti in base ai predicati uniti dall'operatore OR. Se si dispone di più operatori OR nella clausola WHERE, potrebbe essere necessario eseguire questa operazione più volte. Ripetere questo passaggio finché non rimane alcun operatore OR. Ad esempio, se si dispone del predicato seguente:  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     Dopo questo passaggio, si dovrebbe disporre dei predicati seguenti:  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  Eseguire una query con ognuna delle due parti presenti nel Passaggio 2 come predicato. Incollare il risultato di ogni query nella variabile di tabella ottimizzata per la memoria creata nel Passaggio 1.  
  
4.  Se necessario, rimuovere i duplicati dalla variabile di tabella ottimizzata per la memoria.  
  
5.  Utilizzare il contenuto della variabile di tabella ottimizzata per la memoria come risultato della query.  
  
 Nell'esempio seguente vengono utilizzate tabelle del database AdventureWorks2012 aggiornate per [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Per scaricare i file per questo esempio, goto [database AdventureWorks - 2012, 2008R2 e 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587). Per applicare [!INCLUDE[hek_2](../includes/hek-2-md.md)] codice di esempio per AdventureWorks2012, andare a [esempio di OLTP In memoria di SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Aggiungere la seguente stored procedure al database. Questa stored procedure verrà convertita per utilizzare la compilazione nativa.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 Dopo la conversione, lo schema della stored procedure e della tabella sarà il seguente:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>Operatore OR nella condizione JOIN  
 Se si dispone di un operatore OR in una condizione JOIN di un'istruzione SELECT, è possibile utilizzare l'approccio seguente per simularne il comportamento. Se si dispone di più operatori OR in una condizione JOIN o di più condizioni JOIN con operatori OR, potrebbe essere necessario eseguire questa operazione più volte.  
  
 Se si dispone di condizioni OUTER JOIN, è possibile combinare questa soluzione alternativa con quella per le condizioni OUTER JOIN.  
  
1.  Creare una variabile di tabella ottimizzata per la memoria con lo schema appropriato. Per questa operazione è necessario un tipo di tabella ottimizzata per la memoria predefinito.  
  
2.  Separare il predicato nella condizione JOIN in due parti in base ai predicati uniti dall'operatore OR. Se si dispone di più condizioni JOIN, potrebbe essere necessario eseguire questa operazione per ogni condizione JOIN, quindi creare un set di combinazioni dei frammenti risultanti. Ad esempio, se si dispone di tre condizioni JOIN con un operatore OR in ogni condizione JOIN, si potrebbe disporre di 2x2x2=8 predicati.  
  
3.  Per ogni predicato prodotto dal Passaggio 2, creare una query tramite cui verrà inserito il relativo risultato nella variabile di tabella ottimizzata per la memoria creata nel Passaggio 1.  
  
4.  Se necessario, rimuovere i duplicati dalla variabile di tabella ottimizzata per la memoria.  
  
5.  Utilizzare il contenuto della variabile di tabella ottimizzata per la memoria come risultato della query.  
  
 Nell'esempio seguente vengono utilizzate tabelle del database AdventureWorks2012 aggiornate per [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Per scaricare i file per questo esempio, goto [database AdventureWorks - 2012, 2008R2 e 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587). Per applicare [!INCLUDE[hek_2](../includes/hek-2-md.md)] codice di esempio per AdventureWorks2012, andare a [esempio di OLTP In memoria di SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Aggiungere la seguente stored procedure al database. Questa stored procedure verrà convertita per utilizzare la compilazione nativa. In questo esempio vengono utilizzate le condizioni INNER JOIN.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 Dopo la conversione, lo schema della stored procedure e della tabella sarà il seguente:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>Effetti collaterali  
 Se si dispone di più operatori OR nella clausola WHERE o nella condizione JOIN, il numero di query necessario per eseguire la simulazione del comportamento può aumentare in modo esponenziale. Ciò può rallentare le prestazioni delle query e aumentare l'utilizzo della memoria a causa della necessità di utilizzare variabili di tabella ottimizzata per la memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
