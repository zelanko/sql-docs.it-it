---
title: Introduzione alle tabelle temporali con controllo delle versioni di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 725dbc3306f9ad9616b5cbeca2d96249dca1c4a8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165779"
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>Introduzione alle tabelle temporali con controllo delle versioni di sistema

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

A seconda dello scenario, è possibile creare nuove tabelle temporali con controllo delle versioni di sistema o modificare quelli esistenti aggiungendo attributi temporali allo schema della tabella esistente. Quando i dati nella tabella temporale vengono modificati, il sistema compila la cronologia delle versioni in modo trasparente per le applicazioni e gli utenti finali. Di conseguenza, l'uso delle tabelle temporali con controllo delle versioni di sistema non richiede cambiamenti relativi alle modalità di modifica della tabella o alle modalità di query dello stato più recente (effettivo) dei dati.

Oltre ai normali DML e alle query, la tabella temporale fornisce anche metodi semplici e pratici per ottenere informazioni approfondite dalla cronologia dei dati grazie alla sintassi Transact-SQL estesa. A ogni tabella con controllo delle versioni di sistema è assegnata una tabella di cronologia, che però è completamente trasparente per gli utenti a meno che non vogliano ottimizzare le prestazioni del carico di lavoro o il footprint di memoria creando altri indici o scegliendo opzioni di archiviazione diverse.

Il diagramma seguente illustra un flusso di lavoro tipico con le tabelle temporali con controllo delle versioni di sistema: ![Introduzione alle tabelle temporali](../../relational-databases/tables/media/getting-started-with-temporal.png "Introduzione alle tabelle temporali")

L'argomento è suddiviso nelle cinque sezioni seguenti:

- [Creazione di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [Modifica dei dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Modifica dello schema di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Arresto del controllo delle versioni di sistema in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)

## <a name="next-steps"></a>Passaggi successivi

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
- [Verifiche di coerenza del sistema della tabella temporale](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Considerazioni e limitazioni delle tabelle temporali](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Sicurezza di una tabella temporale](../../relational-databases/tables/temporal-table-security.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Funzioni e viste per i metadati delle tabelle temporali](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
