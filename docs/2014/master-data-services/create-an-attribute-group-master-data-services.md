---
title: Creare un gruppo di attributi (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c832fe601eb7151e438d7f93c3e39e9b249ea246
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483327"
---
# <a name="create-an-attribute-group-master-data-services"></a>Creare un gruppo di attributi (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare gruppi di attributi quando si desidera che gli attributi vengano visualizzati in schede singole nella griglia **Esplora** .  
  
> [!NOTE]  
>  Quando si crea un gruppo di attributi, questo viene automaticamente nascosto a tutti gli utenti ad eccezione di quello che lo creato. Per altre informazioni su come rendere visibile un gruppo, vedere [Rendere visibile un gruppo di attributi per gli utenti &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
-   È necessario che esista almeno un attributo. Per altre informazioni, vedere [Creare un attributo di testo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-create-an-attribute-group"></a>Per creare un gruppo di attributi  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **gruppi di attributi**.  
  
3.  Dall'elenco **Modello** , selezionare un modello.  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Fare clic su **Gruppi di foglie**, **Gruppi consolidati**o **Gruppi di raccolte** per creare rispettivamente un gruppo di attributi per membri foglia, membri consolidati o raccolte.  
  
6.  Fare clic su **Aggiungi gruppo di attributi**.  
  
7.  Nella casella **nome gruppo foglia** Digitare un nome per il gruppo. Si tratta del nome visualizzato nella scheda in **Esplora**.  
  
    > [!NOTE]  
    >  Se nel passaggio 5 sono stati selezionati **gruppi consolidati** o **gruppi di raccolte** , questa casella corrisponde rispettivamente al nome del **gruppo consolidato** o al **nome del gruppo di raccolte**.  
  
8.  Fare clic su **Salva gruppo**.  
  
9. Espandere la cartella relativa al gruppo.  
  
10. Fare clic su **Attributi**.  
  
11. Fare clic su **modifica elemento selezionato**.  
  
12. Fare clic su attributi nella casella **disponibile** e fare clic sulla freccia **Aggiungi** . Per aggiungere tutto, fare clic sulla freccia **Aggiungi tutto** .  
  
13. Facoltativamente, fare clic sulle frecce **su** e **giù** per modificare l'ordine degli attributi da sinistra a destra.  
  
14. Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Rendere visibile un gruppo di attributi agli utenti &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Modificare il nome di un gruppo di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [Eliminare un gruppo di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [Autorizzazioni foglia &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Autorizzazioni consolidate &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
