---
title: Funzioni e viste per i metadati delle tabelle temporali | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e5d23ec9-7d18-40f6-add4-bea13132d0b9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68b5a453aced3f456156300e9768812ed3072a15
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "85982703"
---
# <a name="temporal-table-metadata-views-and-functions"></a>Funzioni e viste per i metadati delle tabelle temporali

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] includono alcune viste e funzioni per i metadati che permettono agli amministratori di recuperare informazioni sulle tabelle temporali.

Le informazioni sulle tabelle temporali vengono esposte nelle viste dei metadati seguenti:

- [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)
- [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)
- [sys.periods &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-periods-transact-sql.md)

 Le informazioni sulle tabelle temporali vengono esposte nelle funzioni per i metadati seguenti:

- [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)

- [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)

- [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)

## <a name="next-steps"></a>Passaggi successivi

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
- [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Verifiche di coerenza del sistema della tabella temporale](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerazioni e limitazioni delle tabelle temporali](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Sicurezza di una tabella temporale](../../relational-databases/tables/temporal-table-security.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
