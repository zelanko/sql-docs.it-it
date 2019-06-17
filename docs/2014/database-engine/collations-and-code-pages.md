---
title: Collations and Code Pages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1969a3e30b31a21c380559a3e8898f87eb8848b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786736"
---
# <a name="collations-and-code-pages"></a>Tabelle codici e regole di confronto
  In [!INCLUDE[hek_2](../includes/hek-2-md.md)] sono presenti restrizioni per le tabelle codici supportate per le colonne di tipo (var)char nelle tabelle ottimizzate per la memoria e nelle regole di confronto supportate utilizzate negli indici e nelle stored procedure compilate in modo nativo.  
  
 La tabella codici per il valore (var)char determina il mapping tra i caratteri e la rappresentazione di byte archiviata nella tabella. Ad esempio, con la tabella codici Latin1 di Windows (1252, l'impostazione predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), il carattere "a" corrisponde al byte 0x61.  
  
 La tabella codici di un valore (var)char viene determinata dalle regole di confronto associate al valore. Ad esempio, alle regole di confronto SQL_Latin1_General_CP1_CI_AS è associata la tabella codici 1252.  
  
 Le regole di confronto di un valore vengono ereditate dalle regole di confronto del database o possono essere specificate in modo esplicito utilizzando la parola chiave COLLATE. Le regole di confronto del database non possono essere modificate se il database contiene tabelle ottimizzate per la memoria o stored procedure compilate in modo nativo. Nell'esempio seguente vengono impostate le regole di confronto del database e viene creata una tabella che include una colonna con regole di confronto diverse. Nel database vengono utilizzate regole di confronto con distinzione tra maiuscole e minuscole.  
  
 Gli indici possono essere creati solo sulle colonne stringa se vengono utilizzate le regole di confronto BIN2. Con la variabile LastName vengono utilizzate le regole di confronto BIN2. FirstName utilizza il valore predefinito del database, ovvero CI_AS (senza distinzione tra maiuscole e minuscole, con distinzione tra caratteri accentati e non accentati).  
  
> [!IMPORTANT]  
>  Non è possibile utilizzare un filtro per ordinare o raggruppare gli elementi nelle colonne stringa dell'indice in cui non vengono applicate le regole di confronto BIN2.  
  
```sql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 Le restrizioni seguenti si applicano alle tabelle ottimizzate per la memoria e alle stored procedure compilate in modo nativo:  
  
-   Per le colonne di tipo (var)char in tabelle ottimizzate per la memoria è necessario utilizzare le regole di confronto della tabella codici 1252. Questa restrizione non si applica alle colonne n(var)char. Il codice seguente recupera tutte le regole di confronto 1252:  
  
    ```sql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     Se è necessario archiviare caratteri non latini, utilizzare colonne di tipo colonne di tipo n(var)char.  
  
-   Gli indici su colonne di tipo (n)(var)char possono essere specificati solo con le regole di confronto BIN2 (vedere il primo esempio). La query seguente recupera tutte le regole di confronto BIN2 supportate:  
  
    ```sql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     Se si accede alla tabella tramite codice [!INCLUDE[tsql](../includes/tsql-md.md)]interpretato, è possibile utilizzare la parola chiave `COLLATE` per modificare le regole di confronto con espressioni o operazioni di ordinamento. Vedere l'ultimo esempio a questo proposito.  
  
-   Le stored procedure compilate in modo non possono utilizzare parametri, variabili locali o costanti stringa di tipo (var)char se le regole di confronto del database non sono le regole di confronto della tabella codici 1252.  
  
-   In tutte espressioni e le operazioni di ordinamento nelle stored procedure compilate in modo nativo devono essere utilizzate le regole di confronto BIN2. L'implicazione è che tutti i confronti e le operazioni di ordinamento si basano sugli elementi di codice Unicode dei caratteri (rappresentazioni binarie). Ad esempio, in tutte le operazioni di ordinamento viene fatta distinzione tra maiuscole e minuscole (" Z" viene prima di "a "). Se necessario, utilizzare codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato per le operazioni di ordinamento e confronto senza distinzione tra maiuscole e minuscole.  
  
-   Il troncamento dei dati UTF-16 non è supportato nelle stored procedure compilate in modo nativo. Ciò significa che char n (var) (*n*) i valori non possono essere convertito nel tipo n (var) char (*ho*), se *ho* < *n*, se la le regole di confronto includano SC property. Ad esempio, il codice seguente non è supportato:  
  
    ```sql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     Le funzioni di modifica della stringa, ad esempio LEN, SUBSTRING, LTRIM e RTRIM con dati UTF-16 non sono supportate in stored procedure compilate in modo nativo. Non è possibile utilizzare queste funzioni per valori n(var)char con regole di confronto _SC.  
  
     Dichiarare le variabili utilizzando tipi sufficientemente grandi per evitare il troncamento.  
  
 Nell'esempio seguente vengono illustrate alcune implicazioni e soluzioni alternative per le limitazioni delle regole di confronto in OLTP in memoria. Nell'esempio viene utilizzata la tabella Employees specificata in precedenza. Questo esempio vengono elencati tutti i dipendenti. Si noti che per LastName, a causa delle regole di confronto binarie, i nomi in maiuscolo vengono ordinati prima di quelli in minuscolo. Di conseguenza "Thomas" precede "nolan" perché i caratteri maiuscoli presentano elementi di codice più bassi. Per FirstName vengono utilizzate regole di confronto senza distinzione tra maiuscole e minuscole. L'ordinamento viene quindi applicato per lettera dell'alfabeto, non in base all'elemento di codice dei caratteri.  
  
```sql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
