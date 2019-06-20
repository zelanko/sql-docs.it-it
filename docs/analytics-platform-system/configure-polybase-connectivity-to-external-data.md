---
title: Configurare la connettività di PolyBase - sistema di piattaforma Analitica | Microsoft Docs
description: Viene illustrato come configurare PolyBase in Parallel Data Warehouse, per connettersi a Hadoop o in Microsoft Azure storage blob origini dati esterne. Usare PolyBase per eseguire query che si integrano dati da più origini, inclusi Hadoop, archiviazione blob di Azure e Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057814"
---
# <a name="what-is-polybase"></a>Che cos'è PolyBase?
PolyBase consente il sistema di piattaforma Analitica (AP) per elaborare query Transact-SQL che può leggere i dati da e scrivere dati in origini dati esterne. Le stesse query che accedono ai dati esterni possono anche includere tabelle relazioni in punti di accesso. In questo modo è possibile combinare dati provenienti da origini esterne con dati relazionali di alto valore nei database di punti di accesso.

![Logica PolyBase](media/polybase/polybase-logical.png)

PolyBase sui punti di accesso supporta la lettura e scrittura al file system Hadoop (HDFS) e archiviazione Blob di Azure. PolyBase ha anche la possibilità di eseguire il push di un'attività di calcolo in nodi di Hadoop come processi mapreduce per ottimizzare le prestazioni complessive delle query. PolyBase sui punti di accesso può operare su testo delimitato, ORC e Parquet file. Visualizzare [What ' s PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) per una descrizione completa e le relative funzionalità.

> [!NOTE]
> I punti di accesso attualmente supporta solo standard utilizzo generico v1 con ridondanza locale (LRS) Azure Blob Storage.

## <a name="features-and-limitations"></a>Funzionalità e limitazioni
Visualizzare [le funzionalità e limitazioni di](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) per un riepilogo di PolyBase presenta limitazioni note e disponibili per i punti di accesso e altri prodotti di SQL Server.

> [!NOTE] 
> Il resto di PolyBase correlati descibe articoli sulla configurazione di PolyBase in APS 2016 (AU6) e versioni successive.

## <a name="see-also"></a>Vedere anche
- [Hadoop](polybase-configure-hadoop.md)
- [Archiviazione BLOB di Azure](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
