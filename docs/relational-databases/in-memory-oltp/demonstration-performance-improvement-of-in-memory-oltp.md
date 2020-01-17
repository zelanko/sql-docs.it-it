---
title: Miglioramento delle prestazioni di OLTP in memoria
ms.custom: seo-dt-2019
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68cb4e95046ca2fb071ecf2ba7c713cf57646690
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412732"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Dimostrazione: miglioramento delle prestazioni di OLTP in memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  L'esempio di codice in questo argomento illustra la rapidità delle prestazioni delle tabelle ottimizzate per la memoria. Il miglioramento delle prestazioni è evidente quando l'accesso ai dati in una tabella ottimizzata per la memoria viene eseguito da codice [!INCLUDE[tsql](../../includes/tsql-md.md)]tradizionale e interpretato. Il miglioramento delle prestazioni è ancora maggiore quando l'accesso ai dati in una tabella ottimizzata per la memoria viene eseguito da una stored procedure compilata in modo nativo (NCSProc).  
 
Per visualizzare una dimostrazione più completa dei potenziali miglioramenti delle prestazioni di OLTP In memoria, vedere [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)(Demo sulle prestazioni di OLTP in memoria v1.0). 
  
 L'esempio di codice in questo articolo è a thread singolo e non sfrutta i vantaggi della concorrenza di OLTP in memoria. Un carico di lavoro che utilizza la concorrenza avrà un miglioramento più significativo delle prestazioni. L'esempio di codice illustra solo un aspetto del miglioramento delle prestazioni, l'efficienza dell'accesso ai dati per INSERT.  
  
 Il miglioramento delle prestazioni offerto dalle tabelle ottimizzate per la memoria si ottiene in modo completo quando l'accesso ai dati in una tabella ottimizzata per la memoria viene eseguito da una NCSProc.  
  
## <a name="code-example"></a>Esempio di codice  
 Le sezioni seguenti descrivono ogni passaggio.  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>Passaggio 1a: Prerequisito se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 I passaggi descritti in questa prima sottosezione si applicano solo se è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e non sono applicabili se è in esecuzione [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Eseguire le operazioni seguenti:  
  
1.  Usare SQL Server Management Studio (SSMS.exe) per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. o qualsiasi strumento simile a SSMS.exe.  
  
2.  Creare manualmente una directory denominata **C:\data\\** . Il codice di esempio Transact-SQL prevede che la directory esista già.  
  
3.  Eseguire l'istruzione T-SQL breve per creare il database e il relativo filegroup ottimizzato per la memoria.  
  
```sql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>Passaggio 1b: Prerequisito se si usa [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 Questa sottosezione si applica solo se si usa [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Eseguire le operazioni seguenti:  
  
1.  Decidere quali database di test esistenti usare per l'esempio di codice.  
  
2.  Se si decide di creare un nuovo database di test, usare il [portale di Azure](https://portal.azure.com) per creare un database denominato **imoltp**.  
  
 Per istruzioni relative all'uso del portale di Azure a questo scopo, vedere l'argomento di [introduzione al database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-get-started).  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>Passaggio 2: Creare tabelle ottimizzate per la memoria e NCSProc  
 Questo passaggio crea una tabella ottimizzata per la memoria e una stored procedure compilata in modo nativo (NCSProc). Eseguire le operazioni seguenti:  
  
1.  Usare SSMS.exe per connettersi al nuovo database.  
  
2.  Eseguire l'istruzione T-SQL seguente nel database.  
  
```sql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>Passaggio 3: Eseguire il codice  
 È ora possibile eseguire le query che consentiranno di dimostrare le prestazioni delle tabelle ottimizzate per la memoria. Eseguire le operazioni seguenti:  
  
1.  Usare SSMS.exe per eseguire l'istruzione T-SQL seguente nel database.  
  
     Ignorare qualsiasi velocità o altri dati di prestazioni generati da questa prima esecuzione. La prima esecuzione garantisce l'esecuzione di diverse operazioni singole, ad esempio l'allocazione iniziale della memoria.  
  
2.  Usare nuovamente SSMS.exe per eseguire l'istruzione T-SQL seguente nel database.  
  
```sql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 Di seguito vengono indicate le statistiche temporali di output generate dall'esecuzione del secondo test.  
  
```sql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
