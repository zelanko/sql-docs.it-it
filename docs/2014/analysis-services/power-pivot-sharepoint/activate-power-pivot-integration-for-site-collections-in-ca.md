---
title: Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5a8e3f2930d7975f8c75c8f89ab90b78461a650
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072013"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale
  L'attivazione dell'integrazione della caratteristica PowerPivot per raccolte siti specifiche è obbligatoria se è stata utilizzata l'opzione di installazione Farm esistente per installare SQL Server PowerPivot per SharePoint. Se PowerPivot per SharePoint è stato installato utilizzando l'opzione Nuovo server, è possibile ignorare questa attività perché il programma di installazione di SQL Server ha già attivato l'integrazione della caratteristica PowerPivot per la raccolta siti radice durante la configurazione della distribuzione.  
  
 L'attivazione della caratteristica a livello di raccolta siti è necessaria per rendere disponibili pagine e modelli ai siti, incluse le pagine di configurazione per l'aggiornamento dei dati pianificato e le pagine dell'applicazione per Raccolta PowerPivot e raccolte Feed di dati.  
  
 È necessario attivare l'integrazione PowerPivot per ogni raccolta siti in cui è supportata l'elaborazione di query PowerPivot.  
  
## <a name="prerequisites"></a>Prerequisites  
 È necessario essere un amministratore della raccolta siti.  
  
## <a name="activate-powerpivot-features"></a>Attivare le caratteristiche di PowerPivot  
  
1.  Da un sito di SharePoint scegliere **Azioni sito**.  
  
     Per impostazione predefinita, l'accesso alle applicazioni Web SharePoint viene effettuato tramite la porta 80. Ciò significa che spesso è possibile accedere a un sito di SharePoint immettendo il nome del computer http://\<> per aprire la raccolta siti radice.  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  In Amministrazione raccolta siti selezionare **Caratteristiche raccolta siti**.  
  
4.  Scorrere la pagina verso il basso fino a individuare la **funzionalità di raccolta siti di integrazione PowerPivot**.  
  
5.  Fare clic su **Attiva**.  
  
6.  Ripetere l'operazione per raccolte siti aggiuntive aprendo ogni sito e facendo clic su **Azioni sito**.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configurazione iniziale &#40;PowerPivot per SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
