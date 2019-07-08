---
title: Uso di una tabella temporale con controllo delle versioni di sistema e ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 532bc2d22e7499a5e5d7a1804a1b89262fcf17a7
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412989"
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>Utilizzo di una tabella temporale con controllo delle versioni di sistema e ottimizzazione per la memoria

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Questo argomento illustra in che modo l'utilizzo di una tabella temporale ottimizzata per la memoria con controllo delle versioni di sistema è diverso dall'utilizzo di una tabella temporale con controllo delle versioni di sistema basata su disco.

> [!NOTE]
> L'uso di tabelle temporali con ottimizzazione per la memoria è applicabile solo a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e non a [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].

## <a name="discovering-metadata"></a>Individuazione dei metadati

Per trovare i metadati relativi a una tabella temporale ottimizzata per la memoria con controllo delle versioni di sistema, è necessario combinare informazioni provenienti da [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) e [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md). Una tabella temporale con controllo delle versioni di sistema viene presentata come parent_object_id della tabella di cronologia in memoria interna

Questo esempio mostra come eseguire una query e creare un join di tali tabelle.

```sql
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema
    , OBJECT_NAME(IT.parent_object_id) as TemporalTableName
    , T1.object_id as TemporalTableObjectId
    , IT.Name as InternalHistoryStagingName
    , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema
    , OBJECT_NAME (T1.history_table_id) as HistoryTableName
FROM sys.internal_tables IT
JOIN sys.tables T1
    ON IT.parent_object_id = T1.object_id
JOIN sys.tables T2
    ON T1.history_table_id = T2.object_id
WHERE T1.is_memory_optimized = 1 AND T1.temporal_type = 2

```

## <a name="modifying-data"></a>Modifica dei dati

È possibile modificare le tabelle temporali ottimizzate per la memoria attraverso le stored procedure compilate in modo nativo, che consentono di convertire le tabelle non temporali ottimizzate per la memoria in tabelle con controllo delle versioni e mantenere le stored procedure compilate in modo nativo.

Questo esempio mostra in che modo è possibile modificare una tabella creata in precedenza in un modulo compilato in modo nativo.

```sql
CREATE PROCEDURE dbo.UpdateFXCurrencyPair
   (
      @ProviderID int
      , @CurrencyID1 int
      , @CurrencyID2 int
      , @BidRate decimal(8,4)
      , @AskRate decimal(8,4)
   )
WITH NATIVE_COMPILATION, SCHEMABINDING
   , EXECUTE AS OWNER
AS
   BEGIN ATOMIC WITH
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate = @BidRate
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2
END
GO ;

```

## <a name="see-also"></a>Vedere anche

- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Creazione di una tabella temporale con controllo delle versioni di sistema e ottimizzazione per la memoria](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [Monitoraggio di una tabella temporale con controllo delle versioni di sistema e ottimizzazione per la memoria](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [Considerazioni sulle prestazioni con le tabelle temporali con controllo delle versioni di sistema e ottimizzazione per la memoria](../../relational-databases/tables/
- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
- [Verifiche di coerenza del sistema della tabella temporale](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funzioni e viste per i metadati delle tabelle temporali](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
