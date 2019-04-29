---
title: Creare una gerarchia esplicita (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b24a03ff71e6ddec125dfa40ae4c01b3062ada8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925027"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>Creare una gerarchia esplicita (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare una gerarchia esplicita quando è necessaria una gerarchia incompleta nella quale possono esistere membri a qualsiasi livello. Nelle gerarchie esplicite sono inclusi membri da una singola entità.  
  
 Dopo aver creato una gerarchia esplicita, è possibile aggiungervi membri nell'area funzionale **Esplora** .  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario abilitare l'entità per le gerarchie esplicite e le raccolte. Per altre informazioni, vedere [abilitare un'entità per gerarchie esplicite e raccolte &#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md).  
  
### <a name="to-create-an-explicit-hierarchy"></a>Per creare una gerarchia esplicita  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga relativa all'entità per la quale si desidera creare una gerarchia esplicita.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Nel **modifica entità** nella pagina il **gerarchie esplicite** riquadro, fare clic su **Aggiungi gerarchia esplicita**.  
  
7.  Nel **Aggiungi gerarchia esplicita** pagina il **nome gerarchia esplicita** casella, digitare un nome per la gerarchia.  
  
8.  Facoltativamente, deselezionare la casella di controllo **Gerarchia obbligatoria** per creare una gerarchia come non obbligatoria. Per altre informazioni sui tipi di gerarchia, vedere [Gerarchie esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md).  
  
9. Fare clic su **Salva gerarchia**.  
  
10. Nel **modifica entità** pagina, fare clic su **Salva entità**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Creare membri consolidati &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-consolidated-member-master-data-services.md)  
  
-   [Spostare membri all'interno di una gerarchia di &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchie esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [Gerarchie derivate con estremità esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Modificare il nome di una gerarchia esplicita &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  
