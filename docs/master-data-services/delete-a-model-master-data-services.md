---
title: Eliminare un modello
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting models [Master Data Services]
- models [Master Data Services], deleting models
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 65164c1732aefe6555aa19325a158793d07631a6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728353"
---
# <a name="delete-a-model-master-data-services"></a>Eliminare un modello (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Eliminare un modello per rimuoverlo, inclusi tutti i relativi dati, da [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
> [!NOTE]  
>  Quando si completa questa procedura, tutti gli oggetti e tutti i dati di tutte le versioni del modello verranno eliminati in modo permanente.  
  
## <a name="prerequisites"></a>Prerequisites  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per altre informazioni, vedere [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-model"></a>Per eliminare un modello  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **Vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **Modelli**.  
  
3.  Dalla griglia della pagina **Gestione modelli** selezionare la riga per il modello che si vuole eliminare.  
  
4.  Fare clic su **Elimina**.  
  
5.  Nella finestra di dialogo di conferma fare clic su **OK**.  
  
6.  Nell'ulteriore finestra di dialogo di conferma fare clic su **OK**.  
  
 La colonna **Stato** nella griglia mostra lo stato dell'operazione sul modello. Quando si fa clic sul pulsante **Salva modello** , viene visualizzata l'immagine di ![aggiornamento](../master-data-services/media/mds-model-status-updating.png "Aggiornamento") , che indica che il modello è in fase di aggiornamento. Se si verificano errori durante la creazione o la modifica di un modello, viene visualizzata l'immagine dell' ![errore](../master-data-services/media/mds-model-status-error.png "Errore") . In caso contrario, lo stato è OK e viene visualizzata l'immagine ![OK](../master-data-services/media/mds-model-status-ok.png "OK") .  
  
## <a name="see-also"></a>Vedere anche  
 [Modelli &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)   
 [Creare un modello &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)  
  
  
