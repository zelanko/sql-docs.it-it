---
title: sp_help_fulltext_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 076a3df69245cb269593e1a2298f18c9266ab217
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980319"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le colonne impostate per l'indicizzazione full-text.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Usare la [Sys. fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) invece la vista del catalogo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @table_name = ] 'table\_name'` È il nome della tabella una o due parti per il quale vengono richieste informazioni di indice full-text. *TABLE_NAME* viene **nvarchar(517)** , con un valore predefinito NULL. Se *table_name* viene omesso, viene recuperati informazioni sulle colonne di indice full-text per ogni tabella indicizzata full-text.  
  
`[ @column_name = ] 'column\_name'` È il nome della colonna per cui vengono richiesti metadati di indice full-text. *column_name* viene **sysname**, con un valore predefinito NULL. Se *column_name* viene omesso oppure è NULL, vengono restituite informazioni di colonna full-text per ogni colonna indicizzata full-text per *table_name*. Se *table_name* anche viene omesso oppure è NULL, vengono restituite informazioni di colonna di indice full-text per ogni colonna indicizzata full-text per tutte le tabelle nel database.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Proprietario della tabella. Corrisponde al nome dell'utente del database che ha creato la tabella.|  
|**TABLE_ID**|**int**|ID della tabella.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|Colonna impostata per l'indicizzazione in una tabella indicizzata full-text.|  
|**FULLTEXT_COLID**|**int**|ID della colonna indicizzata full-text.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Colonna di una tabella indicizzata full-text che specifica il tipo di documento della colonna indicizzata full-text. Questo valore è applicabile solo quando la colonna indicizzata full-text è un **varbinary (max)** oppure **immagine** colonna.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|ID della colonna per il tipo di documento. Questo valore è applicabile solo quando la colonna indicizzata full-text è un **varbinary (max)** oppure **immagine** colonna.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Lingua utilizzata per la ricerca full-text nella colonna.|  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione vengono assegnate per impostazione predefinita ai membri del ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sulle colonne impostate per l'indicizzazione full-text della tabella `Document`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
