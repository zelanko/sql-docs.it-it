---
title: Verifiche di coerenza del sistema della tabella temporale | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: ec081d42-57e4-43c7-9e1c-317ba8f23437
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d0957ffb1aa78ee0cbaf3c7c3e5acdb973aa8fb7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165723"
---
# <a name="temporal-table-system-consistency-checks"></a>Verifiche di coerenza del sistema della tabella temporale

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Quando si usano le tabelle temporali, il sistema esegue una serie di verifiche di coerenza per assicurarsi che lo schema sia conforme ai requisiti per le tabelle temporali e che i dati siano coerenti e rimangano tali. Le verifiche temporali sono anche state aggiunte all'istruzione **DBCC CHECKCONSTRAINTS** .

## <a name="system-consistency-checks"></a>Verifiche di coerenza del sistema

Prima di impostare **SYSTEM_VERSIONING** su **ON**, viene eseguita una serie di verifiche sulla tabella di cronologia e sulla tabella corrente. Queste verifiche sono raggruppate in verifiche dello schema e verifiche dei dati (se la tabella di cronologia non è vuota). Il sistema esegue inoltre una verifica della coerenza di runtime.

### <a name="schema-check"></a>Verifica dello schema

Quando si crea o si modifica una tabella affinché diventi una tabella temporale, il sistema verifica che siano soddisfatti i requisiti seguenti:

1. I nomi e il numero di colonne è lo stesso nella tabella corrente e nella tabella di cronologia
2. I tipi di dati corrispondono per ogni colonna tra la tabella corrente e la tabella di cronologia
3. Le colonne periodo sono impostate su **NOT NULL**
4. La tabella corrente include un vincolo di chiave primaria e la tabella di cronologia non dispone di un vincolo di chiave primaria
5. Le colonne **IDENTITY** non sono definite nella tabella di cronologia
6. Nella tabella di cronologia non sono definiti trigger
7. Nella tabella di cronologia non sono definite chiavi esterne
8. Nella tabella di cronologia non sono definiti vincoli di tabella o colonna, tuttavia sono consentiti valori predefiniti delle colonne nella tabella di cronologia
9. La tabella di cronologia non è inserita in un filegroup di sola lettura
10. La tabella di cronologia non è configurata per il rilevamento delle modifiche o per Change Data Capture

### <a name="data-consistency-check"></a>Verifica di coerenza dei dati

Prima di impostare **SYSTEM_VERSIONING** su **ON** e come parte di un'operazione DML, il sistema esegue la verifica seguente: **SysEndTime** ≥**SysStartTime**

Quando si crea un collegamento a una tabella di cronologia esistente, è possibile scegliere di eseguire una verifica della coerenza dei dati. Questa verifica della coerenza dei dati garantisce che i record esistenti non si sovrappongano e che siano soddisfatti i requisiti temporali per ogni singolo record. L'impostazione predefinita prevede l'esecuzione della verifica della coerenza dei dati. È in genere consigliabile eseguire la coerenza dei dati ogni volta che i dati tra le tabelle correnti e di cronologia non sono sincronizzati, ad esempio quando si incorpora una tabella di cronologia esistente popolata con dati cronologici.

> [!WARNING]
> Le modifiche manuali al clock di sistema causeranno un errore imprevisto del sistema poiché le verifiche della coerenza dei dati di runtime apportate per evitare condizioni di sovrapposizione (ossia l'ora di fine di un record non è inferiore all'ora di inizio) avranno esito negativo.

## <a name="dbcc-checkconstraints"></a>DBCC CHECKCONSTRAINTS

Il comando **DBCC CHECKCONSTRAINTS** include verifiche della coerenza dei dati temporali. Per altre informazioni, vedere [DBCC CHECKCONSTRAINTS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md).

## <a name="next-steps"></a>Passaggi successivi

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
- [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerazioni e limitazioni delle tabelle temporali](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Sicurezza di una tabella temporale](../../relational-databases/tables/temporal-table-security.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funzioni e viste per i metadati delle tabelle temporali](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
