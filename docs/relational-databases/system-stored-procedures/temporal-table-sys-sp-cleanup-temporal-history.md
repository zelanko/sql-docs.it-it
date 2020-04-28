---
title: sys. sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 302291ae42fa5fbb2f7dea94ccdb9f659379f5bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74165821"
---
# <a name="syssp_cleanup_temporal_history-transact-sql"></a>sys. sp_cleanup_temporal_history (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

Rimuove tutte le righe dalla tabella di cronologia temporale che corrispondono alla configurazione HISTORY_RETENTION periodo all'interno di una singola transazione.

## <a name="syntax"></a>Sintassi

```
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```

## <a name="arguments"></a>Argomenti

*\@table_name*

Nome della tabella temporale per cui viene richiamata la pulizia della conservazione.

*schema_name*

Nome dello schema a cui appartiene la tabella temporale corrente

*row_count_var* [output]

Parametro di output che restituisce il numero di righe eliminate. Se la tabella di cronologia include un indice columnstore cluster, questo parametro restituirà sempre 0.

## <a name="remarks"></a>Osservazioni

Questa stored procedure può essere usata solo con le tabelle temporali in cui è stato specificato un periodo di conservazione finito.
Usare questa stored procedure solo se è necessario pulire immediatamente tutte le righe obsolete dalla tabella di cronologia. È necessario tenere presente che può avere un impatto significativo sul log del database e sul sottosistema di I/O perché elimina tutte le righe idonee all'interno della stessa transazione.

È sempre consigliabile fare affidamento su un'attività in background interna per la pulizia che rimuove le righe obsolete con l'effetto minimo sui carichi di lavoro normali e sul database in generale.

## <a name="permissions"></a>Autorizzazioni

Richiede autorizzazioni db_owner.

## <a name="example"></a>Esempio

```sql
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="next-steps"></a>Passaggi successivi

[Criteri di conservazione delle tabelle temporali](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
