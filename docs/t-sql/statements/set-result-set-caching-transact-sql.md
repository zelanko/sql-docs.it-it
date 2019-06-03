---
title: SET RESULT SET CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 0b932c1fa3aa8575f8f12ef5f164841788f74c1a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948743"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Consente ad Azure SQL Data Warehouse di memorizzare nella cache i set di risultati delle query.
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

> [!Note]
> Questa funzionalità viene implementata in tutte le aree. Controllare la versione distribuita per l'istanza in uso e le [note sulla versione di Azure SQL Data Warehouse](/azure/sql-data-warehouse/release-notes-10-0-10106-0) più recenti per la disponibilità delle funzionalità.
  
Questo comando deve essere eseguito mentre si è connessi al database master.  Le modifiche apportate a questa impostazione del database hanno effetto immediato.  La memorizzazione nella cache dei set di risultati delle query prevede l'addebito dei costi di archiviazione. Dopo aver disabilitato la memorizzazione nella cache dei risultati per un database, la cache dei risultati precedentemente salvati in modo permanente verrà immediatamente eliminata dalla risorsa di archiviazione di Azure SQL Data Warehouse. È stata introdotta una nuova colonna denominata is_result_set_caching_on in [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest) per mostrare l'impostazione di memorizzazione nella cache dei risultati per un database.  

**SÌ** Specifica che i set di risultati delle query restituiti da questo database verranno memorizzati nella cache nell'archiviazione di Azure SQL Data Warehouse.

**NO** Specifica che i set di risultati delle query restituiti da questo database non verranno memorizzati nella cache nell'archiviazione di Azure SQL Data Warehouse.

Per stabilire se una query è stata eseguita con un riscontro nella cache o un mancato riscontro nella cache dei risultati, gli utenti possono eseguire una query su [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest) con un ID richiesta specifico. In caso di riscontro nella cache, il risultato della query presenterà un singolo passaggio con i dettagli seguenti:

|**Nome colonna**|**Operatore**|**Value**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Controllo|
|comando|Simile a|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>Autorizzazioni

Richiede le autorizzazioni seguenti:

- Account di accesso entità di livello server (creato dal processo di provisioning) oppure
- Membro del ruolo del database dbmanager.

Il proprietario del database può modificare il database solo se è un membro del ruolo dbmanager.
  
## <a name="examples"></a>Esempi

### <a name="enable-result-set-caching-for-a-database"></a>Abilitare la memorizzazione nella cache dei set di risultati per un database

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>Disabilitare la memorizzazione nella cache dei set di risultati per un database

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>Verificare l'impostazione di memorizzazione nella cache dei set di risultati per un database

```sql
SELECT name, is_result_set_caching  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>Verificare il numero di query con riscontri e mancati riscontri nella cache dei set di risultati

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>Verificare i riscontri o i mancati riscontri nella cache dei set di risultati per una query

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>Verificare tutte le query con riscontri nella cache dei set di risultati

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>Vedere anche

[Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)