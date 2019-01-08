---
title: Backup di un database con tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bc4da6702716e845121d2081a166254d4be9449f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408628"
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>Backup di un database con tabelle con ottimizzazione per la memoria
  Il backup delle tabelle con ottimizzazione per la memoria viene eseguito durante i normali backup di database. Per le tabelle basate su disco, il CHECKSUM di coppie di file di dati e file differenziali viene convalidato durante il backup del database per rilevare eventuali danneggiamenti di archiviazione.  
  
> [!NOTE]  
>  Durante il backup, se viene rilevato un errore di CHECKSUM in uno o più file in un filegroup ottimizzato per la memoria, non sarà possibile ripristinare e riavviare il database. In tal caso, è necessario ripristinare il database dall'ultima copia di backup valida nota. Se non è disponibile un backup, è possibile esportare i dati dalle tabelle ottimizzate per la memoria e dalle tabelle basate su disco e ricaricarli dopo aver eliminato e ricreato il database.  
  
 Un backup completo di un database con una o più tabelle ottimizzate per la memoria è costituito dall'archiviazione allocata per le tabelle basate su disco (se presente), dal log delle transazioni attivo e dalle coppie di file di dati e file differenziali (anche note come coppie di file di checkpoint) per le tabelle ottimizzate per la memoria. Tuttavia, come illustrato in [Durabilità per tabelle ottimizzate per la memoria](memory-optimized-tables.md), le dimensioni di archiviazione usate per le tabelle ottimizzate per la memoria possono essere di gran lunga superiori rispetto alle relative dimensioni in memoria e influiscono sulle dimensioni del backup del database.  
  
## <a name="full-database-backup"></a>Backup completo del database  
 L'attenzione di questa discussione verrà posta sui backup di database per i database con solo tabelle ottimizzate per la memoria durevoli, dal momento che il backup per le tabelle basate su disco è lo stesso. Le coppie di file di checkpoint nel filegroup ottimizzato per la memoria possono trovarsi in vari stati. Nella tabella seguente vengono descritte le parti dei file di cui viene eseguito il backup.  
  
|Stato della coppia di file di checkpoint|Backup|  
|--------------------------------|------------|  
|PRECREATED|Solo metadati del file|  
|UNDER CONSTRUCTION|Solo metadati del file|  
|Attiva|Metadati del file più i byte utilizzati|  
|MERGE SOURCE|Metadati del file più i byte utilizzati|  
|MERGE TARGET|Solo metadati del file|  
|REQUIRED FOR BACKUP/HA|Metadati del file più i byte utilizzati|  
|IN TRANSITION TO TOMBSTONE|Solo metadati del file|  
|TOMBSTONE|Solo metadati del file|  
  
 Le dimensioni dei backup del database con una o più tabelle ottimizzate per la memoria sono in genere maggiori delle relative dimensioni in memoria ma inferiori all'archiviazione su disco. Le dimensioni aggiuntive dipendono dal numero di righe eliminate e dal numero di coppie di file di checkpoint negli stati MERGE SOURCE e REQUIRED FOR BACKUP/HA che dipendono indirettamente dal carico di lavoro. Per descrizioni degli stati delle coppie di file di checkpoint, vedere [DM db_xtp_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql).  
  
### <a name="estimating-size-of-full-database-backup"></a>Stima delle dimensioni di un backup completo del database  
  
> [!IMPORTANT]  
>  Si consiglia di non usare il valore BackupSizeInBytes per stimare la dimensione del backup per OLTP in memoria.  
  
 Il primo scenario di carico di lavoro è relativo (principalmente) all'operazione di inserimento. In questo scenario, la maggior parte dei file di dati si trova nello stato Attivo, è completamente caricata e con pochissime righe eliminate. Le dimensioni del backup del database si avvicineranno a quelle dei dati in memoria.  
  
 Il secondo scenario di carico di lavoro è per le operazioni di inserimento, eliminazione e aggiornamento frequenti: Nel peggiore dei casi, tutte le coppie di file del checkpoint sono caricate al 50% dopo aver tenuto conto delle righe eliminate. Pertanto, le dimensioni del backup del database saranno di almeno 2 volte quelle dei dati in memoria. Inoltre, saranno poche le coppie di file di checkpoint negli stati MERGE SOURCE e Required for backup/high availability che verranno aggiunte alle dimensioni del backup del database.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>Backup differenziali di database con tabelle con ottimizzazione per la memoria  
 Lo spazio di archiviazione per le tabelle ottimizzate per la memoria è costituito da file di dati e differenziali come descritto in [Durabilità per tabelle ottimizzate per la memoria](memory-optimized-tables.md). Il backup differenziale di un database con tabelle ottimizzate per la memoria contiene i dati seguenti:  
  
-   Il backup differenziale per i filegroup che archiviano le tabelle basate su disco non è interessato dalla presenza di tabelle ottimizzate per la memoria.  
  
-   Il log delle transazioni attivo è uguale a quello di un backup completo del database.  
  
-   Per un filegroup di dati ottimizzato per la memoria, il backup differenziale utilizza lo stesso algoritmo di un backup completo del database per identificare i file di dati e differenziali per il backup, ma filtra quindi il subset di file nel modo seguente:  
  
    -   Un file di dati contiene le righe appena inserite e, quando è pieno, viene chiuso e contrassegnato in sola lettura. Il backup di un file di dati viene eseguito solo il file è stato chiuso dopo l'ultimo backup completo del database. Con i backup differenziali viene eseguito solo il backup dei file di dati contenenti le righe inserite dopo l'ultimo backup completo del database ad eccezione di uno scenario di aggiornamento ed eliminazione in cui è possibile che alcune righe inserite siano già state contrassegnate per il processo di Garbage Collection o sottoposte a Garbage Collection.  
  
    -   In un file differenziale sono archiviati i riferimenti alle righe di dati eliminate. Poiché qualsiasi futura transazione può eliminare una riga, è possibile modificare un file differenziale in qualsiasi momento nell'arco della sua durata, non viene mai chiuso. Viene sempre eseguito il backup di un file differenziale. I file differenziali in genere utilizzano meno del 10% dello spazio di archiviazione, pertanto tali file hanno un impatto minimo sulle dimensioni del backup differenziale.  
  
 Se le tabelle ottimizzate per la memoria costituiscono una parte significativa delle dimensioni del database, il backup differenziale può ridurre notevolmente le dimensioni del backup del database.  
  
 Per i carichi di lavoro tipici OLTP, i backup differenziali saranno molto più piccoli dei backup completi del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](restore-and-recovery-of-memory-optimized-tables.md)  
  
  
