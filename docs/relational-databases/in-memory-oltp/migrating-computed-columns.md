---
title: Migrazione di colonne calcolate | Microsoft Docs
ms.custom: ''
ms.date: 12/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 36a0a6f82499a617a37b7cc9b848a33ec29c2ce3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68050135"
---
# <a name="migrating-computed-columns"></a>Migrazione di colonne calcolate

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Le colonne calcolate non sono supportate nelle tabelle ottimizzate per la memoria. Tuttavia, è possibile simulare una colonna calcolata.

A partire da [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], le colonne calcolate sono supportate in indici e tabelle ottimizzate per la memoria.

Valutare la necessità di rendere persistenti le colonne calcolate quando si esegue la migrazione delle tabelle basate su disco nelle tabelle ottimizzate per la memoria. Le diverse caratteristiche di prestazioni delle tabelle ottimizzate per la memoria e delle stored procedure compilate in modo nativo possono annullare la necessità della persistenza.  
  
## <a name="non-persisted-computed-columns"></a>Colonne calcolate non persistenti  
 Per simulare gli effetti di una colonna calcolata non persistente, creare una vista nella tabella ottimizzata per la memoria. Nell'istruzione SELECT che definisce la vista, aggiungere la definizione della colonna calcolata nella vista. Ad eccezione di una stored procedure compilata in modo nativo, le query che utilizzano i valori della colonna calcolata devono essere letti dalla vista. All'interno delle stored procedure compilate in modo nativo, è consigliabile aggiornare tutte le istruzioni SELECT, UPDATE o DELETE in base alla definizione della colonna calcolata.  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>Colonne calcolate persistenti  
 Per simulare gli effetti di una colonna calcolata persistente, creare una stored procedure per l'inserimento nella tabella e un'altra stored procedure per l'aggiornamento della tabella. Quando si inserisce o si aggiorna la tabella, chiamare le stored procedure per eseguire queste attività. All'interno delle stored procedure, calcolare il valore del campo calcolato in base agli input, analogamente al modo in cui viene definita la colonna calcolata nella tabella originale basata su disco. Quindi, inserire o aggiornare la tabella in base alle esigenze all'interno della stored procedure.  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  

CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  

DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  

DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
