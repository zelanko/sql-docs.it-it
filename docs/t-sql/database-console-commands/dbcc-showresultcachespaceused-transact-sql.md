---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: c2dd0389f4ec3287fbe23875458ab5d34ef269f7
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2019
ms.locfileid: "72174655"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Mostra lo spazio di archiviazione usato per la memorizzazione nella cache dei set di risultati per un database [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] di Azure.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Remarks

Il comando `DBCC SHOWRESULTCACHESPACEUSED` non accetta parametri e restituisce lo spazio usato dal database in cui viene eseguito il comando.

Le dimensioni massime della cache dei set di risultati sono pari a 1 TB per ogni database.  Azure SQL Data Warehouse rimuove automaticamente le voci nella cache dei set di risultati:

- Ogni 48 ore se il set di risultati non è stato usato.
- Quando la cache dei set di risultati sta per raggiungere le dimensioni massime.

Per svuotare manualmente la cache dei set di risultati per un database, gli utenti possono usare una delle opzioni seguenti:

- Disattivare la funzionalità di memorizzazione nella cache dei set di risultati per il database
- Eseguire `DBCC DROPRESULTSETCACHE` mentre si è connessi al database 

La sospensione di un database non svuoterà la cache dei set di risultati.  

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione VIEW SERVER STATE.
  
## <a name="result-sets"></a>Set di risultati  
  
|colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Spazio totale usato per il database, in KB. Questo numero cambierà con l'aumento del set di risultati memorizzato nella cache.|  
|data_space|BIGINT|Spazio usato per i dati, in KB.|  
|index_space|BIGINT|Spazio usato per gli indici, in KB.|  
|unused_space|BIGINT|Spazio che è parte dello spazio riservato e non usato, in KB.|  


## <a name="see-also"></a>Vedere anche

[Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)