---
title: Assegnare un flag a una versione (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 94c387915d4962eba4d97aa758ca5d5a2aa74b13
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972241"
---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>Assegnare un flag a una versione (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]assegnare un flag a una versione per indicare la versione che utenti o sistemi di sottoscrizione devono utilizzare.  
  
> [!NOTE]  
>  I flag di versione possono essere solo assegnati a una versione alla volta. Se si assegna un flag già assegnato a un'altra versione, il flag verrà spostato alla versione che si è selezionata.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   È necessario aver creato un flag di versione da assegnare. Per altre informazioni, vedere [Creare un flag di versione &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md).  
  
### <a name="to-assign-a-flag-to-a-version"></a>Per assegnare un flag a una versione  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Gestione versioni**.  
  
2.  Nella pagina **Gestisci versioni** nella riga per la versione a cui si vuole assegnare un flag, fare doppio clic sulla cella nella colonna **Flag** .  
  
3.  Nell'elenco selezionare il flag che si desidera assegnare.  
  
    > [!NOTE]  
    >  Se il flag desiderato non è disponibile, è possibile che sia disponibile solo per le versioni con **Commit completato** . Per confermare, passare alla pagina **Gestisci flag di versione** e visualizzare il campo **Solo versioni con commit** per il flag.  
  
4.  Premere INVIO per salvare la modifica la formula.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un flag di versione &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)   
 [Versioni &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
