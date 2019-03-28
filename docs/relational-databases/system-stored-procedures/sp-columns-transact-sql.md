---
title: sp_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1155937c8634fe9859b13b84f2e42be6ceb825d0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530423"
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Vengono restituite le informazioni di colonna per gli oggetti specificati per cui è possibile eseguire una query nell'ambiente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ \@table_name = ] object` È il nome dell'oggetto che viene utilizzata per restituire informazioni del catalogo. *oggetto* può essere una tabella, vista oppure altro oggetto che dispone di colonne, ad esempio le funzioni con valori di tabella. *oggetto* viene **nvarchar (384)**, non prevede alcun valore predefinito. La ricerca con caratteri jolly è supportata.  
  
`[ \@table_owner = ] owner` È il proprietario dell'oggetto dell'oggetto che viene utilizzata per restituire informazioni del catalogo. *proprietario* viene **nvarchar (384)**, con un valore predefinito è NULL. La ricerca con caratteri jolly è supportata. Se *proprietario* non viene specificato, si applicano le regole di visibilità di oggetto predefinito del sistema DBMS sottostante.  
  
 Se l'utente corrente è il proprietario di un oggetto con il nome specificato, vengono restituite le colonne di tale oggetto. Se *owner* non viene specificato e l'utente corrente non dispone di un oggetto con l'oggetto specificato *oggetto*, **sp_columns** Cerca un oggetto con l'oggetto specificato  *oggetto* appartengono al proprietario del database. Se viene individuato, vengono restituite le colonne di tale oggetto.  
  
`[ \@table_qualifier = ] qualifier` È il nome del qualificatore dell'oggetto. *qualificatore* viene **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano tre parti di denominazione per oggetti (_qualificatore_**.** _owner_**.** _nome_). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In alcuni prodotti rappresenta il nome del server dell'ambiente di database dell'oggetto.  
  
`[ \@column_name = ] column` È una singola colonna e viene usato quando è necessaria una sola colonna di informazioni del catalogo. *colonna* viene **nvarchar (384)**, con un valore predefinito è NULL. Se *colonna* viene omesso, vengono restituite tutte le colonne. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *colonna* rappresenta il nome di colonna elencato nella **syscolumns** tabella. La ricerca con caratteri jolly è supportata. Per ottenere la massima interoperabilità, è consigliabile che nel client di gateway siano utilizzati solo i caratteri jolly standard di SQL-92, ovvero i caratteri % e _.  
  
`[ \@ODBCVer = ] ODBCVer` È la versione di ODBC utilizzata. *ODBCVer* viene **int**, con un valore predefinito è 2. che indica ODBC versione 2. I valori validi sono 2 e 3. Per le differenze di comportamento tra le versioni 2 e 3, vedere ODBC **SQLColumns** specifica.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
 Il **sp_columns** è equivalente alla stored procedure di catalogo **SQLColumns** in ODBC. I risultati restituiti vengono ordinati **TABLE_QUALIFIER**, **TABLE_OWNER**, e **TABLE_NAME**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome del qualificatore dell'oggetto. Questo campo può essere NULL.|  
|**TABLE_OWNER**|**sysname**|Nome del proprietario dell'oggetto. Questo campo restituisce sempre un valore.|  
|**TABLE_NAME**|**sysname**|Nome dell'oggetto. Questo campo restituisce sempre un valore.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna, per ogni colonna della **TABLE_NAME** restituito. Questo campo restituisce sempre un valore.|  
|**DATA_TYPE**|**smallint**|Codice integer per il tipo di dati ODBC. Se si tratta di un tipo di dati di cui non è possibile eseguire il mapping a un tipo ODBC, il valore è NULL. Viene restituito il nome del tipo di dati nativi nel **TYPE_NAME** colonna.|  
|**TYPE_NAME**|**sysname**|Stringa che rappresenta un tipo di dati. Il DBMS sottostante utilizza questo nome del tipo di dati.|  
|**PRECISION**|**int**|Numero di cifre significative. Il valore restituito per il **precisione** colonna si trova in base 10.|  
|**LENGTH**|**int**|Dimensioni di trasferimento dei dati. <sup>1</sup>|  
|**SCALABILITÀ**|**smallint**|Numero di cifre a destra del separatore decimale.|  
|**RADIX**|**smallint**|Base per i tipi di dati numerici.|  
|**AMMETTE VALORI NULL**|**smallint**|Specifica se i valori Null sono supportati.<br /><br /> 1 = I valori Null sono supportati.<br /><br /> 0 = I valori Null non sono supportati (NOT NULL).|  
|**REMARKS**|**varchar(254)**|In questo campo viene sempre restituito NULL.|  
|**COLUMN_DEF**|**nvarchar(4000)**|Valore predefinito della colonna.|  
|**SQL_DATA_TYPE**|**smallint**|Valore del tipo di dati SQL visualizzato nel campo TYPE del descrittore. Questa colonna corrisponde al **DATA_TYPE** colonna, tranne che per il **datetime** e SQL-92 **intervallo** i tipi di dati. In questa colonna viene sempre restituito un valore.|  
|**SQL_DATETIME_SUB**|**smallint**|Codice di sottotipo per **data/ora** e SQL-92 **intervallo** i tipi di dati. Per gli altri tipi di dati in questa colonna viene restituito NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Lunghezza massima, espressa in byte, di una colonna di tipo carattere o integer. Per tutti gli altri tipi di dati in questa colonna viene restituito NULL.|  
|**ORDINAL_POSITION**|**int**|Posizione ordinale della colonna nell'oggetto. La prima colonna nell'oggetto è 1. In questa colonna viene sempre restituito un valore.|  
|**IS_NULLABLE**|**varchar(254)**|Supporto di valori Null della colonna dell'oggetto. Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO SQL non vengono restituite stringhe vuote.<br /><br /> YES = La colonna ammette valori Null.<br /><br /> NO = La colonna non ammette valori Null.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Il valore restituito per questa colonna è diversa dal valore restituito per il **NULLABLE** colonna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dalle stored procedure estese. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
 <sup>1</sup> per altre informazioni, vedere la documentazione di Microsoft ODBC.  
  
## <a name="permissions"></a>Permissions  
 Richiede le autorizzazioni SELECT e VIEW DEFINITION per lo schema.  
  
## <a name="remarks"></a>Note  
 **sp_columns** soddisfa i requisiti per gli identificatori delimitati. Per altre informazioni, vedere [Identificatori del database](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sulle colonne della tabella specificata.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente vengono restituite informazioni sulle colonne della tabella specificata.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


