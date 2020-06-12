---
title: Finestra di dialogo elabora (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
author: minewiskan
ms.author: owend
ms.openlocfilehash: f6b9ab6db9fc50b09b752b5deaa59d42c4664bd5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539993"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Elabora (Analysis Services - Dati multidimensionali)
  Utilizzare la finestra di dialogo **Elabora** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per elaborare oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per visualizzare la finestra di dialogo **Elabora** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , è possibile:  
  
-   Fare clic con il pulsante destro del mouse su una struttura di data mining, una dimensione, un cubo o un progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora soluzioni** e scegliere **Elabora**.  
  
-   Selezionare **Elabora** dalla barra degli strumenti in qualsiasi pagina di **Progettazione cubi**o di **Progettazione dimensioni**oppure nelle pagine **Struttura di dati mining** e **Modelli di dati mining** di **Progettazione modelli di dati mining**.  
  
-   Fare clic con il pulsante destro del mouse su un modello di data mining nella pagina **Modelli di data mining** di **Progettazione modelli di data mining** e scegliere **Elabora struttura di data mining e tutti i modelli** o **Elabora modello**.  
  
 Per visualizzare la finestra di dialogo **Elabora** in **SQL Server Management Studio** , è possibile:  
  
-   Fare clic con il pulsante destro del mouse su un modello di data mining, una struttura di data mining, una dimensione, una partizione, un gruppo di misure, un cubo o un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora oggetti** e scegliere **Elabora**.  
  
## <a name="options"></a>Opzioni  
 **Elenco oggetti**  
 Consente di selezionare gli oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] da elaborare, nonché le opzioni di elaborazione e le impostazioni da applicare. La griglia include le colonne seguenti:  
  
 **nome oggetto**  
 Consente di visualizzare il nome dell'oggetto da elaborare. L'icona a sinistra del nome indica il tipo di oggetto.  
  
 **Tipo**  
 Consente di visualizzare il tipo dell'oggetto da elaborare.  
  
 **Opzioni elaborazione**  
 Consente di selezionare il tipo di elaborazione da eseguire sull'oggetto selezionato. Per ulteriori informazioni sulle opzioni di elaborazione disponibili, vedere [elaborazione di oggetti del modello multidimensionale](multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 **Impostazioni**  
 Consente di visualizzare il collegamento ipertestuale **Configura** al momento della selezione di **Elaborazione incrementale** in **Opzioni elaborazione** per cubi, gruppi di misure o partizioni. Per aprire la finestra di dialogo **Aggiornamento incrementale** , fare clic su **Configura** . Per altre informazioni sulla finestra di dialogo **Aggiornamento incrementale**, vedere [Finestra di dialogo Aggiornamento incrementale &#40;Analysis Services - Dati multidimensionali&#41;](incremental-update-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Rimuovi**  
 Fare clic su questo pulsante per rimuovere gli elementi selezionati da **Elenco oggetti**.  
  
 **Analisi di impatto**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Analisi di impatto** e visualizzare gli oggetti interessati dall'attività di elaborazione. Per altre informazioni sulla finestra di dialogo **Analisi di impatto**, vedere [Finestra di dialogo Analisi di impatto &#40;Analysis Services - Dati multidimensionali&#41;](impact-analysis-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Questa opzione è disabilitata quando si seleziona l'opzione **Elabora oggetti interessati** nella finestra di dialogo **Cambia impostazioni** .  
  
 **Modifica impostazioni**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Cambia impostazioni** e modificare le impostazioni che controllano l'elaborazione degli oggetti selezionati, incluse quelle relative a writeback, elaborazione batch ed errori di chiave della dimensione. Per altre informazioni sulla finestra di dialogo **Cambia impostazioni**, vedere [Finestra di dialogo Cambia impostazioni &#40;Analysis Services - Dati multidimensionali&#41;](change-settings-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Esegui**  
 Fare clic su questo pulsante per elaborare gli oggetti.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Finestra di dialogo Stato elaborazione &#40;Analysis Services-Dati multidimensionali&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  
