---
title: 'Lezione 3: Sincronizzazione della sottoscrizione con la pubblicazione di tipo merge | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 847b833d793d3b572b44bcb77903c534300109b7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721004"
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>Lezione 3: Sincronizzazione della sottoscrizione con la pubblicazione di tipo merge
  In questa lezione verrà avviato l'agente di merge per inizializzare la sottoscrizione con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È inoltre necessario eseguire questa procedura per la sincronizzazione con il server di pubblicazione. Per eseguire questa lezione è necessario aver completato la lezione precedente [Lezione 2: Creazione di una sottoscrizione per una pubblicazione di tipo merge](lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Per avviare la sincronizzazione e inizializzare la sottoscrizione  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere il nodo del server e quindi espandere la cartella **Replica** .  
  
2.  Nella cartella **Sottoscrizioni locali** fare clic con il pulsante destro del mouse sulla sottoscrizione nel database **SalesOrdersReplica** e quindi scegliere **Visualizza stato sincronizzazione**.  
  
3.  Fare clic su **Avvia** per inizializzare la sottoscrizione.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo è stato eseguito l'agente di merge per l'avvio della sincronizzazione e l'inizializzazione della sottoscrizione. È anche possibile inserire, aggiornare o eliminare dati nelle tabelle **SalesOrderHeader** o **SalesOrderDetail** nel server di pubblicazione o nel Sottoscrittore, ripetere questa procedura quando è disponibile la connettività di rete per sincronizzare i dati tra il server di pubblicazione e il Sottoscrittore e quindi eseguire query nelle tabelle **SalesOrderHeader** o **SalesOrderDetail** nell'altro server per visualizzare le modifiche replicate.  
  
 Questa lezione completa l'esercitazione Replica di dati con client mobili. Per un'esercitazione simile che usa la replica transazionale, vedere [Esercitazione: Replica di dati tra server con connessione continua](tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Sincronizzare i dati](synchronize-data.md)   
 [Sincronizzare una sottoscrizione pull](synchronize-a-pull-subscription.md)  
  
  
