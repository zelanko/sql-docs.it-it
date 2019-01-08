---
title: Eliminare le autorizzazioni per oggetti modello (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting model object permissions [Master Data Services]
- permissions [Master Data Services], deleting model object permissions
- models [Master Data Services], deleting object permissions
ms.assetid: 859c5952-f600-4940-8064-1afd13f7f6dc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e9dfc21fe4f408362c4e8d32f39533c9d271136
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52755274"
---
# <a name="delete-model-object-permissions-master-data-services"></a>Eliminare le autorizzazioni per oggetti modello (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eliminare le autorizzazioni dell'oggetto modello per rimuovere qualsiasi assegnazione attribuita.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Autorizzazioni utenti e gruppi** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-model-object-permissions"></a>Per eliminare le autorizzazioni dell'oggetto modello  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Autorizzazioni utenti e gruppi**.  
  
2.  Nella pagina **Utenti** o **Gruppi** selezionare la riga relativa all'utente o al gruppo che si desidera modificare.  
  
3.  Fare clic su **Modifica utente selezionato**.  
  
4.  Fare clic sulla scheda **Modelli** .  
  
5.  Facoltativamente selezionare un modello nell'elenco **Modello** .  
  
6.  Nel **riepilogo autorizzazioni modello** riquadro, selezionare la riga relativa all'autorizzazione che si desidera eliminare.  
  
7.  Fare clic su **Elimina autorizzazione selezionata**.  
  
    > [!NOTE]  
    >  Se l'autorizzazione viene ereditata da un gruppo, non sarà possibile rimuoverla da un utente. È necessario invece rimuovere l'autorizzazione dal gruppo.  
  
## <a name="see-also"></a>Vedere anche  
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
  
