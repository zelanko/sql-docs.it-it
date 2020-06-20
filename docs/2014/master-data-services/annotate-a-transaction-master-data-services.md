---
title: Annotare una transazione (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad76c2933cf39bf1a036995a09c3713e79f5db09
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972261"
---
# <a name="annotate-a-transaction-master-data-services"></a>Annotare una transazione (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]annotare una transazione quando si desidera fornire dettagli di supporto sulla transazione per scopi cronologici.  
  
> [!NOTE]  
>  Non è possibile eliminare le annotazioni.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   Per annotare le transazioni create, è necessario disporre dell'autorizzazione per accedere all'area funzionale **Visualizzatore** e almeno dell'autorizzazione **Update** per l'oggetto modello che si vuole annotare.  
  
-   Per annotare le transazioni per tutti gli utenti, è necessario disporre dell'autorizzazione per l'accesso all'area funzionale **Gestione versioni** ed essere un amministratore di modelli. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>Per annotare una transazione in Esplora  
  
1.  Nella home page di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionare un modello nell'elenco **Modello** .  
  
2.  Selezionare una versione dall'elenco **Versione** .  
  
3.  Fare clic su **Esplora**.  
  
4.  Scegliere **Entità** dalla barra dei menu e quindi fare clic sull'entità contenente il membro con una transazione che si vuole annotare.  
  
5.  Fare clic sulla riga del membro nella griglia.  
  
6.  Fare clic su **Visualizza transazioni**.  
  
7.  Nella finestra di dialogo **Visualizza transazioni** fare clic sulla transazione che si vuole annotare.  
  
8.  Nella casella in corrispondenza della parte inferiore della finestra di dialogo digitare l'annotazione.  
  
9. Fare clic su **Aggiungi annotazione**. L'annotazione verrà visualizzata nel riquadro **Annotazioni** .  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>Per annotare una transazione in Gestione versioni (solo amministratori)  
  
1.  Scegliere [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Gestione versioni **dalla home page di**.  
  
2.  Sulla barra dei menu fare clic su **Transazioni**.  
  
3.  Nel riquadro **Transazioni** fare clic sulla riga nella griglia per la transazione che si vuole annotare.  
  
4.  Nella casella **Annotazione** del riquadro **Annotazioni transazioni** digitare l'annotazione.  
  
5.  Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Annotazioni &#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)   
 [Transazioni &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
