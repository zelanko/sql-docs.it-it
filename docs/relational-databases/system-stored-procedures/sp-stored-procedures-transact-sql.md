---
title: sp_stored_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff94284ba1f60d40697ad5a1e209b284dfaaefdf
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535193"
---
# <a name="spstoredprocedures-transact-sql"></a>sp_stored_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco delle stored procedure dell'ambiente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @sp_name = ] 'name'` È il nome della procedura utilizzata per restituire informazioni del catalogo. *nome* viene **nvarchar(390)**, con un valore predefinito è NULL. La ricerca con caratteri jolly è supportata.  
  
`[ @sp_owner = ] 'schema'` È il nome dello schema a cui appartiene la stored procedure. *lo schema* viene **nvarchar (384)**, con un valore predefinito è NULL. La ricerca con caratteri jolly è supportata. Se *proprietario* non viene specificato, si applicano le regole di visibilità predefinite procedure del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se lo schema corrente contiene una procedura con il nome specificato, viene restituita tale procedura. Se è specificata una stored procedure non qualificata, [!INCLUDE[ssDE](../../includes/ssde-md.md)] cerca la procedura nell'ordine seguente:  
  
-   Schema **sys** del database corrente.  
  
-   Schema predefinito del chiamante, se eseguito in batch o in un'istruzione SQL dinamica. In alternativa, se il nome della procedura non qualificata si trova nel corpo di un'altra definizione di procedura, la ricerca viene quindi eseguita all'interno dello schema contenente quest'ultima procedura.  
  
-   Schema **dbo** nel database corrente.  
  
`[ @qualifier = ] 'qualifier'` È il nome del qualificatore della procedura. *qualificatore* viene **sysname**, con un valore predefinito è NULL. Vari prodotti DBMS supportano i nomi di tre parti per le tabelle nel formato (_qualificatore_**.** _schema_**.** _nome_. Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *qualificatore* rappresenta il nome del database. In alcuni prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
`[ @fUsePattern = ] 'fUsePattern'` Determina se il carattere di sottolineatura (_), simbolo di percentuale (%) o parentesi quadre []) vengono interpretati come caratteri jolly. *fUsePattern* viene **bit**, con un valore predefinito è 1.  
  
 **0** = criteri di corrispondenza è disattivata.  
  
 **1** = criteri di corrispondenza si trova in.  
  
## <a name="return-code-values"></a>Valori restituiti  
 None  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Nome di qualificatore della procedura. Questa colonna può essere NULL.|  
|**PROCEDURE_OWNER**|**sysname**|Nome del proprietario della procedura. In questa colonna viene sempre restituito un valore.|  
|**PROCEDURE_NAME**|**nvarchar(134)**|Nome della procedura. In questa colonna viene sempre restituito un valore.|  
|**NUM_INPUT_PARAMS**|**int**|Riservato per utilizzi futuri.|  
|**NUM_OUTPUT_PARAMS**|**int**|Riservato per utilizzi futuri.|  
|**NUM_RESULT_SETS**|**int**|Riservato per utilizzi futuri.|  
|**REMARKS**|**varchar(254)**|Descrizione della procedura. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non viene restituito alcun valore per questa colonna.|  
|**PROCEDURE_TYPE**|**smallint**|Tipo di procedura. Tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene restituito sempre 2.0. I valori validi sono i seguenti:<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>Note  
 Per garantire la massima interoperabilità, con il client del gateway è consigliabile utilizzare solo i caratteri jolly standard SQL, ovvero il segno di percentuale (%) e il carattere di sottolineatura (_).  
  
 Le informazioni sulle autorizzazioni per l'accesso in esecuzione a una stored procedure specifica non vengono necessariamente verificate. Pertanto, l'accesso non è garantito. Si noti che viene utilizzata solo la denominazione in tre parti. Pertanto, con l'esecuzione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono restituite solo le stored procedure locali e non quelle remote, che richiedono una denominazione in quattro parti. Se l'attributo del server ACCESSIBLE_SPROC è Y nel set di risultati **sp_server_info**, vengono restituite solo le stored procedure che possono essere eseguite dall'utente corrente.  
  
 **sp_stored_procedures** equivale a **SQLProcedures** in ODBC. I risultati restituiti vengono ordinati **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**, e **PROCEDURE_NAME**.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione SELECT per lo schema.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. Restituzione di tutte le stored procedure nel database corrente  
 Nell'esempio seguente vengono restituite tutte le stored procedure nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. Restituzione di una singola stored procedure  
 Nell'esempio seguente viene restituito un set di risultati per la stored procedure `uspLogError`.  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
