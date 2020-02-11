---
title: Convalidare membri specifici rispetto a regole business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: edf6d73edb8c4409f82302c2cdf013f18037e4bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478537"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Convalidare membri specifici rispetto a regole business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]è opportuno applicare selettivamente regole business quando si desidera aggiornare o convalidare subset di membri rispetto a regole business.  
  
> [!NOTE]  
>  Per applicare le regole di business a tutti i membri in una versione di un modello, vedere [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
-   È necessario disporre almeno dell'autorizzazione **Update** per l'oggetto modello al quale vengono applicate le regole di business.  
  
### <a name="to-apply-business-rules-selectively"></a>Per applicare regole business selettivamente  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello nell'elenco **Modello** .  
  
2.  Selezionare una versione dall'elenco **Versione** .  
  
3.  Fare clic su **Esplora**.  
  
4.  Scegliere **Entità** dalla barra dei menu, quindi fare clic sul nome dell'entità contenente i membri a cui applicare le regole.  
  
5.  Fare clic su **Applica regole business**. Le regole business sono applicate solo ai membri visualizzati nella griglia.  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare una versione rispetto alle regole business &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)   
 [Regole business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
