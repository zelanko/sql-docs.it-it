---
title: Esercitazione intermedia sul Data Mining (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 404b31d5-27f4-4875-bd60-7b2b8613eb1b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e8418bf91dff36a512db57c45f1d19ad18fde02
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369013"
---
# <a name="intermediate-data-mining-tutorial-analysis-services---data-mining"></a>Esercitazione intermedia sul data mining (Analysis Services - Data mining)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce un ambiente integrato per la creazione e utilizzo di modelli di data mining. È possibile eseguire facilmente l'associazione a origini dati, creare e testare più modelli sugli stessi dati e distribuire modelli da utilizzare nelle analisi predittive.  
  
 Nell'esercitazione di base sul data mining è stato descritto come utilizzare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare una soluzione di data mining e sono stati compilati tre modelli a supporto di una campagna di mailing diretto per analizzare il comportamento di acquisto dei clienti e per individuare i potenziali acquirenti.  
  
 Questa esercitazione intermedia viene compilata su tale esperienza acquisita e introduce diversi nuovi scenari, inclusi i requisiti aziendali comuni come la previsione e il Market basket analysis. Durante l'esercitazione verrà illustrato come creare un modello Time Series, un modello di associazione e un modello Sequence Clustering. Infine, verrà illustrato come utilizzare la rete neurale per esplorare le correlazioni dei dati e per utilizzare la regressione logistica per le stime.  
  
 Le lezioni sono indipendenti e possono essere completate separatamente.  
  
 Per completare le esercitazioni seguenti, l'utente deve avere familiarità con gli strumenti di data mining e con i visualizzatori dei modelli di data mining descritti nell'esercitazione di base sul data mining.  
  
 In tutti gli scenari viene utilizzata l'origine dati [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], tuttavia verranno create viste origine dati diverse per i diversi scenari. È possibile completare le lezioni in qualsiasi ordine, purché si crei innanzitutto l'origine dati.  
  
## <a name="lesson-scenarios"></a>Scenari della lezione  
 Dopo la conclusione positiva della campagna di mailing diretto, si supponga di aver ricevuto la richiesta di sfruttare le proprie conoscenze di data mining per sviluppare diversi nuovi modelli da utilizzare nella pianificazione aziendale. Di seguito vengono descritte alcune di queste attività:  
  
-   **Previsioni:** Si creerà una *time series* modello per prevedere le vendite di prodotti in diverse aree in tutto il mondo. Verranno sviluppati singoli modelli per ogni area e verrà informazioni su come usare *stime incrociate*.  
  
-   **Market basket analysis:** Si creerà un' *modello di associazione*, per analizzare raggruppamenti di prodotti acquistati durante le visite al [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] sito di e-commerce. Questo modello di analisi degli acquisti può essere utilizzato per consigliare prodotti ai clienti.  
  
-   **Analisi delle sequenze:** Si compila un *modello sequence clustering*, per analizzare l'ordine in cui i clienti acquistano i prodotti. Sulla base di questo modello è possibile pianificare le modifiche alla progettazione del sito Web o le nuove offerte di prodotti.  
  
-   **Analisi dei fattori:** Usa un' *rete neurale* modello per esplorare le possibili cause di qualità del servizio insufficiente in dati call center. Basato su informazioni approfondite del modello preliminare, si creerà una *modello di regressione logistica* per prevedere le strategie per migliorare l'esperienza dei clienti.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione viene illustrato come creare e utilizzare tipi diversi di algoritmi di data mining. L'esercitazione è suddivisa nelle lezioni seguenti:  
  
 [Lezione 1: Creazione della soluzione intermedia di Data Mining &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
 In questa lezione verrà creato un nuovo progetto basato sul database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], per supportare diverse nuove viste origine dati e molti più modelli di data mining.  
  
 [Lezione 2: Creazione di uno Scenario di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
 In questa lezione verrà creato un modello di data mining che può essere utilizzato in uno scenario di previsione. Verranno inoltre esplorati i modelli di data mining compilati con l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
 Verranno compilati modelli per le singole aree geografiche, oltre a un modello generale che può essere utilizzato per la stima incrociata.  
  
 [Lezione 3: Creazione di uno Scenario Market Basket &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
 In questa lezione verrà aggiunta una nuova vista origine dati e verrà illustrato come utilizzare le chiavi e le tabelle nidificate. In base a questi dati, verrà creato un modello di data mining che può essere utilizzato in uno scenario di analisi degli acquisti. Verranno inoltre esplorati i modelli di data mining compilati con l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
 [Lezione 4: Compilazione di una Scenario di Clustering delle sequenze &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
 In questa lezione verrà creato un modello di data mining che può essere utilizzato in uno scenario di clustering delle sequenze. Verranno inoltre esaminati i modelli di data mining compilati con l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
 [Lezione 5: Creazione di reti neurali e modelli di regressione logistica &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
 In questa lezione si creeranno alcuni modelli di data mining correlati, utilizzando Microsoft Neural Network e gli algoritmi di Microsoft Logistic Regression. Si apprenderà inoltre a utilizzare le viste origine dati per esplorare i dati sottostanti i modelli.  
  
## <a name="requirements"></a>Requisiti  
 Verificare che sia installato quanto segue:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con il database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database ufficiali per [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visitare il [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) pagina e selezionare la versione appropriata del database di esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Esercitazione su DMX per bike Buyer](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Esercitazione su DMX per Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md)  
  
  
