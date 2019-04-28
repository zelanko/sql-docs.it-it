---
title: Terminare l'attività di gestione del dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ab6505ad-3090-453b-bb01-58435e7fa7c0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ec0413f72261bf2890c372773a13a662e9182498
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792758"
---
# <a name="end-the-domain-management-activity"></a>Sospensione dell'attività di gestione del dominio
  In questo argomento viene descritto come completare, chiudere o annullare l'attività di gestione del dominio in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). La gestione del dominio non viene eseguita da una procedura guidata, pertanto i controlli descritti sotto possono essere utilizzati da qualsiasi pagina dell'attività di gestione del dominio.  
  
## <a name="end-domain-management"></a>Annullare la gestione del dominio  
 **Fine**  
 Fare clic per completare l'attività di gestione del dominio. Verrà visualizzata una finestra popup con le opzioni seguenti:  
  
-   **Sì - Pubblica la Knowledge Base e chiudi**: la Knowledge Base verrà pubblicata per consentirne l'uso da parte dell'utente corrente o di altri utenti. La Knowledge Base non verrà bloccata, lo stato della Knowledge Base nella relativa tabella verrà impostato come vuoto e saranno disponibili entrambe le attività, Gestione dominio e Individuazione informazioni. Verrà di nuovo visualizzata la schermata Apri Knowledge Base.  
  
-   **No - Salva il lavoro relativo alla knowledge base e chiudi**: il lavoro verrà salvato, la Knowledge Base rimarrà bloccata e il suo stato verrà impostato come In lavorazione. Entrambe le attività Gestione dominio e Individuazione informazioni saranno disponibili. Verrà di nuovo visualizzata la home page.  
  
-   **Annulla - Rimani nella schermata corrente**: la finestra popup verrà chiusa e verrà di nuovo visualizzata la schermata Gestione dominio.  
  
 **Annulla**  
 Fare clic per terminare l'attività Gestione dominio. Il lavorò verrà perso e sarà visualizzata di nuovo la home page di DQS.  
  
 **Chiudi**  
 Fare clic per salvare il lavoro e tornare alla home page di DQS. La Knowledge Base verrà bloccata e lo stato della Knowledge Base nella relativa tabella nella schermata **Apri Knowledge Base** sarà **Gestione dominio**. Dopo avere fatto clic su **Chiudi**per eseguire l'attività Individuazione informazioni è necessario tornare alla schermata **Gestione dominio** , fare clic su **Fine**e quindi su **Sì** per pubblicare la Knowledge Base o su **No** per salvare il lavoro sulla Knowledge Base e uscire.  Per ulteriori informazioni sull'apertura di una Knowledge Base bloccata, vedere [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
  
