---
title: Creare un attributo di file (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating file attributes [Master Data Services]
- attributes [Master Data Services], creating file attributes
ms.assetid: d224886b-2ef1-4658-8b01-2213cc4b8df6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 435f68e67080bf006b0c0f121f565ced2339a705
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765343"
---
# <a name="create-a-file-attribute-master-data-services"></a>Creare un attributo di file (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un attributo di file per popolare i valori di attributo con i file.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario che sia presente un'entità perché ne venga creato l'attributo. Per altre informazioni, vedere [Creare un'entità &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-file-attribute"></a>Per creare un attributo di file  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Entità**.  
  
3.  Nella pagina **Gestione entità** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare la riga relativa all'entità per la quale si desidera creare un attributo.  
  
5.  Fare clic su **Modifica entità selezionata**.  
  
6.  Nella pagina **Modifica entità** :  
  
    -   Se l'attributo è per membri foglia, nel riquadro **Attributi membro foglia** fare clic su **Aggiungi attributo foglia**.  
  
    -   Se l'attributo è per membri consolidati, nel riquadro **Attributi membro consolidati** fare clic su **Aggiungi attributo consolidato**.  
  
    -   Se l'attributo è per raccolte, nel riquadro **Attributi raccolta** fare clic su **Aggiungi attributo raccolta**.  
  
7.  Nel **Aggiungi attributo** pagina, selezionare la **File** opzione.  
  
8.  Nella casella **Nome** digitare un nome per l'attributo. Per un elenco di parole che non vanno usate come nomi di attributo, vedere [Parole riservate &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. Nella casella **Larghezza in pixel visualizzazione** digitare la larghezza della colonna attributo da visualizzare nella griglia **Esplora** .  
  
10. Dal **estensione di File** elencare, selezionare uno o più tipi di file che un utente può caricare o lasciare il valore predefinito (*.\*) per consentire tutti i tipi di file.  
  
11. Facoltativamente, selezionare **Abilita rilevamento modifiche** per tenere traccia delle modifiche a gruppi di attributi. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
12. Fare clic su **Salva attributo**.  
  
13. Nella pagina **Gestione entità** , fare clic su **Salva entità**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [Modificare un nome di attributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Creare un attributo basato su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Creare un attributo di testo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
  
