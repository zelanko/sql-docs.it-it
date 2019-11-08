---
title: Nascondere o eliminare i livelli di una gerarchia derivata
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b364213586b8f796101e099c1384cba9569f8ad9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728129"
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Nascondere o eliminare livelli di una gerarchia derivata (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]è possibile nascondere un livello di una gerarchia derivata quando è necessario per il raggruppamento ma non si vuole visualizzarlo. Eliminare un livello quando non si desidera utilizzarlo per il raggruppamento.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>Per nascondere o eliminare i livelli di una gerarchia derivata  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Scegliere **Gestisci** dalla barra dei menu e fare clic su **Gerarchie derivate**.  
  
3.  Nella pagina **Gestione gerarchia derivata** dall'elenco **Modello** selezionare un modello.  
  
4.  Selezionare la riga relativa alla gerarchia derivata da modificare.  
  
5.  Fare clic su **Modifica**.  
  
6.  Nel riquadro **Livelli correnti** :  
  
    -   Per nascondere un livello, fare clic su un livello diverso quello superiore o inferiore. Nell'elenco **Visibile** selezionare **No**. Quindi fare clic su **Salva elemento gerarchia selezionato**.  
  
    -   Per eliminare il livello superiore, fare clic su **Elimina elemento gerarchia selezionato**. Nella finestra di dialogo di conferma fare clic su **OK**. È possibile eliminare solo il livello superiore.  
  
## <a name="see-also"></a>Vedere anche  
    
 [Gerarchie derivate &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
