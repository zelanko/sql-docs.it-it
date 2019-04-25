---
title: Riattivare un membro o una raccolta (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], reactivating
- consolidated members [Master Data Services], reactivating
- reactivating members [Master Data Services]
- members [Master Data Services], reactivating
- reactivating collections [Master Data Services]
- leaf members [Master Data Services], reactivating
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 208f801522e53eb8d8075cced223d2d0360f257b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765564"
---
# <a name="reactivate-a-member-or-collection-master-data-services"></a>Riattivare un membro o una raccolta (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]è possibile riattivare un membro che è stato:  
  
-   Disattivato dal processo di gestione temporanea.  
  
-   Eliminato in [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]MDS.  
  
-   Eliminato nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Quando si riattiva un membro, i relativi attributi e l'appartenenza a gerarchie e raccolte vengono ripristinati.  
  
 È inoltre possibile riattivare le raccolte. Quando si esegue questa operazione, vengono ripristinati gli attributi della raccolta e i membri che appartengono ad essa.  
  
 Quando si riattiva una raccolta o un membro, vengono ripristinate tutte le transazioni precedenti.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]è necessario disporre dell'autorizzazione per l'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-reactivate-a-member-or-collection"></a>Per riattivare un membro o una raccolta  
  
1.  Scegliere [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Gestione versioni **dalla home page di**.  
  
2.  Sulla barra dei menu fare clic su **Transazioni**.  
  
3.  Nella pagina **Transazioni** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare una versione dall'elenco **Versione** .  
  
5.  Nel riquadro **Transazioni** fare clic sulla riga del membro o della raccolta che si vuole riattivare. Per questa riga deve essere visualizzata l'indicazione **Attivo** nella colonna **Valore precedente** e l'indicazione **Disattivato** nella colonna **Nuovo valore** .  
  
6.  Fare clic su **Inverti transazione selezionata**.  
  
7.  Nella finestra di dialogo di conferma fare clic su **OK**. Viene aggiunta una nuova transazione con l'indicazione **Attivo** nella colonna **Nuovo valore** .  
  
## <a name="see-also"></a>Vedere anche  
 [Disattivare o eliminare membri tramite il processo di gestione temporanea &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Eliminare un membro o una raccolta &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [Membri &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Raccolte &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
