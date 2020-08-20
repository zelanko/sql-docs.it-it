---
description: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)
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
ms.openlocfilehash: 813f838e1eae555d28f51a4f799864cc2b2dce15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479778"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Mostra lo spazio di archiviazione usato per la memorizzazione nella cache dei set di risultati per un database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] di Azure.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Osservazioni

Il comando `DBCC SHOWRESULTCACHESPACEUSED` non accetta parametri e restituisce lo spazio usato dal database in cui viene eseguito il comando.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione VIEW SERVER STATE.
  
## <a name="result-sets"></a>Set di risultati  
  
|Colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Spazio totale usato per il database, in KB. Questo numero cambierà con l'aumento del set di risultati memorizzato nella cache.|  
|data_space|bigint|Spazio usato per i dati, in KB.|  
|index_space|bigint|Spazio usato per gli indici, in KB.|  
|unused_space|bigint|Spazio che è parte dello spazio riservato e non usato, in KB.|  

## <a name="see-also"></a>Vedere anche

[Ottimizzazione delle prestazioni con memorizzazione nella cache dei set di risultati](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
