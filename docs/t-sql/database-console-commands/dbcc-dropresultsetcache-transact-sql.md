---
title: DBCC DROPRESULTSETCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e0f87333a1767a8d0a618d2afe5097852b7a6dee
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634778"
---
# <a name="dbcc-dropresultsetcache--transact-sql"></a>DBCC DROPRESULTSETCACHE (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Rimuove tutte le voci della cache dei set di risultati da un'istanza del database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] di Azure.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC DROPRESULTSETCACHE
[;]  
```  

## <a name="permissions"></a>Autorizzazioni

Richiede l'appartenenza al ruolo predefinito del server DB_OWNER.

## <a name="remarks"></a>Osservazioni

- Questo comando svuota la cache del set di risultati per tutte le query.  

- Se si disattiva la funzionalità di memorizzazione nella cache dei set di risultati per un database, vengono eliminati anche tutti i risultati memorizzati nella cache.  

- La sospensione di un database per cui è stata abilitata la memorizzazione nella cache del set di risultati non elimina i risultati memorizzati nella cache.  

## <a name="see-also"></a>Vedere anche

[Ottimizzazione delle prestazioni con memorizzazione nella cache dei set di risultati](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC SHOWRESULTCACHESPACEUSED &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
