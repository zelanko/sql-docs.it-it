---
title: Finestra di dialogo aggiornamento incrementale (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.incrementalupdate.f1
ms.assetid: d5a5ae27-44e7-4179-b9e2-efbf21d6c5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0948fda951bb415d9fe3f457729200752a8afaaf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080491"
---
# <a name="incremental-update-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Aggiornamento incrementale (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Aggiornamento incrementale** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per definire le impostazioni per l'aggiornamento incrementale di gruppi di misure e partizioni. Per visualizzare la finestra di dialogo **Aggiornamento incrementale** , fare clic su **Configura** nella colonna **Impostazioni** della griglia **Elenco oggetti** nella finestra di dialogo **Elabora** .  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Gruppo di misure**|Selezionare il gruppo di misure da aggiornare in modo incrementale.<br /><br /> Nota: Questa opzione è abilitata solo se si sta aggiornando in modo incrementale un cubo. Se si aggiorna in modo incrementale un gruppo di misure o una partizione, questa opzione è disabilitata.|  
|**Partizione**|Selezionare la partizione da aggiornare.<br /><br /> Nota: Questa opzione è abilitata solo se si sta aggiornando in modo incrementale un cubo. Se si aggiorna in modo incrementale un gruppo di misure o una partizione, questa opzione è disabilitata.|  
|**Tabella**|Fare clic su questa opzione per aggiornare l'oggetto da una tabella.|  
|**Origine dati o una vista**|Consente di selezionare l'origine dei dati o la vista origine dati contenente la tabella di origine.<br /><br /> Nota: Questa opzione è abilitata solo se **tabella** sia selezionata.|  
|**Nome e lo schema di tabella**|Consente di selezionare la tabella di origine utilizzata per recuperare i dati per l'aggiornamento incrementale del cubo, del gruppo di misure o della partizione.<br /><br /> Nota: Questa opzione è abilitata solo se **tabella** sia selezionata.|  
|**Query**|Fare clic su questa opzione per aggiornare l'oggetto da una query.|  
|**Data Source**|Consente di selezionare l'origine dei dati contenente le tabelle in cui eseguire la query.<br /><br /> Nota: Questa opzione è abilitata solo se **Query** sia selezionata.|  
|**Testo della query**|Consente di digitare il testo della query utilizzata per recuperare i dati per l'aggiornamento incrementale del cubo, del gruppo di misure o della partizione.<br /><br /> Nota: Questa opzione è abilitata solo se **Query** sia selezionata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Elaborare la finestra di dialogo &#40;Analysis Services - dati multidimensionali&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
