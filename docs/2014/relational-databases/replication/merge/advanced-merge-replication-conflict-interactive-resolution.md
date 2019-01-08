---
title: Risoluzione interattiva dei conflitti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7485f840682c6bc8f8140aae6376431ad92442a0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815413"
---
# <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution
  La replica di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre un sistema di risoluzione interattivo che consente di risolvere i conflitti in modo manuale durante la sincronizzazione su richiesta in Gestione sincronizzazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Attivato in fase di esecuzione, il sistema di risoluzione interattivo è un'interfaccia grafica che visualizza i dati relativi a ogni riga in conflitto e offre opzioni per la visualizzazione e la modifica dei dati in conflitto, nonché per la risoluzione distinta dei singoli conflitti.  
  
 Il sistema di risoluzione interattivo presenta alcune analogie con il Visualizzatore conflitti. Nel Visualizzatore conflitti vengono tuttavia visualizzati i risultati dei conflitti già risolti dopo la sincronizzazione di tipo merge, mentre il sistema di risoluzione interattivo visualizza ogni conflitto prima della risoluzione e consente di determinarne l'esito durante la sincronizzazione di tipo merge. È necessario che sia disponibile un utente per il monitoraggio del sistema di risoluzione interattivo in caso di conflitto.  
  
> [!NOTE]  
>  La risoluzione interattiva richiede Gestione sincronizzazione Microsoft Windows. Se una sincronizzazione viene eseguita all'esterno di Gestione sincronizzazione Microsoft Windows (come sincronizzazione pianificata o sincronizzazione su richiesta in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o Monitoraggio replica), i conflitti vengono risolti automaticamente senza richiedere l'intervento dell'utente, in base al sistema di risoluzione specificato per l'articolo. I conflitti a livello di record logici non vengono visualizzati nel sistema di risoluzione interattivo. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../view-conflict-information-for-merge-publications.md).  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>Sistemi di risoluzione dei conflitti di articolo e sistema di risoluzione interattivo  
 I sistemi di risoluzione dei conflitti, ovvero il sistema di risoluzione dei conflitti predefinito, un gestore della logica di business o un sistema personalizzato, vengono assegnati ad articoli specifici durante la creazione di una pubblicazione. Tali sistemi utilizzano un set di regole predefinite per determinare il set di dati che è necessario utilizzare quando si immettono dati di riga in conflitto. Il sistema di risoluzione interattivo non è un sistema di risoluzione dei conflitti distinto con regole per stabilire la modifica che prevale nei conflitti, ma uno strumento da utilizzare in combinazione con i sistemi di risoluzione dei conflitti predefiniti e personalizzati. Il sistema di risoluzione dei conflitti di articolo determina la riga confermata e la riga non confermata e il sistema di risoluzione interattivo consente all'utente di accettare, rifiutare o modificare i risultati.  
  
 Per utilizzare il sistema di risoluzione interattivo, è necessario che la risoluzione interattiva sia attivata per ogni articolo e sottoscrizione che la richiede. Dopo essere stato abilitato per uno o più articoli e sottoscrizioni, il sistema di risoluzione interattivo viene utilizzato quando viene rilevato un conflitto durante la sincronizzazione di tipo merge.  
  
 Per usare il sistema di risoluzione dei conflitti interattivo , vedere [Specificare la risoluzione interattiva dei conflitti per articoli di merge](../publish/specify-interactive-conflict-resolution-for-merge-articles.md) e [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows &#40;Gestione sincronizzazione Microsoft Windows&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
