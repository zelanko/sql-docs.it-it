---
description: SET RESULT_SET_CACHING (Transact-SQL)
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f8247062993b33a669477be7d71363efa45ead32
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670547"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Controlla il comportamento di memorizzazione nella cache del set di risultati per la sessione client corrente.  

Si applica al [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi

```syntaxsql
SET RESULT_SET_CACHING { ON | OFF };
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>Osservazioni  

Eseguire questo comando durante la connessione al database utente per il quale si vuole configurare l'impostazione result_set_caching.

**ON**   
Abilita la memorizzazione nella cache del set di risultati per la sessione client corrente.  Non è possibile impostare la memorizzazione nella cache del set di risultati su ON per una sessione se è impostata su OFF a livello del database.

**OFF**   
Disabilita la memorizzazione nella cache del set di risultati per la sessione client corrente.

## <a name="examples"></a>Esempi

Eseguire una query sulla colonna result_cache_hit in [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) con request_id di una query per verificare se la query è stata eseguita con riscontro o meno nella cache dei risultati.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>Autorizzazioni

È richiesta l'appartenenza al ruolo public

## <a name="see-also"></a>Vedere anche

- [Ottimizzazione delle prestazioni con memorizzazione nella cache dei set di risultati](/azure/sql-data-warehouse/performance-tuning-result-set-caching)
- [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest&preserve-view=true)
- [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest&preserve-view=true)
- [DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
- [DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
