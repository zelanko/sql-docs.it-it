---
title: Creazione di una tabella con ottimizzazione per la memoria e di una stored procedure compilata in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 48a9a0a3-930f-477b-bd0f-e82e77999ecc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f905e088d158803f26110356b1dad3cc29f62ab6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090392"
---
# <a name="creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure"></a>Creazione di una tabella con ottimizzazione per la memoria e di una stored procedure compilata in modo nativo

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento è incluso un esempio in cui viene illustrata la sintassi per OLTP in memoria.  

Per abilitare un'applicazione all'utilizzo di OLTP in memoria, è necessario completare le attività seguenti:  

-   Creare un filegroup di dati ottimizzato per la memoria e aggiungervi un contenitore.  
  
-   Creare tabelle e indici ottimizzati per la memoria. Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
-   Caricare i dati nella tabella ottimizzata per la memoria e aggiornare le statistiche dopo il caricamento dei dati e prima della creazione delle stored procedure compilate. Per altre informazioni, vedere [Statistiche per tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).  
  
-   Creare stored procedure compilate in modo nativo per l'accesso ai dati nelle tabelle ottimizzate per la memoria. Per altre informazioni, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). È inoltre possibile utilizzare codice [!INCLUDE[tsql](../../includes/tsql-md.md)] tradizionale e interpretato per accedere ai dati nelle tabelle ottimizzate per la memoria.  
  
-   In base alle esigenze, eseguire la migrazione dei dati dalle tabelle esistenti nelle tabelle ottimizzate per la memoria.  

## <a name="background-on-in-memory-objects"></a>Informazioni preliminari sugli oggetti in memoria

Per informazioni su come usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare tabelle ottimizzate per la memoria, vedere [Supporto di SQL Server Management Studio per OLTP in memoria](../../relational-databases/in-memory-oltp/sql-server-management-studio-support-for-in-memory-oltp.md).  

### <a name="natively-compiled-stored-procedures"></a>Stored procedure compilate in modo nativo

Le stored procedure compilate in modo nativo sono stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] compilate nel codice nativo e che accedono a tabelle ottimizzate per la memoria. Le stored procedure compilate in modo nativo consentono un'esecuzione efficiente delle query e della logica di business nella stored procedure. Per altri dettagli sul processo di compilazione nativa, vedere [Compilazione nativa di tabelle e stored procedure](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Per altre informazioni sulla migrazione delle stored procedure basate su disco alle stored procedure compilate in modo nativo, vedere [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).

> [!NOTE]
> Una differenza tra le stored procedure interpretate (basate su disco) e le stored procedure compilate in modo nativo è che una stored procedure interpretata viene compilata alla prima esecuzione, mentre una stored procedure compilata in modo nativo viene compilata quando viene creata. Con le stored procedure compilate in modo nativo, molte condizioni di errore (overflow aritmetico, conversione dei tipi e alcune condizioni di divisione per zero) possono essere rilevate in fase di creazione e impediscono la creazione della stored procedure compilata in modo nativo. Con le stored procedure interpretate, queste condizioni di errore in genere non causano un errore durante la creazione della stored procedure, ma tutte le esecuzioni non riescono.

## <a name="code-example-in-t-sql"></a>Esempio di codice in T-SQL

Nell'esempio di codice seguente è necessaria una directory denominata c:\Data\ .

```sql  
CREATE DATABASE imoltp   
GO  
  
--------------------------------------  
-- create database with a memory-optimized
-- filegroup and a container.

ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp ADD FILE (
    name='imoltp_mod1', filename='c:\data\imoltp_mod1')
    TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
GO  
  
USE imoltp  
GO  
  
-- Create a durable (data will be persisted) memory-optimized table
-- two of the columns are indexed.

CREATE TABLE dbo.ShoppingCart (   
    ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,  
    UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED
        HASH WITH (BUCKET_COUNT=1000000),
    CreatedDate DATETIME2 NOT NULL,   
    TotalPrice MONEY  
    ) WITH (MEMORY_OPTIMIZED=ON)   
GO  

-- Create a non-durable table. Data will not be persisted,
-- data loss if the server turns off unexpectedly.

CREATE TABLE dbo.UserSession (   
   SessionId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED
        HASH WITH (BUCKET_COUNT=400000),
   UserId int NOT NULL,   
   CreatedDate DATETIME2 NOT NULL,  
   ShoppingCartId INT,  
   INDEX ix_UserId NONCLUSTERED
        HASH (UserId) WITH (BUCKET_COUNT=400000)   
    )   
    WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY)
GO  
  
-- insert data into the tables  
INSERT dbo.UserSession VALUES (342, SYSDATETIME(), 4);
INSERT dbo.UserSession VALUES (65, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8798, SYSDATETIME(), 1)   
INSERT dbo.UserSession VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (4321, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8578, SYSDATETIME(), NULL)   
  
INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4)   
INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4)   
GO  
  
-- Verify table contents.

SELECT * FROM dbo.UserSession;
SELECT * FROM dbo.ShoppingCart;
GO  
  
-- Update statistics on memory-optimized tables;

UPDATE STATISTICS dbo.UserSession  WITH FULLSCAN, NORECOMPUTE;
UPDATE STATISTICS dbo.ShoppingCart WITH FULLSCAN, NORECOMPUTE;
GO  
  
-- in an explicit transaction, assign a cart to a session
-- and update the total price.
-- SELECT/UPDATE/DELETE statements in explicit transactions.

BEGIN TRAN;
   UPDATE dbo.UserSession SET ShoppingCartId=3 WHERE SessionId=4;
   UPDATE dbo.ShoppingCart SET TotalPrice=65.84 WHERE ShoppingCartId=3;
COMMIT;
GO   
  
-- Verify table contents.

SELECT *   
    FROM dbo.UserSession u
        JOIN dbo.ShoppingCart s on u.ShoppingCartId=s.ShoppingCartId
    WHERE u.SessionId=4;
 GO  
  
-- Natively compiled stored procedure for assigning
-- a shopping cart to a session.

CREATE PROCEDURE dbo.usp_AssignCart @SessionId int
    WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @UserId INT,  
          @ShoppingCartId INT;
  
  SELECT @UserId=UserId, @ShoppingCartId=ShoppingCartId
  FROM dbo.UserSession WHERE SessionId=@SessionId;
  
  IF @UserId IS NULL   
    THROW 51000, N'The session or shopping cart does not exist.', 1;
  
  UPDATE dbo.UserSession
    SET ShoppingCartId=@ShoppingCartId WHERE SessionId=@SessionId;
 END   
 GO  
  
 EXEC usp_AssignCart 1;
 GO  
  
-- natively compiled stored procedure for inserting
-- a large number of rows this demonstrates the
-- performance of native procs   
CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int
    WITH NATIVE_COMPILATION, SCHEMABINDING   
AS
BEGIN ATOMIC   
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @i int = 0;
  
  WHILE @i < @InsertCount   
  BEGIN   
    INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL)
    SET @i += 1   
  END  
  
END   
GO  
  
-- insert 1,000,000 rows   
 EXEC usp_InsertSampleCarts 1000000   
 GO  
  
---- verify the rows have been inserted   
 SELECT COUNT(*) FROM dbo.ShoppingCart   
 GO  
  
-- Sample memory-optimized tables for
-- sales orders and sales order details.
CREATE TABLE dbo.SalesOrders   
(  
   so_id INT NOT NULL PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATE NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED
        (so_date DESC, so_total DESC)  
) WITH (MEMORY_OPTIMIZED=ON);
GO  
  
CREATE TABLE dbo.SalesOrderDetails  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   CONSTRAINT PK_SOD PRIMARY KEY NONCLUSTERED
        (so_id,lineitem_id)
) WITH (MEMORY_OPTIMIZED=ON)  
GO  

-- Memory-optimized table type for collecting
-- sales order details.

CREATE TYPE dbo.SalesOrderDetailsType AS TABLE  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- stored procedure that inserts a sales order,
-- along with its details.

CREATE PROCEDURE dbo.InsertSalesOrder
    @so_id INT, @cust_id INT,
    @items dbo.SalesOrderDetailsType READONLY  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH   
(  
   TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
   LANGUAGE = N'us_english'  
)  
   DECLARE @total MONEY  
   SELECT @total = SUM(unitprice) FROM @items  

   INSERT dbo.SalesOrders
        VALUES (@so_id, @cust_id, getdate(), @total)

   INSERT dbo.SalesOrderDetails
        SELECT so_id, lineitem_id, product_id, unitprice
        FROM @items  
END  
GO  
  
-- Insert a sample sales order.
DECLARE @so_id INT = 18,  
       @cust_id INT = 8,  
       @items dbo.SalesOrderDetailsType;

INSERT @items  VALUES   
       (@so_id, 1, 4, 43),   
       (@so_id, 2, 3, 3),   
       (@so_id, 3, 8, 453),   
       (@so_id, 4, 5, 76),   
       (@so_id, 5, 4, 43);

EXEC dbo.InsertSalesOrder @so_id, @cust_id, @items;
GO  
  
-- verify the content of the tables  
SELECT   
       so.so_id,  
       so.so_date,  
       sod.lineitem_id,  
       sod.product_id,  
       sod.unitprice  
FROM dbo.SalesOrders so
    JOIN dbo.SalesOrderDetails sod on so.so_id=sod.so_id  
ORDER BY so.so_id, sod.lineitem_id  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di codice di OLTP in memoria](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)  
  
  
