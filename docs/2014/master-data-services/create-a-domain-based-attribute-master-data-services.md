---
title: Creare un attributo basato su dominio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f0760ef2d2a29540b126235d6328af1fbfad39ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483423"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>Creare un attributo basato su dominio (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un attributo basato su dominio per popolare i valori di un attributo con i membri di un'entità.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che un'entità esista perché venga utilizzata come origine dei valori di attributo. Ad esempio per creare un attributo basato su dominio che si basa sull'entità Color, è necessario prima creare l'entità Color. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
-   È necessario che sia presente un'entità perché ne venga creato l'attributo. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-domain-based-attribute"></a>Per creare un attributo basato su dominio  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga relativa all'entità per la quale si desidera creare un attributo.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Nella pagina **Modifica entità** :  
  
    -   Se l'attributo è per membri foglia, nel riquadro **Attributi membro foglia** fare clic su **Aggiungi attributo foglia**.  
  
    -   Se l'attributo è per membri consolidati, nel riquadro **Attributi membro consolidati** fare clic su **Aggiungi attributo consolidato**.  
  
    -   Se l'attributo è per raccolte, nel riquadro **Attributi raccolta** fare clic su **Aggiungi attributo raccolta**.  
  
7.  Nella pagina **Aggiungi attributo** selezionare l'opzione **basata su dominio** .  
  
8.  Nella casella **Nome** digitare un nome per l'attributo. Non deve essere lo stesso nome dell'entità che si utilizza per l'origine dei valori di attributo.  
  
9. Nella casella **Larghezza in pixel visualizzazione** digitare la larghezza della colonna attributo da visualizzare nella griglia **Esplora** .  
  
10. Dall'elenco **entità** scegliere l'entità da usare per popolare i valori dell'attributo.  
  
11. Facoltativo. Selezionare **Enable change tracking** per tenere traccia delle modifiche a gruppi di attributi. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Fare clic su **Salva attributo**.  
  
13. Nella pagina **Gestione entità** , fare clic su **Salva entità**.  
  
## <a name="see-also"></a>Vedi anche  
 [Attributi basati su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [Creare una gerarchia derivata &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [Modificare il nome di un attributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Eliminare un attributo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
