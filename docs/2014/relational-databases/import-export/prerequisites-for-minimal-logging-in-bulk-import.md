---
title: Prerequisiti per la registrazione minima nell'importazione bulk | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ccb9642982b8680e4111346298e7a70bbc606dbb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011893"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Prerequisiti per la registrazione minima nell'importazione bulk
  Per un database con modello di recupero con registrazione completa, tutte le operazioni di inserimento di righe eseguite durante l'importazione bulk vengono registrate in modo completo nel log delle transazioni. In caso di importazioni di grandi quantità di dati, l'utilizzo del modello di recupero con registrazione completa può causare un rapido esaurimento dello spazio disponibile nel log. Nel caso si utilizzi un modello di recupero con registrazione minima o un modello di recupero con registrazione minima delle operazioni bulk invece, la registrazione minima delle operazioni di importazione bulk riduce la possibilità che un'operazione di questo tipo esaurisca lo spazio nel log. La registrazione minima inoltre è più efficiente di quella completa.  
  
> [!NOTE]  
>  Il modello di recupero con registrazione minima delle operazioni bulk è progettato per sostituire temporaneamente il modello di recupero con registrazione completa durante le operazioni bulk di notevoli dimensioni.  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>Requisiti della tabella per la registrazione minima di operazioni di importazione bulk  
 La registrazione minima richiede che la tabella di destinazione soddisfi le condizioni seguenti:  
  
-   La tabella di destinazione non viene replicata.  
  
-   Il blocco di tabella è specificato (utilizzando TABLOID).  
  
    > [!NOTE]  
    >  Sebbene gli inserimenti di dati non vengano registrati nel log delle transazioni quando viene eseguita un'importazione bulk con registrazione minima, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] vengono registrate le allocazioni degli extent per ogni nuovo extent allocato alla tabella.  
  
-   Questa non è una tabella ottimizzata per la memoria.  
  
 La registrazione minima in una tabella dipende inoltre dal fatto che la tabella sia indicizzata e, in tal caso, dal fatto che sia vuota:  
  
-   Se la tabella non include indici, le pagine di dati vengono registrate tramite registrazione minima.  
  
-   Se la tabella non include indici cluster ma uno o più indici non cluster, le pagine di dati vengono sempre registrate con registrazione minima. La modalità di registrazione delle pagine di indice, tuttavia, dipende dal fatto che la tabella sia o meno vuota:  
  
    -   Se la tabella è vuota, le pagine di indice vengono registrate tramite registrazione minima.  
  
    -   Se la tabella non è vuota, le pagine di indice vengono registrate tramite registrazione completa.  
  
        > [!NOTE]  
        >  Se si parte da una tabella vuota e si esegue l'importazione bulk dei dati in più batch, per il primo batch le pagine di indice e di dati vengono registrate con registrazione minima. A partire dal secondo batch, tuttavia, la registrazione minima viene applicata solo alle pagine di dati.  
  
-   Se la tabella include un indice cluster ed è vuota, le pagine di dati e di indice vengono registrate tramite registrazione minima. Se, invece, una tabella include un indice cluster e non è vuota, le pagine di dati e di indice vengono registrate con registrazione completa indipendentemente dal modello di recupero.  
  
    > [!NOTE]  
    >  Se si parte da una tabella vuota e si esegue l'importazione bulk dei dati in batch, per il primo batch le pagine di indice e di dati vengono registrate con registrazione minima. A partire dal secondo batch, tuttavia, la registrazione minima viene applicata solo alle pagine di dati.  
  
> [!NOTE]  
>  Quando la replica transazionale è abilitata, le operazioni BULK INSERT vengono registrate completamente persino nel modello di recupero con registrazione minima delle operazioni bulk.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  

  
## <a name="see-also"></a>Vedere anche  
 [Modelli di recupero &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
