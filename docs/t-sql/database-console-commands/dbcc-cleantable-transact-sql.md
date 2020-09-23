---
description: DBCC CLEANTABLE (Transact-SQL)
title: DBCC CLEANTABLE (Transact-SQL)
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
author: pmasl
ms.author: umajay
ms.openlocfilehash: e8ef7510dfa2583464ac5f0dcf29405c13318476
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115016"
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Recupera lo spazio delle colonne a lunghezza variabile eliminate nelle tabelle e nelle viste indicizzate.
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *database_name* \| *database_id* \| 0  
 Database a cui appartiene la tabella in cui recuperare lo spazio. Se si specifica 0, viene utilizzato il database corrente. I nomi di database devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md).  
  
 *table_name* \| *table_id* \| *view_name* \| *view_id*  
 Tabella o vista indicizzata in cui recuperare lo spazio.  
  
 *batch_size*  
 Numero di righe elaborate per transazione. Se si omette l'argomento o si specifica 0, l'istruzione elabora l'intera tabella in una sola transazione.  
  
 WITH NO_INFOMSGS  
 Disattiva tutti i messaggi informativi.  
  
## <a name="remarks"></a>Osservazioni  
DBCC CLEANTABLE recupera lo spazio dopo l'eliminazione di una colonna a lunghezza variabile. I possibili tipi di dati per una colonna a lunghezza variabile sono i seguenti: **varchar**, **nvarchar**, **varchar(max)** , **nvarchar(max)** , **varbinary**, **varbinary(max)** , **text**, **ntext**, **image**, **sql_variant** e **xml**. Questo comando non consente di recuperare spazio dopo l'eliminazione di colonne a lunghezza fissa.
Se le colonne eliminate erano archiviate all'interno di righe, DBCC CLEANTABLE recupera lo spazio dall'unità di allocazione IN_ROW_DATA della tabella. Se le colonne erano archiviate all'esterno di righe, lo spazio viene recuperato dall'unità di allocazione ROW_OVERFLOW_DATA o LOB_DATA a seconda del tipo di dati della colonna eliminata. Se l'operazione di recupero di spazio da una pagina ROW_OVERFLOW_DATA o LOB_DATA restituisce una pagina vuota, DBCC CLEANTABLE rimuove tale pagina.
DBCC CLEANTABLE viene eseguita come una o più transazioni. Se non si specificano le dimensioni di batch, il comando elabora l'intera tabella in una sola transazione e per la tabella viene acquisito un blocco esclusivo durante l'operazione. Per tabelle di grandi dimensioni, la lunghezza della singola transazione e lo spazio del log necessario potrebbero risultare eccessivi. Se si specificano le dimensioni del batch, il comando viene eseguito in una serie di transazioni, ognuna con il numero di righe specificato. Non è possibile eseguire DBCC CLEANTABLE come una transazione all'interno di un'altra transazione.
Questa operazione viene registrata completamente.
L'istruzione DBCC CLEANTABLE non è supportata per l'utilizzo in tabelle di sistema, tabelle temporanee o nella parte dell'indice columnstore con ottimizzazione per la memoria xVelocity di una tabella.
  
## <a name="best-practices"></a>Procedure consigliate  
Non eseguire DBCC CLEANTABLE come attività di manutenzione di routine. Utilizzare invece DBCC CLEANTABLE dopo aver apportato modifiche significative alle colonne a lunghezza variabile di una tabella o di una vista indicizzata, se è necessario recuperare immediatamente lo spazio inutilizzato. In alternativa, è possibile ricompilare gli indici sulla tabella o sulla vista. Questa operazione richiede tuttavia molte risorse.
  
## <a name="result-sets"></a>Set di risultati  
DBCC CLEANTABLE restituisce:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Autorizzazioni  
 Il chiamante deve essere il proprietario della tabella o della vista indicizzata oppure un membro del ruolo predefinito del server **sysadmin** o dei ruoli predefiniti del database **db_owner** o **db_ddladmin**.  
  
## <a name="examples"></a>Esempi  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>R. Utilizzo di DBCC CLEANTABLE per il recupero di spazio  
Nell'esempio seguente viene eseguito DBCC CLEANTABLE per la tabella `Production.Document` del database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. Utilizzo di DBCC CLEANTABLE e verifica dei risultati  
Nell'esempio seguente viene creata e popolata una tabella con più colonne a lunghezza variabile. Due colonne vengono quindi eliminate e viene eseguito DBCC CLEANTABLE per recuperare lo spazio inutilizzato. Viene eseguita una query per verificare i conteggi delle pagine e i valori relativi allo spazio utilizzato prima e dopo l'esecuzione del comando DBCC CLEANTABLE.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche

- [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
- [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)
