---
title: Importare da Analysis Services (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0c0a07a1822bc01e4ce5048a48b754ae0ea10d2e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938862"
---
# <a name="import-from-analysis-services-ssas-tabular"></a>Importare da Analysis Services (SSAS tabulare)
  In questo argomento viene descritto come creare un nuovo progetto di modello tabulare importando i metadati da un modello tabulare esistente tramite il modello di progetto Importa da server disponibile in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>Creare un nuovo modello importando i metadati da un modello esistente in Analysis Services  
 È possibile utilizzare il modello di progetto Importa da server per creare un nuovo progetto di modello tabulare copiando i metadati da un modello tabulare esistente in un server Analysis Services. Il nuovo progetto sarà creato con le stesse connessioni all'origine dati, tabelle, relazioni, misure, indicatori KPI, ruoli, gerarchie, prospettive e partizioni del modello da cui è stato importato. Tuttavia, i dati non vengono copiati dal modello esistente nella nuova area di lavoro modello. Una volta completato il processo di importazione e creato il nuovo progetto di modello, è necessario fare clic su Elabora tutto per caricare i dati dalle origini dati nel nuovo database dell'area di lavoro del progetto modello.  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>Per creare un nuovo modello importando metadati da un modello esistente  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  In **Modelli installati** della finestra di dialogo **Nuovo progetto**fare clic su **Business Intelligence**, quindi selezionare **Importa da server**.  
  
3.  In **Nome**digitare un nome per il progetto, quindi specificare un percorso e un nome per la soluzione e scegliere **OK**.  
  
4.  In **Nome server** nella finestra di dialogo **Importa da Analysis Services**specificare il nome del server Analysis Services contenente i metadati del modello che si desidera importare.  
  
5.  In **Nome database**selezionare il database modello tabulare in cui sono contenuti i metadati del modello che si desidera importare e scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del progetto &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)  
  
  
