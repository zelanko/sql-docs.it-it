---
title: Aggiungere attributi a un gruppo di rilevamento modifiche (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6d215fe6a1b0c41868816e09e64927b8f736f8c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877486"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Aggiungere attributi ad un gruppo rilevamento modifiche (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]aggiungere attributi a un gruppo rilevamento modifiche quando si vuole tenere traccia delle modifiche apportate ai valori dell'attributo.  
  
> [!NOTE]  
>  In seguito all'aggiunta di un attributo a un gruppo rilevamento modifiche, quando si modificano i valori relativi a tale attributo, l'attributo viene contrassegnato nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Creare una regola business per eseguire le azioni appropriate in base alla modifica.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che esistano degli attributi da aggiungere al gruppo rilevamento modifiche. Per altre informazioni, vedere [Create a Text Attribute &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>Per aggiungere attributi ad un gruppo rilevamento modifiche  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nel **Esplora modelli** pagina, dalla barra dei menu, scegliere **Gestisci** e fare clic su **entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga relativa all'entità per la quale si desidera tenere traccia dei valori di attributo.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Nella pagina **Modifica entità** :  
  
    -   Se l'attributo è per membri foglia, nel **attributi foglia** riquadro, selezionare l'attributo e fare clic su **attributo foglia modifica**.  
  
    -   Se l'attributo è per membri consolidati, nel **attributi consolidati** riquadro, selezionare l'attributo e fare clic su **Modifica attributo consolidato**.  
  
    -   Se l'attributo è per raccolte, nel **attributi raccolta** riquadro, selezionare l'attributo e fare clic su **attributo raccolta modifica**.  
  
7.  Selezionare la casella di controllo **Abilita rilevamento modifiche** .  
  
8.  Nella casella **Gruppo rilevamento modifiche** digitare un numero per il gruppo.  
  
9. Fare clic su **Salva attributo**.  
  
10. Nella pagina **Gestione entità** , fare clic su **Salva entità**.  
  
11. Ripetere questa procedura per tutti gli attributi che si desidera includere nel gruppo. Utilizzare lo stesso numero del gruppo rilevamento modifiche per ciascun attributo del gruppo.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Inizializzare azioni basate su modifiche dei valori di attributo &#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un attributo di testo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
