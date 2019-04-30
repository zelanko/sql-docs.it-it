---
title: Esercitazione di base di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d434df95a26485d4d7795d3ab960b8d2457b8ff6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185569"
---
# <a name="basic-data-mining-tutorial"></a>Esercitazione di base sul data mining
  Ecco il [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esercitazione di base di Data Mining. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornisce un ambiente integrato per la creazione di modelli di data mining e l'esecuzione di stime. In questa esercitazione, si verrà completato uno scenario per una campagna di mailing diretto in cui si usa machine learning per analizzare e identificare il comportamento di acquisto dei clienti. Verrà illustrato come utilizzare tre degli algoritmi di data mining più importanti: clustering, alberi delle decisioni e Naive Bayes. Si apprenderà anche come analizzare i risultati ottenuti utilizzando i visualizzatori modelli di data mining e creare stime e grafici di accuratezza utilizzando gli strumenti di data mining inclusi in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] verrà utilizzata per tutti gli esempi.  
  
 Quando si è a proprio agio usando strumenti di data mining, è consigliabile completare anche il [esercitazione intermedia sul Data Mining &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Nelle lezioni viene illustrato come utilizzare le previsioni, l'analisi Market basket, la serie temporale, i modelli di associazione, le tabelle nidificate e il clustering delle sequenze.  
  
## <a name="tutorial-scenario"></a>Scenario dell'esercitazione  
 In questa esercitazione è dipendenti [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] chi viene affidato l'incarico con informazioni approfondite sui clienti dell'azienda in base alla cronologia degli acquisti e quindi utilizzare tali dati per eseguire stime che possono essere utilizzate nelle iniziative di marketing. L'azienda non ha mai eseguito operazioni di data mining, quindi è necessario creare un nuovo database specifico e impostare diversi modelli di data mining.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Questa esercitazione spiega come creare e utilizzare diversi tipi di metodi di apprendimento automatici. Verrà inoltre illustrato come creare la copia di un modello di data mining e come applicare un filtro ai dati di input per ottenere risultati diversi. Successivamente, sarà possibile confrontare i risultati di entrambi i modelli utilizzando un grafico di accuratezza. Infine, verrà utilizzata la funzione di drill-through per recuperare dati aggiuntivi dalla struttura di data mining sottostante.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Il Data Mining include le seguenti funzionalità che consentono di sviluppare e confrontare più modelli predittivi e intraprendere le azioni in base ai risultati:  
  
-   *Set di Test di controllo -* quando si crea una struttura di data mining, è ora possibile dividere i dati nella struttura di data mining in set di training e set di testing. Ciò consente di testare i modelli in base a set di dati simili e di confrontare l'accuratezza di modelli correlati.  
  
-   *-Filtri dei modelli di data mining*è ora possibile associare filtri a un modello di data mining e applicarli durante il training e il testing. Ciò consente di compilare facilmente modelli correlati in base a subset di dati diversi.  
  
-   *Drill-through nei case della struttura e le colonne della struttura -* è possibile ora spostarsi facilmente dagli schemi generali del modello di data mining ai dettagli utilizzabili nell'origine dati.  
  
 L'esercitazione è suddivisa nelle lezioni seguenti:  
  
 [Lezione 1: L'analisi di preparazione dei servizi per Database di &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 In questa lezione verranno illustrate le procedure per la creazione di un nuovo database [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], l'aggiunta di un'origine dei dati a una vista origine dati e la preparazione del nuovo database per l'utilizzo con il data mining.  
  
 [Lezione 2: Compilazione di una struttura di Mailing diretto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 In questa lezione verranno illustrate le procedure per la creazione di una struttura di modello di data mining che può essere utilizzata nello scenario relativo al mailing diretto.  
  
 [Lezione 3: Aggiunta ed elaborazione di modelli](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 In questa lezione verranno illustrate le procedure per l'aggiunta di modelli a una struttura. I modelli creati verranno compilati con gli algoritmi seguenti:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes  
  
 [Lezione 4: Esplorazione dei modelli di Mailing diretto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 In questa lezione verranno illustrate le procedure per l'esplorazione e l'interpretazione dei risultati di ogni modello mediante i visualizzatori.  
  
 [Lezione 5: Testare i modelli &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 In questa lezione verranno illustrate le procedure per creare una copia di uno dei modelli di mailing diretto, aggiungere un filtro del modello di data mining per limitare i dati di training a un particolare set di clienti e valutare l'affidabilità del modello.  
  
 [Lezione 6: Creazione e utilizzo di stime &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 In questa lezione finale dell'esercitazione di base sul data mining si utilizzerà il modello per individuare i clienti che con maggiore probabilità acquisteranno una bicicletta. Verrà quindi eseguito il drill-through nei case sottostanti per ottenere informazioni di contatto.  
  
## <a name="requirements"></a>Requisiti  
 Verificare che sia installato quanto segue:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modalità multidimensionale  
  
-   Database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Per garantire una maggiore sicurezza, i database di esempio non vengono installati con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per installare i database ufficiali per [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visitare il [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) pagina e selezionare [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Quando si lavora in un'esercitazione, si potrebbe risultare più agevole spostarsi avanti e indietro tra i passaggi se si aggiunge il **argomento successivo** e **argomento precedente** pulsanti alla barra degli strumenti del Visualizzatore di documenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Soluzioni di data mining](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [Attività e procedure relative al modello di data mining](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Creazione ed esecuzione di query su modelli di Data Mining con DMX: Esercitazioni su &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
