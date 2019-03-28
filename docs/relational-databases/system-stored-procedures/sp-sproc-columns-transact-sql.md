---
title: sp_sproc_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8fd3e7ba4880a5d908991d32faaa9c1a5275976f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533993"
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni relative alle colonne per una sola stored procedure o funzione definita dall'utente nell'ambiente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @procedure_name = ] 'name'` È il nome della procedura utilizzata per restituire informazioni del catalogo. *nome* viene **nvarchar (** 390 **)**, valore predefinito è %, ovvero tutte le tabelle nel database corrente. La ricerca con caratteri jolly è supportata.  
  
`[ @procedure_owner = ] 'owner'` È il nome del proprietario della procedura. *proprietario*viene **nvarchar (** 384 **)**, con un valore predefinito è NULL. La ricerca con caratteri jolly è supportata. Se *proprietario* non viene specificato, si applicano le regole di visibilità predefinite procedure del sistema DBMS sottostante.  
  
 Se l'utente corrente è il proprietario di una procedura avente il nome specificato, vengono restituite informazioni su tale procedura. Se *owner*non viene specificato e l'utente corrente non dispone di una procedura con il nome specificato **sp_sproc_columns** cerca di una procedura avente il nome specificato che appartenga al proprietario del database. Se tale procedura viene individuata, vengono restituite informazioni sulle colonne corrispondenti.  
  
`[ @procedure_qualifier = ] 'qualifier'` È il nome del qualificatore della procedura. *qualificatore* viene **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi di tabelle in tre parti (*composti*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questo parametro rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
`[ @column_name = ] 'column_name'` È una singola colonna e viene usato quando è necessaria una sola colonna di informazioni del catalogo. *column_name* viene **nvarchar (** 384 **)**, con un valore predefinito è NULL. Se *column_name* viene omesso, vengono restituite tutte le colonne. La ricerca con caratteri jolly è supportata. Per ottenere la massima interoperabilità, è consigliabile che nel client del gateway vengano utilizzati solo i caratteri jolly dello standard ISO, ovvero i caratteri % e _.  
  
`[ @ODBCVer = ] 'ODBCVer'` È in uso la versione di ODBC. *ODBCVer* viene **int**, e il valore predefinito è 2, che indica ODBC versione 2.0. Per altre informazioni sulle differenze tra ODBC versione 2.0 e ODBC versione 3.0, fare riferimento a ODBC **SQLProcedureColumns** specifica per ODBC versione 3.0  
  
`[ @fUsePattern = ] 'fUsePattern'` Determina se il carattere di sottolineatura (_), simbolo di percentuale (%) e parentesi quadre ([]) vengono interpretate come caratteri jolly. I valori validi sono 0 (utilizzo dei criteri di ricerca disattivato) e 1 (utilizzo dei criteri di ricerca attivato). *fUsePattern* viene **bit**, con un valore predefinito è 1.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Nome di qualificatore della procedura. Questa colonna può essere NULL.|  
|**PROCEDURE_OWNER**|**sysname**|Nome del proprietario della procedura. In questa colonna viene sempre restituito un valore.|  
|**PROCEDURE_NAME**|**nvarchar(** 134 **)**|Nome della procedura. In questa colonna viene sempre restituito un valore.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna per ogni colonna della **TABLE_NAME** restituito. In questa colonna viene sempre restituito un valore.|  
|**COLUMN_TYPE**|**smallint**|In questo campo viene sempre restituito un valore.<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|Codice integer di un tipo di dati ODBC. Se non è possibile effettuare il mapping di questo tipo di dati a un tipo ISO, il valore è NULL. Viene restituito il nome del tipo di dati nativi nel **TYPE_NAME** colonna.|  
|**TYPE_NAME**|**sysname**|Rappresentazione in forma di stringa del tipo di dati. Corrisponde al nome del tipo di dati visualizzato dal sistema DBMS sottostante.|  
|**PRECISION**|**int**|Numero di cifre significative. Il valore restituito per il **precisione** colonna si trova in base 10.|  
|**LENGTH**|**int**|Dimensioni di trasferimento dei dati.|  
|**SCALABILITÀ**|**smallint**|Numero di cifre a destra del separatore decimale.|  
|**RADIX**|**smallint**|Base per i tipi di dati numerici.|  
|**AMMETTE VALORI NULL**|**smallint**|Specifica se i valori Null sono supportati o meno:<br /><br /> 1 = È possibile creare il tipo di dati con supporto per valori Null.<br /><br /> 0 = I valori Null non sono supportati.|  
|**REMARKS**|**varchar(** 254 **)**|Descrizione della colonna della procedura. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene restituito alcun valore per questa colonna.|  
|**COLUMN_DEF**|**nvarchar(** 4000 **)**|Valore predefinito della colonna.|  
|**SQL_DATA_TYPE**|**smallint**|Valore del tipo di dati SQL visualizzato nei **tipo** campo del descrittore. Questa colonna corrisponde alla colonna **DATA_TYPE**, tranne che per i tipi di dati **datetime** e ISO **interval**. In questa colonna viene sempre restituito un valore.|  
|**SQL_DATETIME_SUB**|**smallint**|Sottocodice **datetime** ISO **interval** se il valore di **SQL_DATA_TYPE** è **SQL_DATETIME** o **SQL_INTERVAL**. Per i dati di tipi diversi da **data/ora** e ISO **intervallo**, questo campo è NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Lunghezza massima in byte di un **carattere** oppure **binario** colonna tipo di dati. Per gli tutti gli altri tipi di dati, il valore di questa colonna è NULL.|  
|**ORDINAL_POSITION**|**int**|Posizione ordinale della colonna nella tabella. La prima colonna nella tabella è 1. In questa colonna viene sempre restituito un valore.|  
|**IS_NULLABLE**|**varchar(254)**|Impostazione relativa al supporto di valori Null nella colonna della tabella. Per determinare il supporto di valori Null vengono seguite le regole ISO. In un sistema DBMS conforme a ISO non vengono restituite stringhe vuote.<br /><br /> Se la colonna ammette valori Null, viene visualizzato YES. In caso contrario viene visualizzato NO.<br /><br /> Quando non è noto se i valori Null sono supportati, in questa colonna viene restituita una stringa di lunghezza zero.<br /><br /> Il valore restituito per questa colonna è diverso dal valore restituito per la colonna NULLABLE.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dalle stored procedure estese. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
## <a name="remarks"></a>Note  
 **sp_sproc_columns** equivale a **SQLProcedureColumns** in ODBC. I risultati restituiti vengono ordinati **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**, **PROCEDURE_NAME**e l'ordine in cui i parametri vengono visualizzati nella procedura definizione.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
