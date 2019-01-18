---
title: sp_special_columns_100 (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fdebe91359fbe9d7c9ef7aaadc38ba096427f651
ms.sourcegitcommit: 0a64d26f865a21f4bd967b2b72680fd8638770b8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "54395387"
---
# <a name="spspecialcolumns100-sql-data-warehouse"></a>sp_special_columns_100 (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Restituisce il set di colonne ottimale per l'identificazione univoca di una riga nella tabella. Restituisce inoltre le colonne che vengono aggiornate automaticamente quando qualsiasi valore della riga viene aggiornato tramite una transazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @table_name=] '*table_name*'  
 Nome della tabella utilizzata per restituire informazioni sul catalogo. *nome* viene **sysname**, non prevede alcun valore predefinito. I criteri di ricerca con caratteri jolly non sono supportati.  
  
 [ @table_owner=] '*table_owner*'  
 Proprietario della tabella utilizzata per restituire informazioni sul catalogo. *proprietario* viene **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *proprietario* non viene specificato, si applicano le regole di visibilità della tabella predefinite del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se l'utente corrente è il proprietario di una tabella con il nome specificato, vengono restituite le colonne di tale tabella. Se *owner* non viene specificato e l'utente corrente non dispone di una tabella dell'oggetto specificato *name*, viene eseguita la ricerca per una tabella dell'oggetto specificato *nome* di proprietà del database proprietario. Se la tabella esiste, vengono restituite le colonne corrispondenti.  
  
 [ @qualifier=] '*qualifier*'  
 Nome del qualificatore di tabella. *qualificatore* viene **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi di tabelle in tre parti (*composti*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa colonna rappresenta il nome del database. In alcuni prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
 [ @col_type=] '*col_type*'  
 Tipo di colonna. *col_type* viene **char (** 1 **)**, con un valore predefinito di R. digitare R restituisce la colonna o ottimale set di colonne, tramite il recupero dei valori di colonna o le colonne, che consente di qualsiasi riga nell'oggetto specificato tabella che deve essere identificato in modo univoco. Una colonna può essere una pseudocolonna progettata a questo scopo oppure la colonna o le colonne di un indice univoco della tabella. Il tipo di colonna V restituisce le eventuali colonne della tabella specificata che vengono aggiornate automaticamente dall'origine dati in corrispondenza dell'aggiornamento di un valore della riga tramite una transazione.  
  
 [ @scope=] '*scope*'  
 Ambito minimo richiesto per ROWID. *ambito* viene **char (** 1 **)**, valore predefinito T. l'ambito C specifica che il valore ROWID è valido solo se posizionato in tale riga. L'ambito T indica che il valore ROWID è valido per la transazione.  
  
 [ @nullable=] '*nullable*'  
 Indica se le colonne speciali possono accettare un valore null. *nullable* viene **char (** 1 **)**, con un valore predefinito è u. il valore O specifica le colonne speciali che non ammettono valori null. mentre U specifica le colonne che ammettono parzialmente valori Null.  
  
 [ @ODBCVer=] '*ODBCVer*'  
 Versione ODBC utilizzata. *ODBCVer* viene **int (** 4 **)**, con un valore predefinito è 2. che indica ODBC versione 2.0. Per altre informazioni sulle differenze tra ODBC versione 2.0 e ODBC versione 3.0, vedere la specifica ODBC SQLSpecialColumns per ODBC versione 3.0.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|Ambito effettivo dell'ID della riga. Il Può essere 0, 1 o 2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Restituisce sempre 0. Questo campo restituisce sempre un valore.<br /><br /> 0 = SQL_SCOPE_CURROW. La validità dell'ID di riga è garantita solo mentre si è posizionati in tale riga. Una selezione successiva in base all'ID di riga potrebbe non restituire la riga se questa è stata aggiornata o eliminata da un'altra transazione.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. La validità dell'ID di riga è garantita per l'intera durata della transazione corrente.<br /><br /> 2 = SQL_SCOPE_SESSION. La validità dell'ID della riga è garantita per l'intera durata della sessione (oltre i limiti delle transazioni).|  
|COLUMN_NAME|**sysname**|Nome della colonna per ogni colonna della *tabella*restituito. Questo campo restituisce sempre un valore.|  
|DATA_TYPE|**smallint**|Tipo di dati SQL ODBC.|  
|TYPE_NAME|**sysname**|Nome del tipo di dati dipende dall'origine dati; ad esempio, **char**, **varchar**, **money**, oppure **testo**.|  
|PRECISION|**Int**|Precisione della colonna nell'origine dati. Questo campo restituisce sempre un valore.|  
|LENGTH|**Int**|Lunghezza, espressa in byte, necessaria per il tipo di dati in forma binaria nell'origine dati, ad esempio, 10 per **char (** 10 **)**, 4 per **integer**e 2 per **smallint** .|  
|SCALE|**smallint**|Scala della colonna nell'origine dati. Per i tipi di dati in cui la scala non è applicabile viene restituito NULL.|  
|PSEUDO_COLUMN|**smallint**|Indica se la colonna è una pseudocolonna. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce sempre 1:<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>Note  
 sp_datatype_columns corrisponde a SQLSpecialColumns in ODBC. I risultati restituiti vengono ordinati in base a SCOPE.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente vengono restituite informazioni sulla colonna che identifica in modo univoco le righe nella tabella `FactFinance`.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure di SQL Data Warehouse](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

