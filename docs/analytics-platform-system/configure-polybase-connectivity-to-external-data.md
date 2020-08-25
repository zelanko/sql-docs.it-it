---
title: Configurare la connettività di base
description: Viene illustrato come configurare la polibase in parallelo data warehouse per connettersi a origini dati BLOB di archiviazione Hadoop o Microsoft Azure esterni. Usare la polibase per eseguire query che integrano i dati da più origini, tra cui Hadoop, archiviazione BLOB di Azure e data warehouse parallele.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 98527bf770da61c98368171e75b3a9b82ceba13c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767180"
---
# <a name="configure-polybase-connectivity"></a>Configurare la connettività di base
La polibase consente al sistema di piattaforma di analisi (APS) di elaborare query Transact-SQL in grado di leggere e scrivere dati in origini dati esterne. Le stesse query che accedono a dati esterni possono includere anche tabelle di relazioni nei punti di accesso. In questo modo è possibile combinare dati da origini esterne con dati relazionali di valore elevato nei database APS.

![Logica di PolyBase](media/polybase/polybase-logical.png)

La polibase su APS supporta la lettura e la scrittura in Hadoop (HDFS) file system e nell'archiviazione BLOB di Azure. La funzione polibase è inoltre in grado di eseguire il push di alcuni calcoli nei nodi Hadoop come processi MapReduce per ottimizzare le prestazioni complessive delle query. La funzione di base su APS può funzionare su file di testo, ORC e parquet delimitati. Per una descrizione completa e le relative funzionalità, vedere [che cos'è](../relational-databases/polybase/polybase-guide.md) la funzione di base.

> [!NOTE]
> APS supporta attualmente solo l'archiviazione BLOB di Azure con ridondanza locale (con ridondanza locale) standard per utilizzo generico.

## <a name="features-and-limitations"></a>Funzionalità e limitazioni
Vedere [funzionalità e limitazioni](../relational-databases/polybase/polybase-versioned-feature-summary.md) per un riepilogo delle funzionalità di polibase disponibili e limitazioni note su APS e altri prodotti SQL Server.

> [!NOTE] 
> Il resto degli articoli correlati alla polibase descibe come configurare la polibase in APS 2016 (AU6) e versioni successive.

## <a name="see-also"></a>Vedere anche
- [Hadoop](polybase-configure-hadoop.md)
- [Archiviazione BLOB di Azure](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
