---
title: Operazione su checkpoint per le tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 07560ea0bf147198fb759f6769ae1c6d5c68a71e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050312"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Operazione su checkpoint per le tabelle con ottimizzazione per la memoria
  Un checkpoint deve essere eseguito periodicamente per consentire l'avanzamento dei dati ottimizzati per la memoria nei file di dati e differenziali nella parte attiva del log delle transazioni. Il checkpoint consente il ripristino o il recupero delle tabelle ottimizzate per la memoria all'ultimo checkpoint eseguito correttamente, quindi viene applicata la parte attiva del log delle transazioni per aggiornare le tabelle ottimizzate per la memoria in modo da completare il recupero. L'operazione di checkpoint per le tabelle basate su disco e quella per le tabelle ottimizzate per la memoria sono distinte. Di seguito vengono descritti diversi scenari e viene indicato il comportamento del checkpoint per le tabelle basate su disco e per quelle ottimizzate per la memoria:  
  
## <a name="manual-checkpoint"></a>Checkpoint manuale  
 Quando si crea un checkpoint manuale, il checkpoint per le tabelle basate su disco e per quelle ottimizzate per la memoria viene chiuso. Il file di dati attivo viene chiuso anche se è riempito parzialmente.  
  
## <a name="automatic-checkpoint"></a>Checkpoint automatico  
 Il checkpoint automatico viene implementato in modo diverso per le tabelle basate su disco e per le tabelle ottimizzate per la memoria a causa dei modi diversi in cui i dati sono resi persistenti.  
  
 Per le tabelle basate su disco, viene acquisito un checkpoint automatico in base all'opzione di configurazione dell'intervallo di recupero. Per altre informazioni, vedere [Modificare il tempo di recupero di riferimento di un database &#40;SQL Server&#41;](../logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Per le tabelle ottimizzate per la memoria, viene effettuato un checkpoint automatico quando il file di log delle transazioni diventa più grande di 512 MB dall'ultimo checkpoint. 512 MB include i record del log delle transazioni sia per le tabelle basate su disco che per quelle ottimizzate per la memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti ottimizzati per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
