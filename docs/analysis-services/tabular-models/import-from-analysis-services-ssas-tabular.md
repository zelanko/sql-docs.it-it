---
title: Importare da Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 625ac4fb1bf7c09aa0cfa651e105b6621e5be4b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162817"
---
# <a name="import-from-analysis-services"></a>Importare da Analysis Services 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive come creare un nuovo progetto di modello tabulare importando i metadati da un modello tabulare esistente tramite l'importazione da modello di progetto Server in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>Creare un nuovo modello importando i metadati da un modello esistente in Analysis Services  
 È possibile utilizzare il modello di progetto Importa da server per creare un nuovo progetto di modello tabulare copiando i metadati da un modello tabulare esistente in un server Analysis Services. Il nuovo progetto sarà creato con le stesse connessioni all'origine dati, tabelle, relazioni, misure, indicatori KPI, ruoli, gerarchie, prospettive e partizioni del modello da cui è stato importato. Tuttavia, i dati non vengono copiati dal modello esistente nella nuova area di lavoro modello. Una volta completato il processo di importazione e creato il nuovo progetto di modello, è necessario fare clic su Elabora tutto per caricare i dati dalle origini dati nel nuovo database dell'area di lavoro del progetto modello.  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>Per creare un nuovo modello importando metadati da un modello esistente  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
2.  In **Modelli installati** della finestra di dialogo **Nuovo progetto**fare clic su **Business Intelligence**, quindi selezionare **Importa da server**.  
  
3.  In **Nome**digitare un nome per il progetto, quindi specificare un percorso e un nome per la soluzione e scegliere **OK**.  
  
4.  In **Nome server** nella finestra di dialogo **Importa da Analysis Services**specificare il nome del server Analysis Services contenente i metadati del modello che si desidera importare.  
  
5.  In **Nome database**selezionare il database modello tabulare in cui sono contenuti i metadati del modello che si desidera importare e scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà progetto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
