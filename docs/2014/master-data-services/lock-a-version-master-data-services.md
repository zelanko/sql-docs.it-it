---
title: Bloccare una versione (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b3048a3845e3e65c305abdde3f75a30f777ed1ed
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971281"
---
# <a name="lock-a-version-master-data-services"></a>Bloccare una versione (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]bloccare una versione di un modello per evitare modifiche ai membri del modello e ai relativi attributi.  
  
> [!NOTE]  
>  Quando viene bloccata una versione, gli amministratori del modello possono continuare a aggiungere, modificare e rimuovere membri. Gli altri utenti con autorizzazione per il modello possono solo visualizzare membri.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Lo stato della versione deve essere **Aperto**.  
  
### <a name="to-lock-a-version"></a>Per bloccare una versione  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Gestione versioni**.  
  
2.  Nella pagina **Gestisci versioni** selezionare la riga relativa alla versione che si vuole bloccare.  
  
3.  Fare clic su **Blocca**.  
  
4.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [Eseguire il commit di una versione &#40;Master Data Services&#41;](../../2014/master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Versioni &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)   
 [Sbloccare una versione &#40;Master Data Services&#41;](../../2014/master-data-services/unlock-a-version-master-data-services.md)  
  
  
