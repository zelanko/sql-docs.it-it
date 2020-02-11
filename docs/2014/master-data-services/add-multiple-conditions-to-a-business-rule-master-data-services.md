---
title: Aggiungere più condizioni a una regola di business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54ab01033fc65f829f2a06bb5cbad8fc9e4d08f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480187"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Aggiungere più condizioni a una regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]aggiungere più condizioni **AND** o **OR** a una regola di business quando si vuole creare una regola più complessa.  
  
> [!NOTE]  
>  Se si crea una regola di business che usa l'operatore **OR** , considerare la possibilità di creare una regola separata per ogni istruzione condizionale che può essere valutata indipendentemente. È quindi possibile escludere regole in base alle esigenze, offrendo maggiore flessibilità e una più facile risoluzione dei problemi.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che sia presente una regola business. Per altre informazioni, vedere [Creare e pubblicare una regola di business &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>Per aggiungere più condizioni a una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Manutenzione regola business** selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Dall'elenco **tipo di membro** selezionare un tipo di membro.  
  
6.  Dall'elenco **Attributo** selezionare un attributo o lasciare inalterata l'impostazione predefinita **Tutti**.  
  
7.  Fare clic sulla riga della regola business che si desidera modificare.  
  
8.  Fare clic su **Modifica regola business selezionata**.  
  
9. Nel riquadro **componenti** espandere il nodo **operatori logici** .  
  
10. Fare clic su **and** o **or** e trascinarlo sull'etichetta **e** del riquadro **if** .  
  
11. Nel riquadro **Componenti** espandere il nodo **Condizioni** .  
  
12. Fare clic su una condizione e trascinarla nel riquadro **if** , nell'etichetta **and** o **or** del passaggio 10.  
  
13. Nel riquadro **attributi** fare clic su un attributo e trascinarlo sull'etichetta **Seleziona attributo** del riquadro **Modifica condizione** .  
  
14. Nel riquadro **Modifica condizione** completare tutti i campi obbligatori.  
  
15. Nel riquadro **Modifica condizione** fare clic su **Salva elemento**.  
  
16. Facoltativamente, per aggiungere altre condizioni, dal riquadro **componenti** trascinare **and** o **or su any** **and** o or nel **riquadro** **if** . Seguire quindi i passaggi da 13 a 15.  
  
    > [!TIP]  
    >  Per eliminare una condizione, fare clic sul nome della condizione e nel riquadro **Modifica condizione** fare clic su **Elimina elemento**.  
  
## <a name="see-also"></a>Vedere anche  
 [Regole business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Modificare il nome di una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Configurare regole business per l'invio di notifiche &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
