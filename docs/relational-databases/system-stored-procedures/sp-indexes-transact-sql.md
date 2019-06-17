---
title: sp_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b1a14d1cf8c9eac0ace93e3aac6e16219fd60eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62961913"
---
# <a name="spindexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli indici per la tabella remota specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @table_server= ] '*table_server*'  
 Nome di un server collegato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di cui vengono richieste informazioni di tabella. *table_server* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ @table_name=] '*table_name*'  
 Nome della tabella remota per cui si desidera ottenere le informazioni di indice. *TABLE_NAME* viene **sysname**, con un valore predefinito è NULL. con cui vengono restituite tutte le tabelle del database specificato.  
  
 [ @table_schema=] '*table_schema*'  
 Specifica lo schema di tabella. In ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrisponde al proprietario della tabella. *TABLE_SCHEMA* viene **sysname**, con un valore predefinito è NULL.  
  
 [ @table_catalog= ] '*table_db*'  
 È il nome del database in cui *table_name* risiede. *table_db* viene **sysname**, con un valore predefinito è NULL. Se NULL, *table_db* per impostazione predefinita **master**.  
  
 [ @index_name=] '*index_name*'  
 Nome dell'indice per cui si desidera ottenere informazioni. *indice* viene **sysname**, con un valore predefinito è NULL.  
  
 [ @is_unique= ] '*is_unique*'  
 Tipo di indice per cui si desidera ottenere informazioni. *is_unique* viene **bit**, con un valore predefinito è NULL, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|1|Restituisce informazioni sugli indici univoci.|  
|0|Restituisce informazioni sugli indici non univoci.|  
|NULL|Restituisce informazioni su tutti gli indici.|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|Nome del database contenente la tabella specificata.|  
|TABLE_SCHEM|**sysname**|Schema della tabella.|  
|TABLE_NAME|**sysname**|Nome della tabella remota.|  
|NON_UNIQUE|**smallint**|Indica se l'indice è o meno univoco:<br /><br /> 0 = Univoco<br /><br /> 1 = Non univoco|  
|INDEX_QUALIFER|**sysname**|Nome del proprietario dell'indice. In alcuni prodotti DBMS gli indici possono essere creati da utenti diversi dal proprietario della tabella. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa colonna è sempre identico **TABLE_NAME**.|  
|INDEX_NAME|**sysname**|Nome dell'indice.|  
|TYPE|**smallint**|Tipo di indice:<br /><br /> 0 = Statistiche di una tabella<br /><br /> 1 = Cluster<br /><br /> 2 = Hash<br /><br /> 3 = altro|  
|ORDINAL_POSITION|**int**|Posizione ordinale della colonna nell'indice. La prima colonna nell'indice è 1. In questa colonna viene sempre restituito un valore.|  
|COLUMN_NAME|**sysname**|Nome corrispondente alle colonne di TABLE_NAME restituite.|  
|ASC_OR_DESC|**varchar**|Ordine adottato nelle regole di confronto:<br /><br /> A = Crescente<br /><br /> D = Decrescente<br /><br /> NULL = Non applicabile<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce sempre A.|  
|CARDINALITY|**int**|Numero di righe della tabella o valori univoci dell'indice.|  
|PAGES|**int**|Numero di pagine necessarie per l'archiviazione dell'indice o della tabella.|  
|FILTER_CONDITION|**nvarchar(** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non restituisce un valore.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite tutte le informazioni sugli indici dalla tabella `Employees` del database `AdventureWorks2012` nel server collegato `Seattle1`.  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Distributed query Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
