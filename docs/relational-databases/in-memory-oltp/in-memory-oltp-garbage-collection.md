---
title: Garbage Collection per OLTP in memoria | Microsoft Docs
description: Informazioni sulle Garbage Collection in OLTP in memoria in SQL Server. Se una transazione non più attiva elimina una riga, è soggetta a Garbage Collection.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8784e1fe3f44cd2927ffc1f1a48d51242671051a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537033"
---
# <a name="in-memory-oltp-garbage-collection"></a>Garbage Collection per OLTP in memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Una riga di dati viene considerata non aggiornata se è stata eliminata da una transazione non più attiva. Una riga obsoleta è qualificata per il processo di Garbage Collection. Di seguito sono riportate le caratteristiche del processo di Garbage Collection in [!INCLUDE[hek_2](../../includes/hek-2-md.md)]:  
  
-   Non bloccante. Il processo di Garbage Collection viene distribuito nel tempo con un impatto minimo sul carico di lavoro.  
  
-   Cooperativo. Le transazioni utente partecipano al processo di Garbage Collection con un thread principale di Garbage Collection.  
  
-   Efficiente. Con le transazioni utente vengono scollegate le righe non aggiornate nel percorso di accesso (indice) utilizzato. In questo modo viene ridotto il lavoro richiesto per la rimozione finale della riga.  
  
-   Reattivo. Il numero di richieste di memoria genera operazioni di Garbage Collection aggressive.  
  
-   Scalabile. Dopo il commit, tramite le transazioni utente viene eseguita parte del lavoro di Garbage Collection. Più sono le attività transazionali, più sono numerose le transazioni tramite cui vengono scollegate le righe non aggiornate.  
  
 Il processo di Garbage Collection è controllato dal thread principale di Garbage Collection. Il thread principale di Garbage Collection viene eseguito ogni minuto o quando il numero di transazioni completate supera una soglia interna. L'attività di Garbage Collector è costituita dalle azioni seguenti:  
  
-   Identificare le transazioni tramite cui è stato eliminato o aggiornato un set di righe e viene eseguito il commit prima della transazione attiva meno recente.  
  
-   Identificare le versioni di riga create dalle transazioni precedenti.  
  
-   Raggruppare le righe precedenti in una o più unità di 16 righe ciascuna. Questa attività permette di distribuire il lavoro di Garbage Collector in unità più piccole.  
  
-   Spostare nella coda di Garbage Collection le unità di lavoro per ciascuna utilità di pianificazione. Per informazioni dettagliate, vedere le viste a gestione dinamica (DMV) del Garbage Collector: [sys.dm_xtp_gc_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md), [sys.dm_db_xtp_gc_cycle_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md) e [sys.dm_xtp_gc_queue_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md).  
  
 Dopo il commit di una transazione utente, vengono identificati tutti gli elementi nella coda associati all'utilità di pianificazione in cui è stata eseguita e quindi rilasciata la memoria. Se la coda di Garbage Collection nell'utilità di pianificazione è vuota, viene cercata una coda non vuota nel nodo NUMA corrente. Se l'attività transazionale è scarsa e sono presenti richieste di memoria, tramite il thread principale di Garbage Collection è possibile accedere alle righe di Garbage Collection da qualsiasi coda. Se non esiste alcuna attività transazionale dopo, ad esempio, l'eliminazione di un numero elevato di righe e non vi sono richieste di memoria, le righe eliminate non verranno sottoposte a Garbage Collection fino a quando l'attività transazionale non viene ripresa o non vi sono richieste di memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione della memoria per OLTP in memoria](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)  
  
  
