---
title: Eliminare una regola business
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6af3aac4ac8e2a1a4026162eb6ab5f6038b5eed
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729410"
---
# <a name="delete-a-business-rule-master-data-services"></a>Eliminare una regola business (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] eliminare una regola di business quando non è più necessaria.  
  
> [!NOTE]  
>  È possibile impedire la convalida dei dati rispetto a una regola business escludendoli, anziché eliminandoli. Per altre informazioni, vedere [Exclude a Business Rule &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-business-rule"></a>Per eliminare una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Regole business** selezionare un modello nell'elenco a discesa **Modello** .  
  
4.  Nell'elenco a discesa **Entità** selezionare un'entità.  
  
5.  Nell'elenco a discesa **Tipi di membri** selezionare un tipo di membro a cui applicare la regola business.  
  
6.  Nella griglia fare clic sulla riga relativa alla regola business da eliminare.  
  
7.  Fare clic su **Elimina**.  
  
8.  Nella finestra di dialogo di conferma fare clic su **OK**. Il valore nella colonna **Stato della regola di business** è **Eliminazione in sospeso**.  
  
9. Fare clic su **Pubblica tutto**.  
  
10. Nella finestra di dialogo di conferma fare clic su **OK**. La regola business eliminata non viene più visualizzata nella griglia.  
  
## <a name="see-also"></a>Vedere anche  
 [Escludere una regola business &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [Creare e pubblicare una regola business &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regole business &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
