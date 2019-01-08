---
title: sp_columns_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aaf644b6a8795e9c68e0053eaed0023c4b9299b6
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588405"
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le informazioni sulle colonne, utilizzando una riga per ogni colonna, per le tabelle del server collegato specificato. **sp_columns_ex** restituisce informazioni relative alla solo la colonna specifica, se *colonna* è specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@table_server =** ] **'**_table_server_**'**  
 Nome del server collegato per cui si desidera restituire le informazioni sulle colonne. *table_server* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 Nome della tabella per cui si desidera restituire le informazioni sulle colonne. *TABLE_NAME* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 Nome dello schema per cui si desidera restituire le informazioni sulle colonne. *TABLE_SCHEMA* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 Nome del catalogo per cui si desidera restituire le informazioni sulle colonne. *TABLE_CATALOG* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@column_name =** ] **'**_colonna_**'**  
 Nome della colonna del database per cui si desidera ottenere informazioni. *colonna* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@ODBCVer =** ] **'**_ODBCVer_**'**  
 Versione di ODBC utilizzata. *ODBCVer* viene **int**, con un valore predefinito è 2. che indica ODBC versione 2. I valori validi sono 2 e 3. Per informazioni sulle differenze di comportamento tra le versioni 2 e 3, vedere la specifica relativa a SQLColumns di ODBC.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nome del qualificatore della tabella o della vista. Vari prodotti DBMS supportano nomi di tabelle in tre parti (_qualificatore_**.** _owner_**.** _nome_). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa colonna rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella. Questo campo può essere NULL.|  
|**TABLE_SCHEM**|**sysname**|Nome del proprietario della tabella o della vista. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome dell'utente del database che ha creato la tabella. Questo campo restituisce sempre un valore.|  
|**TABLE_NAME**|**sysname**|Nome della tabella o della vista. Questo campo restituisce sempre un valore.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna, per ogni colonna della **TABLE_NAME** restituito. Questo campo restituisce sempre un valore.|  
|**DATA_TYPE**|**smallint**|Valore intero corrispondente agli indicatori del tipo di dati ODBC. Se si tratta di un tipo di dati di cui non è possibile eseguire il mapping a un tipo ODBC, il valore è NULL. Viene restituito il nome del tipo di dati nativi nel **TYPE_NAME** colonna.|  
|**TYPE_NAME**|**varchar (** 13 **)**|Stringa che rappresenta un tipo di dati. Il DBMS sottostante utilizza questo nome del tipo di dati.|  
|**VALORE DI COLUMN_SIZE**|**int**|Numero di cifre significative. Il valore restituito per il **precisione** colonna si trova in base 10.|  
|**BUFFER_LENGTH**|**int**|Dimensioni di trasferimento dei dati.1|  
|**DECIMAL_DIGITS**|**smallint**|Numero di cifre a destra del separatore decimale.|  
|**NUM_PREC_RADIX**|**smallint**|Base per i tipi di dati numerici.|  
|**AMMETTE VALORI NULL**|**smallint**|Specifica se i valori Null sono supportati.<br /><br /> 1 = I valori Null sono supportati.<br /><br /> 0 = I valori Null non sono supportati (NOT NULL).|  
|**SEZIONE OSSERVAZIONI**|**varchar (** 254 **)**|In questo campo viene sempre restituito NULL.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|Valore predefinito della colonna.|  
|**SQL_DATA_TYPE**|**smallint**|Valore del tipo di dati SQL visualizzato nel campo TYPE del descrittore. Questa colonna corrisponde al **DATA_TYPE** colonna, tranne che per il **datetime** e SQL-92 **intervallo** i tipi di dati. In questa colonna viene sempre restituito un valore.|  
|**SQL_DATETIME_SUB**|**smallint**|Codice di sottotipo per **data/ora** e SQL-92 **intervallo** i tipi di dati. Per gli altri tipi di dati in questa colonna viene restituito NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Lunghezza massima, espressa in byte, di una colonna di tipo carattere o integer. Per tutti gli altri tipi di dati in questa colonna viene restituito NULL.|  
|**ORDINAL_POSITION**|**int**|Posizione ordinale della colonna nella tabella. La prima colonna nella tabella è 1. In questa colonna viene sempre restituito un valore.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|Impostazione relativa al supporto di valori Null nella colonna della tabella. Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO SQL non vengono restituite stringhe vuote.<br /><br /> YES = La colonna ammette valori Null.<br /><br /> NO = La colonna non ammette valori Null.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Il valore restituito per questa colonna è diversa dal valore restituito per il **NULLABLE** colonna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato in stored procedure estese.|  
  
 Per ulteriori informazioni, vedere la documentazione di Microsoft ODBC.  
  
## <a name="remarks"></a>Note  
 **sp_columns_ex** viene eseguita tramite una query di set di righe COLUMNS il **IDBSchemaRowset** interfaccia del provider OLE DB corrispondente a *table_server*. Il *nome_tabella*, *table_schema*, *table_catalog*, e *colonna* i parametri vengono passati a questa interfaccia per limitare le righe restituito.  
  
 **sp_columns_ex** restituisce un risultato vuoto se il provider OLE DB del server collegato specificato non supporta il set di righe COLUMNS di impostare il **IDBSchemaRowset** interfaccia.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="remarks"></a>Note  
 **sp_columns_ex** soddisfa i requisiti per gli identificatori delimitati. Per altre informazioni, vedere [Identificatori del database](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il tipo di dati della colonna `JobTitle` della tabella `HumanResources.Employee` inclusa nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] disponibile nel server collegato `Seattle1`.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
