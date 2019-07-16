---
title: sp_help_fulltext_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ac8e09eff53c04377ccd48a47cc31d9d7ddc5e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055021"
---
# <a name="sphelpfulltexttables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco delle tabelle registrate per l'indicizzazione full-text.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso **Sys. fulltext_indexes** invece la vista del catalogo. Per altre informazioni, vedere [Sys. fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` È il nome del catalogo full-text. *fulltext_catalog_name* viene **sysname**, con un valore predefinito è NULL. Se *fulltext_catalog_name* viene omesso oppure è NULL, vengono restituite tutte le tabelle indicizzate full-text associate al database. Se *fulltext_catalog_name* è specificato, ma *table_name* viene omesso oppure è NULL, viene recuperati le informazioni sugli indici full-text per ogni tabella indicizzata full-text associata al catalogo. Se entrambe *fulltext_catalog_name* e *table_name* vengono specificati, viene restituita una riga se *table_name* associata *fulltext_catalog_name*; in caso contrario, viene generato un errore.  
  
`[ @table_name = ] 'table_name'` È il nome della tabella una o due parti per cui vengono richiesti i metadati full-text. *TABLE_NAME* viene **nvarchar(517)** , con un valore predefinito NULL. Se solo *nome_tabella* è specificato, solo la riga relativa a *table_name* viene restituito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Proprietario della tabella. Corrisponde al nome dell'utente del database che ha creato la tabella.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|Indice che impone il vincolo UNIQUE sulla colonna impostata come colonna chiave univoca.|  
|**FULLTEXT_KEY_COLID**|**int**|ID di colonna dell'indice univoco identificato da FULLTEXT_KEY_NAME.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|Specifica se le colonne contrassegnate per l'indicizzazione full-text nella tabella corrente sono soggette all'esecuzione di query:<br /><br /> 0 = Inattivo<br /><br /> 1 = Attivo|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|Catalogo full-text contenente i dati dell'indice full-text.|  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione vengono assegnate per impostazione predefinita ai membri del ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i nomi delle tabelle indicizzate full-text associate al catalogo full-text `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
