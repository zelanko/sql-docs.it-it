---
title: sp_help_fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_TSQL
- sp_help_fulltext_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs
ms.assetid: 1b94f280-e095-423f-88bc-988c9349d44c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5da958d15c211063165de110d91910e378c940b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983090"
---
# <a name="sphelpfulltextcatalogs-transact-sql"></a>sp_help_fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce l'ID, il nome, la directory radice, lo stato e il numero di tabelle indicizzate full-text per il catalogo full-text specificato.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Usare la [Sys. fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) invece la vista del catalogo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_fulltext_catalogs [ @fulltext_catalog_name = ] 'fulltext_catalog_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` È il nome del catalogo full-text. *fulltext_catalog_name* viene **sysname**. Se questo parametro viene omesso oppure è NULL, vengono restituite informazioni su tutti i cataloghi full-text associati al database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nella tabella seguente viene descritto il set di risultati ordinato in base alla colonna **ftcatid**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|ID del catalogo full-text.|  
|**NAME**|**sysname**|Nome del catalogo full-text.|  
|**PATH**|**nvarchar(260)**|A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], questa clausola non ha alcun effetto.|  
|**STATO**|**int**|Stato di popolamento dell'indice full-text del catalogo:<br /><br /> 0 = inattivo<br /><br /> 1 = popolamento completo in corso<br /><br /> 2 = sospeso<br /><br /> 3 = rallentato<br /><br /> 4 = Recupero in corso<br /><br /> 5 = Chiusura<br /><br /> 6= popolamento incrementale in corso<br /><br /> 7 = compilazione dell'indice in corso<br /><br /> 8 = disco pieno Paused<br /><br /> 9 = rilevamento modifiche<br /><br /> NULL = l'utente non dispone dell'autorizzazione VIEW per il catalogo full-text, il database non è abilitato per la funzionalità full-text oppure il componente full-text non è installato.|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Numero di tabelle indicizzate full-text associate al catalogo|  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione vengono assegnate per impostazione predefinita ai membri del ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni relative al catalogo full-text `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_catalogs 'Cat_Desc' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
