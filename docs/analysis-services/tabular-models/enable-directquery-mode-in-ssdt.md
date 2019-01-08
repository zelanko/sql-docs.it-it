---
title: Abilitare la modalità DirectQuery di Analysis Services in SSDT | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83fa1cf8d99f18cd82e00b4020a2d846b1bdfdc6
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206300"
---
# <a name="enable-directquery-mode-in-ssdt"></a>Abilitare la modalità DirectQuery in SSDT
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
In questo argomento verrà descritto come abilitare la modalità DirectQuery per un progetto di modello tabulare in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
Quando si attiva la modalità DirectQuery per un modello tabulare che si sta realizzando in SSDT:
-   le funzionalità che non sono compatibili con la modalità DirectQuery vengono disabilitate.  
-   il modello esistente viene convalidato. gli avvisi vengono visualizzati se le funzionalità non sono compatibili con la modalità DirectQuery.  
-   Se i dati sono stati importati prima di abilitare la modalità DirectQuery, la cache del modello di lavoro viene svuotata.  
  
### <a name="enable-directquery"></a>Abilitare DirectQuery  
  
In SSDT, nel riquadro **Proprietà** per il file **Model.bim** , impostare la proprietà **Modalità DirectQuery**su **On**.  

![Abilitare la modalità DirectQuery in SSDT](../../analysis-services/tabular-models/media/enable-directquery-mode-in-ssdt.png)
  
Se il modello presenta già una connessione a un'origine dati e a dati esistenti, verrà richiesto di immettere le credenziali di database usate per connettersi al database relazionale. I dati già esistenti all'interno del modello verranno rimossi dalla cache in memoria.  
  
Se il modello è parzialmente o completamente completo prima dell'attivazione della modalità DirectQuery, è possibile ottenere errori relativi a funzionalità non compatibili. In Visual Studio aprire l' **Elenco errori** e risolvere eventuali problemi che impedirebbero di impostare la modalità DirectQuery per il modello.  


### <a name="whats-next"></a>Quali sono le operazioni successive? 
È ora possibile importare dati usando l'Importazione guidata tabella per ottenere i metadati per il modello. Non si otterranno righe di dati, ma tabelle, colonne e relazioni da usare come base per il modello. 

È possibile creare una partizione di esempio per ogni tabella e aggiungere dati di esempio in modo da poter verificare il comportamento del modello mentre viene creato. Eventuali dati di esempio aggiunti verranno usati **Analizza in Excel** o in altri strumenti client che possono connettersi al database dell'area di lavoro. Per informazioni più dettagliate, vedere [Aggiungere dati di esempio a un modello DirectQuery in modalità progettazione](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) .  
  
> [!TIP]
>  Anche in modalità DirectQuery in un modello vuoto è sempre possibile visualizzare un piccolo set di righe predefinito per ogni tabella. In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic su **Tabella** > **Proprietà tabella** per visualizzare il set di dati di 50 righe.  
  
  
## <a name="see-also"></a>Vedere anche  
[Abilitare la modalità DirectQuery in SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Aggiungere dati di esempio a un modello DirectQuery in modalità progettazione](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  
