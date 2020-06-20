---
title: 'Dimostrazione: Miglioramento delle prestazioni di OLTP in memoria | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4858e4c35263ab3dd1d9fdcf55a2b136dd8eeaf2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050184"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Dimostrazione: Miglioramento delle prestazioni di OLTP in memoria
  Questo esempio mostra i miglioramenti delle prestazioni che si ottengono quando si utilizza OLTP in memoria, mettendo a confronto le differenze nei tempi di risposta per l'esecuzione di una query Transact-SQL identica su tabelle ottimizzate per la memoria e su tabelle basate su disco tradizionali. Viene anche creata una stored procedure compilata in modo nativo (basata sulla stessa query), che viene quindi eseguita per dimostrare che in genere si ottengono i tempi di risposta migliori eseguendo query su una tabella ottimizzata per la memoria con una stored procedure compilata in modo nativo. Questo esempio illustra solo un aspetto dei miglioramenti delle prestazioni in caso di accesso ai dati in tabelle ottimizzate per la memoria, ovvero l'efficienza dell'accesso ai dati durante l'esecuzione di inserimenti. Questo esempio è a thread singolo e non sfrutta i vantaggi della concorrenza di OLTP in memoria. Un carico di lavoro che utilizza la concorrenza avrà un miglioramento più significativo delle prestazioni.  
  
> [!NOTE]  
>  Un altro esempio che illustra le tabelle ottimizzate per la memoria è disponibile nell' [esempio di OLTP in memoria SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Per completare questo esempio, sarà necessario eseguire queste operazioni:  
  
1.  Creare un database denominato **imoltp** e modificare i dettagli del file per configurarlo per l'uso di OLTP in memoria.  
  
2.  Creare gli oggetti di database per l'esempio, ovvero tre tabelle e una stored procedure compilata in modo nativo.  
  
3.  Eseguire le diverse query e visualizzare i tempi di risposta per ognuna.  
  
 Per configurare il database **imoltp** per questo esempio, creare prima di tutto una cartella vuota: **c:\ imoltp_data**e quindi eseguire il codice seguente:  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 Eseguire successivamente il codice seguente per creare la tabella basata su disco, due (2) tabelle ottimizzate per la memoria e la stored procedure compilata in modo nativo da utilizzare per illustrare i diversi metodi di accesso ai dati:  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 L'impostazione è stata completata e si è pronti per eseguire le query che visualizzeranno i tempi di risposta confrontando le prestazioni dei diversi metodi di accesso ai dati.  
  
 Per completare l'esempio, eseguire più volte il codice seguente. Ignorare i risultati della prima esecuzione perché su di essa influisce negativamente l'allocazione di memoria iniziale.  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 I risultati previsti forniscono tempi di risposta effettivi che mostrano come l'utilizzo di tabelle ottimizzate per la memoria e di stored procedure compilate in modo nativo in genere garantisca in modo coerente tempi di risposta più rapidi rispetto all'esecuzione degli stessi carichi di lavoro su tabelle basate su disco tradizionali.  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni a AdventureWorks per illustrare OLTP in memoria](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [OLTP in memoria &#40;l'ottimizzazione in memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)   
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)   
 [Requisiti per l'uso di tabelle ottimizzate per la memoria](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [CREATE PROCEDURE e tabelle con ottimizzazione per la memoria](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
