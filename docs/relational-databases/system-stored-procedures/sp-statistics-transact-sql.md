---
title: sp_statistics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_statistics_TSQL
- sp_statistics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fdf0984f172657ad45ee6da0a09de5e0e457b003
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004197"
---
# <a name="spstatistics-transact-sql"></a>sp_statistics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce un elenco di tutti gli indici e le statistiche per la tabella o vista indicizzata specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @table_name = ] 'table_name'` Specifica la tabella utilizzata per restituire informazioni del catalogo. *TABLE_NAME* viene **sysname**, non prevede alcun valore predefinito. I criteri di ricerca con caratteri jolly non sono supportati.  
  
`[ @table_owner = ] 'owner'` È il nome del proprietario della tabella della tabella utilizzata per restituire informazioni del catalogo. *TABLE_OWNER* viene **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *proprietario* non viene specificato, si applicano le regole di visibilità della tabella predefinite del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se l'utente corrente è il proprietario di una tabella con il nome specificato, vengono restituiti gli indici di tale tabella. Se *proprietario* non viene specificato e l'utente corrente non dispone di una tabella con la proprietà specificata *nome*, viene eseguita la ricerca per una tabella con la proprietà specificata *nome* di proprietà di proprietario del database. Se tale tabella esiste, vengono restituiti gli indici corrispondenti.  
  
`[ @table_qualifier = ] 'qualifier'` È il nome del qualificatore della tabella. *qualificatore* viene **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano nomi di tabelle in tre parti (_qualificatore_ **.** _owner_ **.** _nome_). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questo parametro rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
`[ @index_name = ] 'index_name'` È il nome dell'indice. *index_name* viene **sysname**, con un valore predefinito è %. La ricerca con caratteri jolly è supportata.  
  
`[ @is_unique = ] 'is_unique'` È se solo indici univoci (se **Y**) devono essere restituiti. *is_unique* viene **char (1)** , il valore predefinito è **N**.  
  
`[ @accuracy = ] 'accuracy'` È il livello di accuratezza della pagina per le statistiche e cardinalità. *accuratezza* viene **char (1)** , il valore predefinito è **Q**. Specificare **elettronica** per assicurarsi che le statistiche vengono aggiornate in modo che la cardinalità e le pagine siano accurate.  
  
 Il valore **elettronica** (SQL_ENSURE) chiede al driver di recuperare in modo incondizionato le statistiche.  
  
 Il valore **Q** (SQL_QUICK) chiede al driver di recuperare la cardinalità e le pagine solo se queste sono immediatamente disponibili dal server. In tal caso, il driver non garantisce che i valori siano aggiornati. Per le applicazioni scritte in base allo standard Open Group viene restituito sempre il comportamento di SQL_QUICK da driver conformi a ODBC 3.x.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nome del qualificatore della tabella. Questa colonna può essere NULL.|  
|**TABLE_OWNER**|**sysname**|Nome del proprietario della tabella. In questa colonna viene sempre restituito un valore.|  
|**TABLE_NAME**|**sysname**|Nome della tabella. In questa colonna viene sempre restituito un valore.|  
|**NON_UNIQUE**|**smallint**|NOT NULL.<br /><br /> 0 = Univoco<br /><br /> 1 = Non univoco|  
|**INDEX_QUALIFIER**|**sysname**|Nome del proprietario dell'indice. In alcuni prodotti DBMS gli indici possono essere creati da utenti diversi dal proprietario della tabella. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa colonna è sempre identico **TABLE_NAME**.|  
|**INDEX_NAME**|**sysname**|Nome dell'indice. In questa colonna viene sempre restituito un valore.|  
|**TYPE**|**smallint**|Questa colonna restituisce sempre un valore:<br /><br /> 0 = Statistiche di una tabella<br /><br /> 1 = Cluster<br /><br /> 2 = Hash<br /><br /> 3 = non cluster|  
|**SEQ_IN_INDEX**|**smallint**|Posizione della colonna all'interno dell'indice.|  
|**COLUMN_NAME**|**sysname**|Nome della colonna per ogni colonna della **TABLE_NAME** restituito. In questa colonna viene sempre restituito un valore.|  
|**COLLATION**|**char(1)**|Ordine utilizzato nelle regole di confronto. I possibili valori sono i seguenti:<br /><br /> A = Crescente<br /><br /> D = Decrescente<br /><br /> NULL = Non applicabile|  
|**CARDINALITÀ**|**int**|Numero di righe nella tabella o di valori univoci nell'indice.|  
|**PAGES**|**int**|Numero di pagine in cui archiviare l'indice o la tabella.|  
|**FILTER_CONDITION**|**varchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non restituisce un valore.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="remarks"></a>Note  
 Gli indici nel set di risultati vengono visualizzati in ordine crescente per le colonne **NON_UNIQUE**, **tipo**, **INDEX_NAME**, e **SEQ_IN_INDEX**.  
  
 Gli indici di tipo cluster sono quelli in cui i dati della tabella sono archiviati nell'ordine dell'indice, Ciò corrisponde a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indici cluster.  
  
 Il tipo di indice Hash accetta ricerche di corrispondenze esatte o ricerche basate su intervalli, ma non viene utilizzato per ricerche con criteri.  
  
 **sp_statistics** equivale a **SQLStatistics** in ODBC. I risultati restituiti vengono ordinati **NON_UNIQUE**, **tipo**, **INDEX_QUALIFIER**, **INDEX_NAME**, e **SEQ_IN_ INDICE**. Per altre informazioni, vedere la [riferimento all'API ODBC](https://go.microsoft.com/fwlink/?LinkId=68323).  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempio: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente restituisce informazioni relative al `DimEmployee` tabella.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

