---
title: Nascondere o bloccare colonne nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 624216b190b0a408305c90224087b1f65a4a8286
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207644"
---
# <a name="hide-or-freeze-columns"></a>Nascondere o bloccare colonne 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  In Progettazione modelli, se in una tabella sono presenti colonne che non si desidera visualizzare, è possibile nasconderle temporaneamente. Nascondendo una colonna si ottiene maggiore spazio sullo schermo per aggiungerne di nuove o per utilizzare solo le colonne di dati rilevanti. È possibile nascondere e scoprire colonne dal menu **Colonna** in Progettazione modelli e dal menu di scelta rapida disponibile in ogni intestazione di colonna. Per mantenere visibile un'area di un modello durante lo scorrimento a un'altra area del modello, è possibile bloccare colonne specifiche in un'area.  
  
> [!IMPORTANT]  
>  La possibilità di nascondere colonne non dovrebbe essere utilizzata per la sicurezza dei dati, ma solo per semplificare e abbreviare l'elenco di colonne visibili in Progettazione modelli o nei report. Per proteggere i dati, è possibile definire ruoli di sicurezza. I ruoli possono limitare la visualizzazione di metadati e dati in base agli oggetti definiti nel ruolo. Per altre informazioni, vedere [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 Quando si nasconde una colonna, è possibile scegliere se nasconderla mentre si lavora in Progettazione modelli o nei report. Se si nascondono tutte le colonne, l'intera tabella appare vuota in Progettazione modelli.  
  
> [!NOTE]  
>  Se sono molte le colonne da nascondere, è possibile creare una prospettiva anziché nascondere e scoprire colonne. Una prospettiva è una vista personalizzata dei dati tramite cui si semplifica l'utilizzo di un subset di dati correlati. Per altre informazioni, vedere [crea e Gestisci prospettive](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)  
  
### <a name="to-hide-an-individual-column"></a>Per nascondere una singola colonna  
  
1.  In Progettazione modelli selezionare la tabella contenente la colonna che si desidera nascondere.  
  
2.  Fare clic con il pulsante destro del mouse sulla colonna, selezionare **Nascondi colonne**, quindi fare clic su **Da finestra progettazione e report**, **Da report**oppure su **Da finestra di progettazione**.  
  
### <a name="to-hide-multiple-columns"></a>Per nascondere più colonne  
  
1.  In Progettazione modelli selezionare la tabella contenente le colonne che si desidera nascondere.  
  
2.  Fare clic sul menu **Colonne** , quindi scegliere **Nascondi e scopri**.  
  
3.  Nella finestra di dialogo **Nascondi e scopri colonne** individuare ogni colonna che si desidera nascondere, quindi deselezionare una o entrambe le opzioni **In Designer** (Nella finestra di progettazione) e **In Reports**(Nei report).  
  
4.  Fare clic su **OK**.  
  
### <a name="to-freeze-columns"></a>Per bloccare le colonne  
  
1.  In Progettazione modelli selezionare la tabella contenente le colonne che si desidera bloccare.  
  
2.  Selezionare una o più colonne da bloccare.  
  
3.  Fare clic sul menu **Colonne** , quindi scegliere **Blocca**.  
  
    > [!NOTE]  
    >  Quando una colonna viene bloccata, viene spostata a sinistra della tabella (o davanti) nella finestra di progettazione. Se sbloccata, la colonna non torna nella relativa posizione originale.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
