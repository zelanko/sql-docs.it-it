---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7eee258c997cf6b0aab59b4de158f2e3f35484f4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "77608423"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Rilascia tutte le voci non utilizzate da tutte le cache. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rimuove in background le voci non utilizzate nella cache per liberare memoria per le voci correnti. È tuttavia possibile usare questo comando per rimuovere manualmente le voci inutilizzate da ogni cache o da una cache di pool di Resource Governor specificata.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argomenti  
( 'ALL' [,_pool\_name_ ] )  
ALL specifica tutte le cache supportate.  
_pool\_name_ specifica una cache di pool di Resource Governor. Vengono liberate solo le voci associate a questo pool.  
  
MARK_IN_USE_FOR_REMOVAL  
Libera in modalità asincrona le voci in uso dalle rispettive cache quando non vengono più usate. Dopo l'esecuzione di DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL le nuove voci create nella cache non vengono coinvolte.  
  
NO_INFOMSGS  
Disattiva tutti i messaggi informativi.  
  
## <a name="remarks"></a>Osservazioni  
L'esecuzione di DBCC FREESYSTEMCACHE comporta la cancellazione della cache dei piani per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cancellazione della cache dei piani determina la ricompilazione di tutti i piani di esecuzione successivi e può causare un improvviso peggioramento temporaneo delle prestazioni delle query. Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il messaggio informativo seguente per ogni archivio cache cancellato nella cache dei piani: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha rilevato %d occorrenza/e di scaricamento dell'archivio cache '%s' (parte della cache dei piani) a causa di operazioni 'DBCC FREEPROCCACHE' o 'DBCC FREESYSTEMCACHE'". Questo messaggio viene registrato ogni cinque minuti per tutta la durata dello scaricamento della cache.

## <a name="result-sets"></a>Set di risultati  
DBCC FREESYSTEMCACHE restituisce: "Esecuzione DBCC completata. Se sono stati visualizzati messaggi di errore DBCC, rivolgersi all'amministratore di sistema".
  
## <a name="permissions"></a>Autorizzazioni  
È necessario disporre dell'autorizzazione ALTER SERVER STATE per il server.
  
## <a name="examples"></a>Esempi  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>R. Rilascio delle voci inutilizzate da una cache di pool di Resource Governor  
Nell'esempio seguente viene illustrato come pulire le cache dedicate a un pool di risorse di Resource Governor specificato.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. Rilascio delle voci dalle relative cache non appena tali voci diventano inutilizzate  
Nell'esempio seguente viene utilizzata la clausola MARK_IN_USE_FOR_REMOVAL per rilasciare le voci da tutte le cache correnti non appena le voci diventano inutilizzate.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)
  
  
