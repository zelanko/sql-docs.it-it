---
title: Proprietà sottoscrizione - Server di pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords:
- Subscription Properties dialog box
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5213c07fcdf84db3297ae5737d1d8726f4355257
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794443"
---
# <a name="subscription-properties---publisher"></a>Proprietà sottoscrizione - Server di pubblicazione
  La finestra di dialogo **Proprietà sottoscrizione** nel server di pubblicazione consente di visualizzare e impostare proprietà per le sottoscrizioni push. Sebbene sia possibile visualizzare alcune proprietà per le sottoscrizioni pull, nella finestra di dialogo **Proprietà sottoscrizione** nel Sottoscrizione sono incluse proprietà aggiuntive ed è possibile modificarle.  
  
 Ogni proprietà nella finestra di dialogo **Proprietà sottoscrizione** include una descrizione. Fare clic su una proprietà per visualizzarne la descrizione nella parte inferiore della finestra di dialogo. In questo argomento vengono fornite informazioni aggiuntive su alcune proprietà che, nella maggior parte dei casi, sono visualizzate nel server di pubblicazione solo per le sottoscrizioni push. Le proprietà sono raggruppate nelle categorie seguenti:  
  
-   Proprietà che si applicano a tutte le sottoscrizioni.  
  
-   Proprietà che si applicano alle sottoscrizioni transazionali.  
  
-   Proprietà che si applicano alle sottoscrizioni di tipo merge.  
  
 Se un'opzione è visualizzata in modalità di sola lettura, può essere impostata solo al momento della creazione della sottoscrizione. Se si desidera impostare opzioni non disponibili nella Creazione guidata nuova sottoscrizione, creare la sottoscrizione tramite stored procedure. Per ulteriori informazioni, vedere [Create a Pull Subscription](create-a-pull-subscription.md) e [Create a Push Subscription](create-a-push-subscription.md).  
  
## <a name="options-for-all-subscriptions"></a>Opzioni per tutte le sottoscrizioni  
 **Sicurezza**  
 Fare clic sulla riga **Account processo agente** e quindi sul pulsante delle proprietà (**...**) per modificare l'account utilizzato per l'esecuzione dell'agente di distribuzione o dell'agente di merge nel server di distribuzione. Per modificare l'account utilizzato dall'agente di distribuzione o dall'agente di merge per creare connessioni al Sottoscrittore, fare clic su **Connessione al Sottoscrittore**e quindi sul pulsante delle proprietà (**...**).  
  
 Per ulteriori informazioni sulle autorizzazioni necessarie per ogni agente, vedere [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
## <a name="options-for-transactional-subscriptions"></a>Opzioni per le sottoscrizioni transazionali  
 **Impedisci il loop delle transazioni**  
 Consente di stabilire se l'agente di distribuzione reinvia le transazioni originate nel Sottoscrittore al Sottoscrittore. Questa opzione viene utilizzata per la replica transazionale bidirezionale. Per altre informazioni, vedere [Bidirectional Transactional Replication](transactional/bidirectional-transactional-replication.md).  
  
 **Sottoscrizione aggiornabile**  
 Consente di stabilire se le modifiche del Sottoscrittore vengono replicate sul server di pubblicazione. È possibile replicare le modifiche utilizzando l'aggiornamento in coda o immediato. L'opzione **Metodo di aggiornamento del Sottoscrittore** determina quale metodo utilizzare. Per altre informazioni, vedere [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="options-for-merge-subscriptions"></a>Opzioni per sottoscrizioni di tipo merge  
 **Definizione partizione (HOST_NAME)**  
 Per una pubblicazione che utilizza filtri con parametri, replica di tipo merge valuta una delle due sistema funzioni (o entrambe se il filtro fa riferimento a entrambe le funzioni) durante la sincronizzazione per determinare i dati che deve ricevere un sottoscrittore: **SUSER_SNAME ()** oppure **HOST_NAME ()**. Per impostazione predefinita, **HOST_NAME()** restituisce il nome del computer in cui è in esecuzione l'agente di merge. È tuttavia possibile sostituire questo valore nella Creazione guidata nuova sottoscrizione. Per ulteriori sui filtri con parametri e la sostituzione di **HOST_NAME()**, vedere [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Tipo di sottoscrizione** e **Priorità**  
 Indica se la sottoscrizione è una sottoscrizione client o server. Questa impostazione non può essere modificata dopo la creazione della sottoscrizione. Le sottoscrizioni server possono ripubblicare i dati in altri Sottoscrittori. A tali sottoscrizioni è inoltre possibile assegnare una priorità per la risoluzione dei conflitti.  
  
 Se si seleziona un tipo di sottoscrizione server nella Creazione guidata nuova sottoscrizione, al Sottoscrittore viene assegnata una priorità che verrà utilizzata nella risoluzione dei conflitti.  
  
 **Risoluzione interattiva**  
 Consente di indicare di utilizzare l'interfaccia utente del sistema di risoluzione dei conflitti interattivo durante la sincronizzazione di tipo merge. A tale scopo, è necessario impostare **Usa Gestione sincronizzazione Microsoft Windows** su **Abilita**. Per altre informazioni, vedere [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà delle sottoscrizioni pull](view-and-modify-pull-subscription-properties.md)   
 [Visualizzare e modificare le proprietà delle sottoscrizioni push](view-and-modify-push-subscription-properties.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
