---
title: Creare e gestire partizioni nel database dell'area di lavoro di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 40e87650a36f717aea1a333c134e7722383f4ec4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207725"
---
# <a name="create-and-manage-partitions-in-the-workspace-database"></a>Creare e gestire partizioni nel database dell'area di lavoro 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente o in parallelo ad altre. Le partizioni possono consentire di migliorare la scalabilità e la facilità di gestione di database grandi. Per impostazione predefinita, ogni tabella dispone di una partizione in cui sono incluse tutte le colonne. Nelle attività di questo argomento viene descritto come creare e gestire partizioni nel database dell'area di lavoro modello tramite la finestra di dialogo **Gestione partizioni** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 Dopo aver distribuito un modello in un'altra istanza di Analysis Services, gli amministratori di database possono creare e gestire partizioni nel modello (distribuito) utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Non è possibile unire partizioni nel database dell'area di lavoro modello tramite la finestra di dialogo Gestione partizioni. Le partizioni possono essere unite in un modello distribuito solo utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="tasks"></a>Attività  
 Per creare e gestire partizioni, usare la finestra di dialogo **Gestione partizioni** . Per visualizzare la finestra di dialogo **Gestione partizioni** , in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic sul menu **Tabella** e quindi scegliere **Partizioni**.  
  
###  <a name="bkmk_create_new"></a> Per creare una nuova partizione  
  
1.  In Progettazione modelli selezionare la tabella per cui si desidera definire una partizione.  
  
2.  Fare clic sul menu **Tabella** , quindi scegliere **Partizioni**.  
  
3.  Nella casella di riepilogo **Tabella**di **Gestione partizioni** verificare o selezionare la tabella che si vuole partizionare e quindi fare clic su **Nuova**.  
  
4.  In **Nome partizione**digitare un nome per la partizione. Per impostazione predefinita, il nome della partizione predefinita sarà numerato in modo incrementale per ogni nuova partizione.  
  
5.  È possibile selezionare le righe e le colonne da includere nella partizione utilizzando la modalità Anteprima tabella o una query SQL creata tramite la modalità Editor query.  
  
     Per usare la modalità Anteprima tabella (impostazione predefinita), fare clic sul pulsante **Anteprima tabella** in prossimità dell'angolo superiore destro della finestra di anteprima. Scegliere le colonne che si desidera includere nella partizione selezionando la casella di controllo accanto al nome della colonna. Per filtrare le righe, fare clic con il pulsante destro del mouse su un valore della cella e scegliere **Filtro in base al valore della cella selezionata**.  
  
     Per usare un'istruzione SQL, fare clic sul pulsante **Editor query** in prossimità dell'angolo superiore destro della finestra di anteprima e quindi digitare o incollare un'istruzione della query SQL nella finestra Query. Per convalidare l'istruzione, fare clic su **Convalida**. Per usare Progettazione query, fare clic su **Progettazione**.  
  
###  <a name="bkmk_copy"></a> Per copiare una partizione  
  
1.  Nella casella di riepilogo **Tabella**di **Gestione partizioni** verificare o selezionare la tabella contenente la partizione che si vuole copiare.  
  
2.  Dall'elenco **Partizioni** selezionare la partizione che si vuole copiare e quindi fare clic su **Copia**.  
  
3.  In **Nome partizione**digitare un nuovo nome per la partizione.  
  
###  <a name="bkmk_delete"></a> Per eliminare una partizione  
  
1.  Nella casella di riepilogo **Tabella**di **Gestione partizioni** verificare o selezionare la tabella contenente la partizione che si vuole eliminare.  
  
2.  Nell'elenco **Partizioni** selezionare la partizione che si vuole eliminare e quindi fare clic su **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Elaborare partizioni nel database dell'area di lavoro](../../analysis-services/tabular-models/process-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
