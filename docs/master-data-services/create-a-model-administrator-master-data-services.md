---
title: Creare un amministratore di modelli (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 44bede292cb49ddcfd791b3e7d65605e1aa2399c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65487497"
---
# <a name="create-a-model-administrator-master-data-services"></a>Creare un amministratore di modelli (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare un amministratore di modelli quando si vuole che un gruppo o un utente abbia tutte le autorizzazioni per tutti gli oggetti in uno o più modelli.  
  
> [!TIP]  
>  Per semplificare l'amministrazione, creare un gruppo locale o di Windows e configurarlo come amministratore di modelli. È quindi possibile aggiungere e rimuovere utenti nel gruppo senza accedere a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso all'area funzionale **Autorizzazioni utenti e gruppi** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model-administrator"></a>Per creare un amministratore del modello  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Autorizzazioni utenti e gruppi**.  
  
2.  Nella pagina **Utenti** o **Gruppi** selezionare la riga relativa all'utente o al gruppo che si desidera modificare.  
  
3.  Fare clic su **Modifica utente selezionato**.  
  
4.  Fare clic sulla scheda **Modelli** .  
  
5.  Facoltativamente selezionare un modello nell'elenco **Modello** .  
  
6.  Fare clic su **Modifica**.  
  
7.  Fare clic sul modello al quale si desidera concedere l'autorizzazione.  
  
8.  Scegliere **Amministratore**dal menu.  
  
9. Completare i passaggi 7 e 8 per ogni modello per cui si desidera che il gruppo o l'utente sia configurato come amministratore.  
  
10. Fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Assegnare autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Assegnare autorizzazioni membri gerarchia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Autorizzazioni per oggetti modello &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Autorizzazioni membri gerarchie &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
