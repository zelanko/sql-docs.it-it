---
title: Creare membri consolidati (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f96ab2cb9c2076d36ae36d3aa3358ae4886a1b23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483437"
---
# <a name="create-a-consolidated-member-master-data-services"></a>Create a Consolidated Member (Master Data Services)
  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]creare un membro consolidato quando si desidera un nodo padre per una gerarchia esplicita. I membri consolidati possono avere attributi specifici, che vengono usati per il raggruppamento. Come illustrato nell'esempio seguente, i membri consolidati possono essere usati per i gruppi di account che includono account sottostanti.  
  
 ![I membri consolidati MDS](../../2014/master-data-services/media/mds-consolidated-members.png "MDS membri consolidati")  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
-   È necessario disporre almeno dell'autorizzazione **Aggiornamento** per l'oggetto modello consolidato per l'entità a cui si desidera aggiungere un membro.  
  
### <a name="to-create-a-consolidated-member"></a>Per creare un membro consolidato  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello nell'elenco **Modello** .  
  
2.  Selezionare una versione dall'elenco **Versione** .  
  
3.  Fare clic su **Esplora**.  
  
4.  Dalla barra dei menu scegliere **Gerarchie** , quindi fare clic sul nome della gerarchia alla quale si desidera aggiungere un membro consolidato.  
  
5.  Sopra la griglia, selezionare l'opzione **Membri consolidati** o **Tutti i membri consolidati nella gerarchia** .  
  
6.  Scegliere **Aggiungi**.  
  
7.  Nel riquadro sulla destra, completare i campi.  
  
8.  Facoltativo. Nella casella **Annotazioni** , digitare un commento indicando il perché è stato aggiunto il membro. Tutti gli utenti che dispongono di accesso al membro possono visualizzare l'annotazione.  
  
9. Fare clic su **OK**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Spostare membri all'interno di una gerarchia di &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una gerarchia esplicita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Creare un membro foglia &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)   
 [Caricare o aggiornare membri in Master Data Services tramite il processo di gestione temporanea](add-update-and-delete-data-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Gerarchie esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
