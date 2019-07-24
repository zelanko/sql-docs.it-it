---
title: CREATE TABLE (grafo SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc76bc81bc1f8573430bec9cdeba62b04e25167f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116947"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE (grafo SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Crea una nuova tabella di grafi SQL come tabella `NODE` o `EDGE`. 
  
> [!NOTE]   
>  Per le istruzioni Transact-SQL standard, vedere [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
CREATE TABLE   
    { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>Argomenti  
Questo documento include solo gli argomenti relativi al grafo SQL. Per un elenco completo e una descrizione degli argomenti supportati, vedere [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 Nome del database in cui è viene creata la tabella. *database_name* deve specificare il nome di un database esistente. Se non viene specificato, per impostazione predefinita *database_name* è il database corrente. L'account di accesso per la connessione corrente deve essere associato a un ID utente esistente nel database specificato da *database_name*. Questo ID utente deve avere le autorizzazioni CREATE TABLE.  
  
 *schema_name*    
 Nome dello schema a cui appartiene la nuova tabella.  
  
 *table_name*    
 Nome della tabella nodi o bordi. I nomi delle tabelle devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md). *table_name* può essere costituito al massimo da 128 caratteri, ad eccezione dei nomi di tabelle temporanee locali, ovvero i nomi preceduti da un solo simbolo di cancelletto (#), che non possono superare i 116 caratteri.  
  
 NODE   
 Crea una tabella nodi.

 EDGE  
 Crea una tabella bordi.  
  
## <a name="remarks"></a>Remarks  
La creazione di una tabella temporanea come tabella nodi o bordi non è supportata.  

La creazione di una tabella nodi o bordi come tabella temporanea non è supportata.

Stretch Database non è supportato per la tabella nodi o bordi.

Le tabelle nodi o bordi non possono essere tabelle esterne. PolyBase non supporta le tabelle di grafi. 
  
 
## <a name="examples"></a>Esempi  
  
### <a name="a-create-a-node-table"></a>A. Creare una tabella `NODE`
 L'esempio seguente illustra come creare una tabella `NODE`

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. Creare una tabella `EDGE`
L'esempio seguente illustra come creare tabelle `EDGE`

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT (grafo SQL)](../../t-sql/statements/insert-sql-graph.md)  
 [Graph Processing with SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md) (Elaborazione di grafi con SQL Server 2017)

