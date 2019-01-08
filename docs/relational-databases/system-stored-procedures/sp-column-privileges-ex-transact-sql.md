---
title: sp_column_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b79fbbd504f7294835e92401a2210e6acac3c440
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514017"
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce i privilegi di una colonna della tabella specificata nel server collegato specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@table_server =** ] **'**_table_server_**'**  
 Nome del server collegato per cui si desidera restituire le informazioni. *table_server* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 Nome della tabella che include la colonna specificata. *TABLE_NAME* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 Schema della tabella. *TABLE_SCHEMA* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 È il nome del database in cui l'oggetto specificato *table_name* risiede. *TABLE_CATALOG* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@column_name =** ] **'**_column_name_**'**  
 Nome della colonna di cui si desidera ottenere informazioni sui privilegi. *column_name* viene **sysname**, con un valore predefinito è NULL (tutte le comuni).  
  
## <a name="result-sets"></a>Set di risultati  
 Nella tabella seguente vengono descritte le colonne dei set di risultati. I risultati restituiti vengono ordinati **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, **COLUMN_NAME**, e  **PRIVILEGIO**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome del qualificatore della tabella. Vari prodotti DBMS supportano nomi di tabelle in tre parti (_qualificatore_**.** _owner_**.** _nome_). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella. Questo campo può essere NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome del proprietario della tabella. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome dell'utente del database che ha creato la tabella. Questo campo restituisce sempre un valore.|  
|**TABLE_NAME**|**sysname**|Nome della tabella. Questo campo restituisce sempre un valore.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna, per ogni colonna della **TABLE_NAME** restituito. Questo campo restituisce sempre un valore.|  
|**UTENTE CHE CONCEDE**|**sysname**|Nome utente del database che ha concesso autorizzazioni al **COLUMN_NAME** per la tabella **all'utente autorizzato**. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa colonna è sempre lo stesso come il **TABLE_OWNER**. Questo campo restituisce sempre un valore.<br /><br /> Il **GRANTOR** colonna può essere il proprietario del database (**TABLE_OWNER**) o un utente a cui il proprietario del database concesso autorizzazioni tramite la clausola WITH GRANT OPTION dell'istruzione GRANT.|  
|**ALL'UTENTE AUTORIZZATO**|**sysname**|Nome utente del database che disponga delle autorizzazioni per questo **COLUMN_NAME** per la tabella **GRANTOR**. Questo campo restituisce sempre un valore.|  
|**CON PRIVILEGI**|**varchar (** 32 **)**|Una delle autorizzazioni di colonna disponibili. Le autorizzazioni di colonna possono essere rappresentate da uno dei valori riportati di seguito o da altri valori supportati dall'origine dei dati in fase di definizione dell'implementazione:<br /><br /> Selezionare = **al BENEFICIARIO** può recuperare dati per le colonne.<br /><br /> INSERT = **all'utente autorizzato** può fornire dati per questa colonna quando vengono inserite nuove righe (per il **all'utente autorizzato**) nella tabella.<br /><br /> UPDATE = **al BENEFICIARIO** può modificare i dati della colonna.<br /><br /> I riferimenti = **al BENEFICIARIO** può fare riferimento a una colonna in una tabella esterna in una relazione chiave primaria/esterna principale. Questo tipo di relazione viene definito tramite vincoli di tabella.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Indica se il **al BENEFICIARIO** è la possibilità di concedere autorizzazioni ad altri utenti (noto anche come "Concedi" autorizzazione). I possibili valori sono YES, NO e NULL. Un valore sconosciuto, o NULL, corrisponde a un'origine dei dati per la quale questo tipo di assegnazione delle autorizzazioni non è consentito.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni relative ai privilegi di colonna della tabella `HumanResources.Department` del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nel server collegato `Seattle1`.  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_table_privileges_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
