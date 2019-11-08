---
title: Creare un flag di versione
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 25c52ac4dc179940f1a3c45fd5200cf3525c56f9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729560"
---
# <a name="create-a-version-flag-master-data-services"></a>Creare un flag di versione (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un flag di versione da assegnare a una versione. Il flag può indicare la versione che utenti o sistemi di sottoscrizione devono usare.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale Gestione versioni. Per altre informazioni, vedere [Autorizzazioni per aree funzionali &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-create-a-version-flag"></a>Per creare un flag di versione  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Gestione versioni**.  
  
2.  Nella pagina **Gestisci versioni** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Flag**.  
  
3.  Nella pagina **Gestisci flag di versione** nel campo **Modello** selezionare il modello per il quale si vuole creare un flag.  
  
4.  Scegliere **Aggiungi**.  
  
5.  Nella casella **Nome** digitare un nome.  
  
6.  Nella casella **Descrizione** digitare una descrizione.  
  
7.  Nel campo **Solo versioni con commit** selezionare **True** per indicare che il flag può essere assegnato solo alle versioni con stato **Commit completato** . Selezionare **False** per indicare che il flag può essere assegnato alle versioni con qualsiasi stato.  
  
8.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Assegnare un flag a una versione &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Versioni &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Modificare il nome di un flag di versione &#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
