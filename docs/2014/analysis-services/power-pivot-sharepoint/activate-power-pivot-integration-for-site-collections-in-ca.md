---
title: Attivare integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e22c18ef92fbc82401bb9f8294e42971fcdb41c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743276"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>Attivare l'integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale
  L'attivazione dell'integrazione della caratteristica PowerPivot per raccolte siti specifiche è obbligatoria se è stata utilizzata l'opzione di installazione Farm esistente per installare SQL Server PowerPivot per SharePoint. Se PowerPivot per SharePoint è stato installato utilizzando l'opzione Nuovo server, è possibile ignorare questa attività perché il programma di installazione di SQL Server ha già attivato l'integrazione della caratteristica PowerPivot per la raccolta siti radice durante la configurazione della distribuzione.  
  
 L'attivazione della caratteristica a livello di raccolta siti è necessaria per rendere disponibili pagine e modelli ai siti, incluse le pagine di configurazione per l'aggiornamento dei dati pianificato e le pagine dell'applicazione per Raccolta PowerPivot e raccolte Feed di dati.  
  
 È necessario attivare l'integrazione PowerPivot per ogni raccolta siti in cui è supportata l'elaborazione di query PowerPivot.  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario essere un amministratore della raccolta siti.  
  
## <a name="activate-powerpivot-features"></a>Attivare le caratteristiche di PowerPivot  
  
1.  Da un sito di SharePoint scegliere **Azioni sito**.  
  
     Per impostazione predefinita, l'accesso alle applicazioni Web SharePoint viene effettuato tramite la porta 80. Ciò significa che è possibile accedere spesso a un sito di SharePoint immettendo http://\<nome computer > per aprire la raccolta siti radice.  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  In Amministrazione raccolta siti selezionare **Caratteristiche raccolta siti**.  
  
4.  Scorrere verso il basso la pagina fino a individuare **caratteristica della raccolta siti PowerPivot integrazione**.  
  
5.  Fare clic su **Attiva**.  
  
6.  Ripetere per le raccolte siti aggiuntive aprendo ogni sito e facendo clic su **Azioni sito**.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione Server PowerPivot e la configurazione in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Configurazione iniziale &#40;PowerPivot per SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [Installazione di PowerPivot per SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
