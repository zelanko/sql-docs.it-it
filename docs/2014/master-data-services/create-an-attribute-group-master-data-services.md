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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483327"
---
# <a name="create-an-attribute-group-master-data-services"></a>Creare un gruppo di attributi (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare gruppi di attributi quando si desidera che gli attributi vengano visualizzati in schede singole nella griglia **Esplora** .  
  
> [!NOTE]  
>  Quando si crea un gruppo di attributi, questo viene automaticamente nascosto a tutti gli utenti ad eccezione di quello che lo creato. Per altre informazioni su come rendere visibile un gruppo, vedere [Rendere visibile un gruppo di attributi per gli utenti &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
-   È necessario che esista almeno un attributo. Per altre informazioni, vedere [Creare un attributo di testo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-create-an-attribute-group"></a>Per creare un gruppo di attributi  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nel **Vista modelli** pagina, dalla barra dei menu scegliere **Gestisci** e fare clic su **gruppi di attributi**.  
  
3.  Selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Fare clic su **Gruppi di foglie**, **Gruppi consolidati**o **Gruppi di raccolte** per creare rispettivamente un gruppo di attributi per membri foglia, membri consolidati o raccolte.  
  
6.  Fare clic su **Aggiungi gruppo di attributi**.  
  
7.  Nel **nome gruppo di foglie** , digitare un nome per il gruppo. Si tratta del nome visualizzato nella scheda **Explorer**.  
  
    > [!NOTE]  
    >  Se è stato selezionato **gruppi consolidati** oppure **gruppi di raccolte** nel passaggio 5, questa casella è **nome gruppo consolidato** o **nome del gruppo di raccolta**rispettivamente.  
  
8.  Fare clic su **Salva gruppo**.  
  
9. Espandere la cartella relativa al gruppo.  
  
10. Fare clic su **Attributi**.  
  
11. Fare clic su **Modifica elemento selezionato**.  
  
12. Fare clic sugli attributi nel **Available** casella e fare clic sul **Add** freccia. Per aggiungere tutto, fare clic sulla freccia **Aggiungi tutto** .  
  
13. Facoltativamente, fare clic il **iscrizione** e **verso il basso** frecce per modificare l'ordine da sinistra a destra degli attributi.  
  
14. Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Rendere visibile un gruppo di attributi per gli utenti &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Modificare il nome di un gruppo di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [Eliminare un gruppo di attributi &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [Autorizzazioni per elementi foglia &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [Consolidare le autorizzazioni &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
