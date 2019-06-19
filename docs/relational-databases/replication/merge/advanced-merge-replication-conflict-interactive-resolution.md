---
title: Risoluzione interattiva dei conflitti | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 20c748e6dea95ae06c2f0c8364b8720ca0d7a36a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640107"
---
# <a name="advanced-merge-replication-conflict---interactive-resolution"></a>Conflitti nella replica di tipo merge avanzata - Risoluzione interattiva
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replica di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre un sistema di risoluzione interattivo che consente di risolvere i conflitti in modo manuale durante la sincronizzazione su richiesta in Gestione sincronizzazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Attivato in fase di esecuzione, il sistema di risoluzione interattivo è un'interfaccia grafica che visualizza i dati relativi a ogni riga in conflitto e offre opzioni per la visualizzazione e la modifica dei dati in conflitto, nonché per la risoluzione distinta dei singoli conflitti.  
  
 Il sistema di risoluzione interattivo presenta alcune analogie con il Visualizzatore conflitti. Nel Visualizzatore conflitti vengono tuttavia visualizzati i risultati dei conflitti già risolti dopo la sincronizzazione di tipo merge, mentre il sistema di risoluzione interattivo visualizza ogni conflitto prima della risoluzione e consente di determinarne l'esito durante la sincronizzazione di tipo merge. È necessario che sia disponibile un utente per il monitoraggio del sistema di risoluzione interattivo in caso di conflitto.  
  
> [!NOTE]  
>  La risoluzione interattiva richiede Gestione sincronizzazione Microsoft Windows. Se una sincronizzazione viene eseguita all'esterno di Gestione sincronizzazione Microsoft Windows (come sincronizzazione pianificata o sincronizzazione su richiesta in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o Monitoraggio replica), i conflitti vengono risolti automaticamente senza richiedere l'intervento dell'utente, in base al sistema di risoluzione specificato per l'articolo. I conflitti a livello di record logici non vengono visualizzati nel sistema di risoluzione interattivo. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>Sistemi di risoluzione dei conflitti di articolo e sistema di risoluzione interattivo  
 I sistemi di risoluzione dei conflitti, ovvero il sistema di risoluzione dei conflitti predefinito, un gestore della logica di business o un sistema personalizzato, vengono assegnati ad articoli specifici durante la creazione di una pubblicazione. Tali sistemi utilizzano un set di regole predefinite per determinare il set di dati che è necessario utilizzare quando si immettono dati di riga in conflitto. Il sistema di risoluzione interattivo non è un sistema di risoluzione dei conflitti distinto con regole per stabilire la modifica che prevale nei conflitti, ma uno strumento da utilizzare in combinazione con i sistemi di risoluzione dei conflitti predefiniti e personalizzati. Il sistema di risoluzione dei conflitti di articolo determina la riga confermata e la riga non confermata e il sistema di risoluzione interattivo consente all'utente di accettare, rifiutare o modificare i risultati.  
  
 Per utilizzare il sistema di risoluzione interattivo, è necessario che la risoluzione interattiva sia attivata per ogni articolo e sottoscrizione che la richiede. Dopo essere stato abilitato per uno o più articoli e sottoscrizioni, il sistema di risoluzione interattivo viene utilizzato quando viene rilevato un conflitto durante la sincronizzazione di tipo merge.  
  
 Per usare il sistema di risoluzione dei conflitti interattivo, vedere [Specify Merge Replication options](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Specificare le opzioni di replica di merge) e [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
