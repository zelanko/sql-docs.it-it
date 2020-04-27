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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479942"
---
# <a name="create-a-subscription-view-master-data-services"></a>Creare una vista sottoscrizioni (Master Data Services)
  Creare una vista sottoscrizioni quando si desidera creare una vista dei dati nel database per [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] l'utilizzo da parte dei sistemi di sottoscrizione.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Gestione integrazione** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-subscription-view"></a>Per creare una vista sottoscrizioni  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]fare clic su **Gestione integrazione**.  
  
2.  Dalla barra dei menu scegliere **Crea viste**.  
  
3.  Nella pagina **viste sottoscrizioni** fare clic su **Aggiungi vista sottoscrizioni**.  
  
4.  Nella casella **nome vista** sottoscrizioni del riquadro **Crea vista sottoscrizioni** Digitare un nome per la visualizzazione.  
  
5.  Selezionare un modello dall'elenco **Modello** .  
  
6.  Selezionare l'opzione **versione** o **flag versione** , quindi selezionare una voce dall'elenco corrispondente.  
  
    > [!TIP]  
    >  Creare una vista sottoscrizioni basata su un flag di versione. Quando si blocca una versione, è possibile riassegnare il flag a una versione aperta senza aggiornare la vista sottoscrizioni.  
  
7.  Selezionare l'opzione **entità** o **gerarchia derivata** , quindi selezionare una voce dall'elenco corrispondente.  
  
8.  Selezionare un formato di vista sottoscrizioni dall'elenco **Formato** .  
  
9. Se si sceglie **Livelli espliciti** o **Livelli derivati** dall'elenco **Formato** , digitare il numero di livelli della gerarchia da includere nella vista.  
  
10. Fare clic su **Save**.  
  
## <a name="see-also"></a>Vedi anche  
 [Esportazione dei dati &#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [Eliminare una vista sottoscrizioni &#40;Master Data Services&#41;](delete-a-subscription-view-master-data-services.md)   
 [Creare un flag di versione &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
