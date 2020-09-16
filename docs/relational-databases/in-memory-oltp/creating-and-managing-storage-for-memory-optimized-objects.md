---
title: Creare e gestire l'archiviazione - oggetti con ottimizzazione per la memoria
description: Informazioni sugli attributi delle tabelle ottimizzate per la memoria e delle tabelle basate su disco. Usare queste risorse per creare e gestire l'archiviazione per gli oggetti con ottimizzazione per la memoria.
ms.custom: seo-dt-2019
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d6c12e45c920abcb8b3284be8d60c07d645c61b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89519608"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Il motore di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è integrato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in modo da consentire la presenza sia di tabelle ottimizzate per la memoria che di tabelle tradizionali basate su disco nello stesso database. Tuttavia, la struttura di archiviazione per le tabelle ottimizzate per la memoria è diversa rispetto alle tabelle basate su disco.  
  
 L'archiviazione per una tabella basata su disco presenta gli attributi chiave seguenti:  
  
-   È stato eseguito il mapping a un filegroup e il filegroup contiene uno o più file.  
  
-   Ogni file è suddiviso in extent di 8 pagine e ogni pagina è 8 KB di dimensioni.  
  
-   Un extent può essere condiviso tra più tabelle, ma esiste un mapping 1 a 1 tra una pagina allocata e la tabella o l'indice. In altri termini, una pagina non può includere righe di due o più tabelle o indici.  
  
-   I dati vengono spostati in memoria (pool di buffer) in base alle esigenze e le pagine appena create o modificate vengono scritte in modo asincrono sul disco generando operazioni IO principalmente casuali.  
  
 L'archiviazione per le tabelle ottimizzate per la memoria presenta gli attributi chiave seguenti:  
  
-   Tutte le tabelle ottimizzate per la memoria sono mappate a un filegroup di dati ottimizzato per la memoria. Questo filegroup usa sintassi e semantica simili a Filestream.  
  
-   Non sono presenti pagine e i dati vengono salvati in modo permanente come riga.  
  
-   Tutte le modifiche apportate alle tabelle ottimizzate per la memoria vengono archiviate aggiungendole ai file attivi. La lettura e la scrittura nei file è sequenziale.  
  
-   Un aggiornamento viene implementato come un'eliminazione seguita da un inserimento. Le righe eliminate non vengono rimosse immediatamente dalla risorsa di archiviazione. Le righe eliminate vengono rimosse da un processo in background, denominato MERGE, in base ai criteri descritti in [Durabilità per tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md).  
  
-   A differenza delle tabelle basate su disco, lo spazio di archiviazione per le tabelle ottimizzate per la memoria non è compresso. Quando si esegue la migrazione di una tabella basata su disco (ROW o PAGE) compressa a una tabella ottimizzata per la memoria, è necessario tenere conto della variazione di dimensioni.  
  
-   Una tabella ottimizzata per la memoria può essere durevole o non durevole. È sufficiente configurare l'archiviazione per le tabelle ottimizzate per la memoria durevoli.  
  
 In questa sezione vengono descritte le coppie di file di checkpoint e altri aspetti della modalità di archiviazione dei dati nelle tabelle ottimizzate per la memoria.  
  
 Contenuto della sezione:  
  
-   [Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/configuring-storage-for-memory-optimized-tables.md)  
  
-   [Filegroup con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
-   [Durabilità per tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)  
  
-   [Operazione su checkpoint per le tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definizione di durabilità per gli oggetti con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
-   [Confronto dell'archiviazione delle tabelle basate su disco con quella delle tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
