---
title: Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1d6bb42e4b35a74ef2bd6eefb85ea81b0ed18e40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63073846"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria
  Il motore di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è integrato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in modo da consentire la presenza sia di tabelle ottimizzate per la memoria che di tabelle tradizionali basate su disco nello stesso database. Tuttavia, la struttura di archiviazione per le tabelle ottimizzate per la memoria è diversa rispetto alle tabelle basate su disco.  
  
 L'archiviazione per una tabella basata su disco presenta gli attributi chiave seguenti:  
  
-   È stato eseguito il mapping a un filegroup e il filegroup contiene uno o più file.  
  
-   Ogni file è suddiviso in extent di 8 pagine e ogni pagina è 8 KB di dimensioni.  
  
-   Un extent può essere condiviso tra più tabelle, ma esiste un mapping 1 a 1 tra una pagina allocata e la tabella o l'indice. In altri termini, una pagina non può includere righe di due o più tabelle o indici.  
  
-   I dati vengono spostati in memoria (pool di buffer) in base alle esigenze e le pagine appena create o modificate vengono scritte in modo asincrono sul disco generando operazioni IO principalmente casuali.  
  
 L'archiviazione per le tabelle ottimizzate per la memoria presenta gli attributi chiave seguenti:  
  
-   Tutte le tabelle ottimizzate per la memoria vengono eseguito il mapping a un filegroup ottimizzato per la memoria. Il filegroup viene compilato usando il filegroup filestream.  
  
-   Non sono presenti pagine e i dati vengono salvati in modo permanente come riga.  
  
-   Tutte le modifiche apportate alle tabelle ottimizzate per la memoria vengono archiviate aggiungendole ai file attivi. La lettura e la scrittura nei file è sequenziale.  
  
-   Un aggiornamento viene implementato come un'eliminazione seguita da un inserimento. Le righe eliminate non vengono rimosse immediatamente dalla risorsa di archiviazione. Le righe eliminate vengono rimosse da un processo in background, denominato MERGE, in base ai criteri descritti in [Durabilità per tabelle con ottimizzazione per la memoria](memory-optimized-tables.md).  
  
-   A differenza delle tabelle basate su disco, lo spazio di archiviazione per le tabelle ottimizzate per la memoria non è compresso. Quando si esegue la migrazione di una tabella basata su disco (ROW o PAGE) compressa a una tabella ottimizzata per la memoria, è necessario tenere conto della variazione di dimensioni.  
  
-   Una tabella ottimizzata per la memoria può essere durevole o non durevole. È sufficiente configurare l'archiviazione per durabilità memoria tabelle con ottimizzazione per.  
  
 In questa sezione vengono descritte le coppie di file di checkpoint e altri aspetti della modalità di archiviazione dei dati nelle tabelle ottimizzate per la memoria.  
  
 Contenuto della sezione:  
  
-   [Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria](configuring-storage-for-memory-optimized-tables.md)  
  
-   [Filegroup con ottimizzazione per la memoria](the-memory-optimized-filegroup.md)  
  
-   [Durabilità per tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)  
  
-   [Operazione su checkpoint per le tabelle con ottimizzazione per la memoria](checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definizione di durabilità per gli oggetti con ottimizzazione per la memoria](defining-durability-for-memory-optimized-objects.md)  
  
-   [Confronto dell'archiviazione delle tabelle basate su disco con quella delle tabelle con ottimizzazione per la memoria](comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
-   [Monitoraggio e risoluzione di problemi relativi all'unione di coppie di file di dati e differenziali](../../database-engine/monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
