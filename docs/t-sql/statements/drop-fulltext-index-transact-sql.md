---
title: DROP FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_INDEX_TSQL
- DROP FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- deleting full-text indexes
- removing full-text indexes
- full-text indexes [SQL Server], removing
- DROP FULLTEXT INDEX statement
- dropping full-text indexes
ms.assetid: 7443a4ab-1d43-4a22-bbba-a07f620892cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 88684e76718c3a16f3949dc3b7cbef04c9e655be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766351"
---
# <a name="drop-fulltext-index-transact-sql"></a>DROP FULLTEXT INDEX (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Rimuove un indice full-text da una tabella o una vista indicizzata specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP FULLTEXT INDEX ON table_name  
```  
  
## <a name="arguments"></a>Argomenti  
 *table_name*  
 Nome della tabella o della vista indicizzata contenente l'indice full-text da rimuovere.  
  
## <a name="remarks"></a>Osservazioni  
 Non è necessario eliminare tutte le colonne dall'indice full-text prima di utilizzare il comando DROP FULLTEXT INDEX.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'utente deve disporre dell'autorizzazione ALTER per la tabella o la vista indicizzata oppure essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** o **db_ddladmin**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato l'indice full-text presente nella tabella `JobCandidate`.  
  
```  
USE AdventureWorks2012;  
GO  
DROP FULLTEXT INDEX ON HumanResources.JobCandidate;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)  
  
  
