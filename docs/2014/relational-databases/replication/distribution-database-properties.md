---
title: Proprietà database di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distdbproperties.f1
helpviewer_keywords:
- Distribution Database Properties dialog box
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89b8381de605ab3736afc6ac8e3a7da0d53bf9e6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796883"
---
# <a name="distribution-database-properties"></a>Proprietà database di distribuzione
  La finestra di dialogo **Proprietà database di distribuzione** consente di visualizzare varie proprietà e di impostare il periodo di memorizzazione della transazione e della cronologia per il database.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Il nome del database di distribuzione, il cui valore predefinito è "distribution" (sola lettura).  
  
 **Percorsi dei file**  
 Il percorso del file di database e del file di log (sola lettura).  
  
 **Periodo di memorizzazione della transazione**  
 Questa proprietà è nota anche come periodo di memorizzazione della distribuzione. Si tratta della quantità di tempo di memorizzazione delle transazioni ai fini della replica transazionale. Per altre informazioni, vedere [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
 **Periodo di memorizzazione cronologia**  
 Quantità di tempo di memorizzazione dei metadati della cronologia ai fini di tutti i tipi di replica.  
  
 **Sicurezza agente di lettura coda**  
 L'agente di lettura coda viene utilizzato dalla replica transazionale con sottoscrizioni ad aggiornamento in coda. L'agente di lettura coda viene creato automaticamente se si seleziona **Creazione di una pubblicazione transazionale con aggiornamento delle sottoscrizioni** nella pagina **Tipo di pubblicazione** della Creazione guidata nuova pubblicazione. Fare clic su **Impostazioni di sicurezza...** per modificare l'account nell'ambito del quale l'agente viene eseguito e si connette al server di distribuzione.  
  
 In questa pagina è inoltre possibile creare un agente di lettura coda selezionando **Crea agente di lettura coda** . L'opzione è disabilitata se l'agente è già stato creato.  
  
 Ulteriori informazioni sulla connessione relative all'agente di lettura coda vengono specificate in due posizioni:  
  
-   L'agente si connette al server di pubblicazione mediante le credenziali specificate nella finestra di dialogo **Proprietà server di pubblicazione** che è disponibile nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione** .  
  
-   L'agente si connette al Sottoscrittore mediante le credenziali specificate per l'agente di distribuzione in Creazione guidata nuova sottoscrizione.  
  
 Per altre informazioni, vedere  \\[Replication Agent Security Model](security/replication-agent-security-model.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](configure-distribution.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)  
  
  
