---
title: Finestra di dialogo aggiornamento incrementale (Analysis Services-Dati multidimensionali) | Microsoft Docs
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
ms.openlocfilehash: 6115a5123fd6e72cee0ebccaac5f539be8aebfbe
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544173"
---
# <a name="incremental-update-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Aggiornamento incrementale (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Aggiornamento incrementale** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per definire le impostazioni per l'aggiornamento incrementale di gruppi di misure e partizioni. Per visualizzare la finestra di dialogo **Aggiornamento incrementale** , fare clic su **Configura** nella colonna **Impostazioni** della griglia **Elenco oggetti** nella finestra di dialogo **Elabora** .  
  
## <a name="options"></a>Opzioni  
  
|Termine|Definizione|  
|----------|----------------|  
|**Gruppo di misure**|Selezionare il gruppo di misure da aggiornare in modo incrementale.<br /><br /> Nota: questa opzione è abilitata solo se si sta aggiornando un cubo in modo incrementale. Se si aggiorna in modo incrementale un gruppo di misure o una partizione, questa opzione è disabilitata.|  
|**Partizione**|Selezionare la partizione da aggiornare.<br /><br /> Nota: questa opzione è abilitata solo se si sta aggiornando un cubo in modo incrementale. Se si aggiorna in modo incrementale un gruppo di misure o una partizione, questa opzione è disabilitata.|  
|**Tabella**|Fare clic su questa opzione per aggiornare l'oggetto da una tabella.|  
|**Origine dati o vista origine dati**|Consente di selezionare l'origine dei dati o la vista origine dati contenente la tabella di origine.<br /><br /> Nota: questa opzione è abilitata solo se si seleziona **Tabella** .|  
|**Schema e nome tabella**|Consente di selezionare la tabella di origine utilizzata per recuperare i dati per l'aggiornamento incrementale del cubo, del gruppo di misure o della partizione.<br /><br /> Nota: questa opzione è abilitata solo se si seleziona **Tabella** .|  
|**Query**|Fare clic su questa opzione per aggiornare l'oggetto da una query.|  
|**Origine dati**|Consente di selezionare l'origine dei dati contenente le tabelle in cui eseguire la query.<br /><br /> Nota: questa opzione è abilitata solo se si seleziona **Query** .|  
|**Testo della query**|Consente di digitare il testo della query utilizzata per recuperare i dati per l'aggiornamento incrementale del cubo, del gruppo di misure o della partizione.<br /><br /> Nota: questa opzione è abilitata solo se si seleziona **Query** .|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Finestra di dialogo elabora &#40;Analysis Services-Dati multidimensionali&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
