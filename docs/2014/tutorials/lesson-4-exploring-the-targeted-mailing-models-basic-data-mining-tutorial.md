---
title: 'Lezione 4: esplorazione dei modelli di mailing diretto (esercitazione di base sul data mining) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e00c5b9-a9f8-4503-99ee-377c9cc02d7f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97db61dc3b9adf2e345957c8e08aa752e51286e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312147"
---
# <a name="lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial"></a>Lezione 4: Esplorazione dei modelli di mailing diretto (Esercitazione di base sul data mining)
  Dopo avere elaborato i modelli nel progetto, è possibile esplorarli per individuare tendenze interessanti. Poiché l'analisi dei numeri dei modelli può risultare difficile e complessa, SQL Server Data Mining offre alcuni strumenti visivi che consentono di analizzare i dati e comprendere le regole e le relazioni che gli algoritmi hanno individuato all'interno dei dati. È inoltre possibile utilizzare vari test di accuratezza per convalidare il set di dati o per individuare il modello che garantisce le prestazioni migliori prima di distribuirlo.  
  
 Quando si utilizza [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per esplorare i modelli, ogni modello creato viene elencato nella scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining. Per esplorare i modelli, è possibile utilizzare i visualizzatori. Questi visualizzatori sono disponibili anche in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Ognuno degli algoritmi utilizzati per compilare un modello in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restituisce un risultato di tipo diverso. Di conseguenza, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sono disponibili visualizzatori personalizzati per ogni tipo di modello di apprendimento automatico.  
  
 Per informazioni dettagliate, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce anche un visualizzatore HTML, denominato **Generic Content Tree Viewer**, che consente di visualizzare informazioni dettagliate sui dati del modello e sui modelli rilevati in un formato semi-tabulare. Per altre informazioni, vedere [Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
 In questa lezione verranno analizzati dei tre modelli creati. Ogni tipo di modello è basato su un algoritmo diverso e fornisce informazioni diverse sui dati.  
  
-   Il modello Decision Trees offre informazioni sui fattori che influiscono sull'acquisto di biciclette.  
  
-   Il modello di clustering raggruppa i clienti per attributi che includono il comportamento relativo all'acquisto di biciclette e altri attributi selezionati.  
  
-   Il modello Naive Bayes consente di esplorare la relazione tra attributi diversi.  
  
 Per ulteriori informazioni su ogni visualizzatore dei modelli di data mining, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello di clustering &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello Naive Bayes &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
 Tutti e tre i modelli possono essere visualizzati utilizzando **Generic Content Tree Viewer**, per estrarre formule, valori dei dati e così via.  
  
## <a name="first-task-in-lesson"></a>Prima attività della lezione  
 [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-lesson"></a>Lezione precedente  
 [Lezione 3: Aggiunta ed elaborazione di modelli](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 5: Testing models &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Attività e procedure relative al Visualizzatore modello di data mining](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Visualizzatori modello di data mining](../../2014/analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
