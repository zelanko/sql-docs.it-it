---
title: Sincronizzare le sottoscrizioni (replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d82ef2a50da415504c2a7c461e652beb7547d501
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772014"
---
# <a name="synchronize-subscriptions-replication"></a>Sincronizzazione delle sottoscrizioni (replica)
  Le sottoscrizioni vengono sincronizzate dagli agenti di replica. L'agente di distribuzione sincronizza le sottoscrizioni di pubblicazioni transazionali e snapshot, mentre l'agente di merge sincronizza le sottoscrizioni di pubblicazioni di tipo merge. Per sincronizzare le sottoscrizioni e controllare il comportamento della sincronizzazione, è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], le stored procedure di replica e gli oggetti RMO (Replication Management Objects). Negli argomenti seguenti viene descritto come sincronizzare le sottoscrizioni e specificare le opzioni di sincronizzazione.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Creazione e applicazione dello snapshot iniziale](create-and-apply-the-initial-snapshot.md)  
  
-   [Creare uno snapshot per una pubblicazione di tipo merge con filtri con parametri](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Abilitare l'inizializzazione con un backup per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [Inizializzare una sottoscrizione transazionale da un backup &#40;programmazione Transact-SQL della replica&#41;](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Inizializzare manualmente una sottoscrizione](initialize-a-subscription-manually.md)  
  
-   [Sincronizzazione di una sottoscrizione pull](synchronize-a-pull-subscription.md)  
  
-   [Sincronizzazione di una sottoscrizione push](synchronize-a-push-subscription.md)  
  
-   [Reinizializzare una sottoscrizione](reinitialize-a-subscription.md)  
  
-   [Eseguire script prima e dopo l'applicazione di uno snapshot &#40;SQL Server Management Studio&#41;](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [Eseguire script durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Visualizzare e risolvere i conflitti di dati per le pubblicazioni di tipo merge &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [Visualizzare i conflitti di dati per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows &#40;Gestione sincronizzazione Microsoft&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [Implementare un gestore della logica di business per un articolo di merge](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Eseguire il debug di un gestore della logica di business &#40;programmazione della replica&#41;](debug-a-business-logic-handler-replication-programming.md)  
  
-   [Controllare il comportamento di trigger e vincoli durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](synchronize-data.md)  
  
  
