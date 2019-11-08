---
title: Convalidare membri specifici rispetto a regole business
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 885d0c1018c1d30fd4ea5d10276c971dbbf0a114
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728855"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Convalidare membri specifici rispetto a regole business (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è opportuno applicare selettivamente regole business quando si desidera aggiornare o convalidare subset di membri rispetto a regole business.  
  
> [!NOTE]  
>  Per applicare le regole di business a tutti i membri in una versione di un modello, vedere [Validate a Version against Business Rules &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
-   È necessario disporre almeno dell'autorizzazione **Update** per l'oggetto modello al quale vengono applicate le regole di business.  
  
### <a name="to-apply-business-rules-selectively"></a>Per applicare regole business selettivamente  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello nell'elenco **Modello** .  
  
2.  Nell'elenco a discesa **Versione** selezionare una versione.  
  
3.  Fare clic sulla scheda **Esplora** .  
  
4.  Scegliere **Entità** dalla barra dei menu, quindi fare clic sul nome dell'entità contenente i membri a cui applicare le regole.  
  
5.  Fare clic su **Applica regole**. Le regole business sono applicate solo ai membri visualizzati nella griglia.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Regole di business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
