---
title: sp_primarykeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_primarykeys_TSQL
- sp_primarykeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_primarykeys
ms.assetid: 0f76dd31-5b7b-4209-9e2e-b9ed5cac164d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 484890cfe30ace1c65ea45fe2d9e447a6396b52e
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591455"
---
# <a name="spprimarykeys-transact-sql"></a>sp_primarykeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le colonne chiave primaria (una riga per ogni colonna chiave) per la tabella remota specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@table_server =** ] **'**_table_server'_  
 Nome del server collegato da cui si desidera ottenere informazioni sulla chiave primaria. *table_server* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 Nome della tabella per cui si desidera ottenere informazioni sulla chiave primaria. *TABLE_NAME*viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 Schema della tabella. *TABLE_SCHEMA* viene **sysname**, con un valore predefinito è NULL. In ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrisponde al proprietario della tabella.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 È il nome del catalogo in cui l'oggetto specificato *table_name* risiede. In ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrisponde al nome del database. *TABLE_CATALOG* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Catalogo della tabella.|  
|**TABLE_SCHEM**|**sysname**|Schema della tabella.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna.|  
|**KEY_SEQ**|**int**|Numero sequenziale della colonna in una chiave primaria a più colonne.|  
|**PK_NAME**|**sysname**|Identificatore della chiave primaria. Se non è applicabile all'origine dei dati, restituisce NULL.|  
  
## <a name="remarks"></a>Note  
 **sp_primarykeys** viene eseguita tramite una query di set di righe PRIMARY_KEYS del **IDBSchemaRowset** interfaccia del provider OLE DB corrispondente a *table_server*. Il *nome_tabella*, *table_schema*, *table_catalog*, e *colonna* i parametri vengono passati a questa interfaccia per limitare le righe restituito.  
  
 **sp_primarykeys** restituisce un risultato vuoto se il provider OLE DB del server collegato specificato non supporta il set di righe PRIMARY_KEYS di impostare il **IDBSchemaRowset** interfaccia.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite le colonne chiave primaria dal server `LONDON1` per la tabella `HumanResources.JobCandidate` nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2012',   
   @table_schema = N'HumanResources';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Distributed query Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
