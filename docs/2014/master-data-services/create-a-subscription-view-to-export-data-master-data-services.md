---
title: Creare una vista sottoscrizioni (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf14f942857361256febd4329a116c2d349659a0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747933"
---
# <a name="create-a-subscription-view-master-data-services"></a>Creare una vista sottoscrizioni (Master Data Services)
  Creare una vista sottoscrizioni quando si desidera creare una visualizzazione dei dati all'interno di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database per l'uso da sistemi di sottoscrizione.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Gestione integrazione** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-subscription-view"></a>Per creare una vista sottoscrizioni  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]fare clic su **Gestione integrazione**.  
  
2.  Dalla barra dei menu scegliere **Crea viste**.  
  
3.  Nel **viste sottoscrizioni** pagina, fare clic su **Aggiungi vista sottoscrizioni**.  
  
4.  Nel **Crea vista sottoscrizioni** riquadro, nella **nome vista sottoscrizioni** , digitare un nome per la visualizzazione.  
  
5.  Selezionare un modello dall'elenco **Modello** .  
  
6.  Selezionare il **versione** oppure **Flag di versione** opzione e quindi selezionare dall'elenco corrispondente.  
  
    > [!TIP]  
    >  Creare una vista sottoscrizioni basata su un flag di versione. Quando si blocca una versione, è possibile riassegnare il flag a una versione aperta senza aggiornare la vista sottoscrizioni.  
  
7.  Selezionare il **Entity** oppure **gerarchia derivata** opzione e quindi selezionare dall'elenco corrispondente.  
  
8.  Selezionare un formato di vista sottoscrizioni dall'elenco **Formato** .  
  
9. Se si sceglie **Livelli espliciti** o **Livelli derivati** dall'elenco **Formato** , digitare il numero di livelli della gerarchia da includere nella vista.  
  
10. Fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Esportazione di dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [Eliminare una vista sottoscrizioni &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [Creare un flag di versione &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
