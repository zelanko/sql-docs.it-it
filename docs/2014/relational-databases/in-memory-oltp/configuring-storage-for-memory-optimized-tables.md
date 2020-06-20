---
title: Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d2a487354f9cebf8f957f49d065a8d32ce109a0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050263"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configurazione dell'archiviazione per le tabelle con ottimizzazione per la memoria
  È necessario configurare la capacità di archiviazione e le operazioni di input/output al secondo (IOPS).  
  
## <a name="storage-capacity"></a>Capacità di archiviazione  
 Usare le informazioni in [Stimare i requisiti di memoria delle tabelle ottimizzate per la memoria](memory-optimized-tables.md) per stimare le dimensioni in memoria delle tabelle ottimizzate per la memoria durevoli del database. Poiché gli indici non vengono mantenuti per le tabelle ottimizzate per la memoria, non includere le dimensioni degli indici. Una volta determinata la dimensione, è necessario fornire uno spazio libero su disco quattro volte superiore alla dimensione delle tabelle in memoria durevoli.  
  
## <a name="storage-performance"></a>Prestazioni di archiviazione  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] consente di aumentare notevolmente la velocità effettiva del carico di lavoro. Pertanto, è importante verificare che le operazioni di IO non rappresentino un collo di bottiglia.  
  
-   Quando si esegue la migrazione delle tabelle basate su disco nelle tabelle ottimizzate per la memoria, verificare che il log delle transazioni sia in un supporto di archiviazione che supporti l'attività aumentata del log delle transazioni. Ad esempio, se il supporto di archiviazione supporta le operazioni del log delle transazioni a 100 MB/sec e le tabelle ottimizzate per la memoria restituiscono prestazioni cinque volte superiori, anche il supporto di archiviazione del log delle transazioni deve essere in grado di supportare un incremento di cinque volte delle prestazioni, per impedire all'attività del log delle transazioni di diventare un collo di bottiglia.  
  
-   Le tabelle con ottimizzazione per la memoria sono persistenti nei file distribuiti in uno o più contenitori. In genere è necessario eseguire il mapping al proprio spindle di ogni contenitore, che viene usato per aumentare la capacità di archiviazione e migliorare le prestazioni. È necessario assicurarsi che gli IOPS sequenziali del supporto di archiviazione possano supportare un aumento di 3 volte nella velocità effettiva del log delle transazioni.  
  
     Ad esempio, se le tabelle ottimizzate per la memoria generano 500MB/sec di attività nel log delle transazioni, l'archiviazione per le tabelle ottimizzate per la memoria deve supportare 1,5 GB/sec. La necessità di supportare un aumento di 3 volte nella velocità effettiva del log delle transazioni deriva dall'osservazione che le coppie di file di dati e differenziali vengono prima scritti con i dati iniziali e quindi devono essere letti/riscritti come parte di un'operazione di merge.  
  
     Un altro fattore per stimare la velocità effettiva per l'archiviazione è il tempo di recupero per le tabelle ottimizzate per la memoria. I dati delle tabelle durevoli devono essere letti in memoria prima che un database viene reso disponibile alle applicazioni. In genere, il caricamento dei dati nelle tabelle ottimizzate per la memoria può essere eseguito alla velocità delle operazioni di IOPS. Pertanto se l'archiviazione totale per le tabelle ottimizzate per la memoria durevoli è di 60 GB e si desidera essere in grado di caricare i dati in 1 minuto, le operazioni di IOPS per l'archiviazione devono essere impostati su 1 GB/sec.  
  
-   Se si dispone di un numero pari di spindle, è necessario creare due volte il numero dei contenitori, eseguendo per ogni coppia il mapping allo stesso spindle. Ciò è necessario per ripartire le operazioni di IOPS e l'archiviazione. Per ulteriori informazioni, vedere [il filegroup con ottimizzazione per la memoria](the-memory-optimized-filegroup.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
