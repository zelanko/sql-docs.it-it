---
title: Inizializzare le sottoscrizioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d7bf65224506e820ad6c486f3bb0e78d002cc793
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127916"
---
# <a name="initialize-subscriptions"></a>Inizializzazione sottoscrizioni
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È necessario inizializzare i Sottoscrittori prima che possano iniziare a ricevere dati replicati. Non è necessario un set di dati iniziale, ma è necessario che il Sottoscrittore disponga almeno dello schema per ogni oggetto replicato, nonché delle tabelle dei metadati e delle procedure necessarie per la replica.  
  
## <a name="options"></a>Opzioni  
 **Proprietà sottoscrizione**  
 Selezionare la casella di controllo nella colonna **Inizializza** per ogni Sottoscrittore che necessita di un set di dati iniziale. Se la casella di controllo non è selezionata, verranno inizializzati solo i metadati e le procedure della replica. Per altre informazioni sull'inizializzazione di una sottoscrizione senza uno snapshot, vedere [Inizializzare una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Selezionare **Immediatamente** nell'elenco a discesa della colonna **Quando** per fare in modo che l'agente di merge o l'agente di distribuzione trasferisca i file di snapshot al Sottoscrittore al termine della procedura guidata. Selezionare **Alla prima sincronizzazione** per fare in modo che l'agente trasferisca i file alla successiva esecuzione pianificata dell'agente. L'opzione **Immediatamente** non è disponibile per le sottoscrizioni pull di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. L'agente di merge e l'agente di distribuzione non vengono eseguiti nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. È pertanto necessario inizializzare la sottoscrizione utilizzando un altro metodo.  
  
> [!NOTE]  
>  Durante la procedura guidata è possibile che venga richiesto di selezionare la connessione al server di distribuzione per consentire l'avvio del processo appropriato per l'agente di distribuzione o l'agente di merge.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Inizializzare una sottoscrizione](../../relational-databases/replication/initialize-a-subscription.md)   
 [Sottoscrizione delle pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
