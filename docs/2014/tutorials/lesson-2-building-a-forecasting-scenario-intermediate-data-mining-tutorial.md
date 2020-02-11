---
title: 'Lezione 2: compilazione di uno scenario di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee814dc0891e70dfeccf2b96383d1d7b5c324aa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62931524"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>Lezione 2: Compilazione di uno scenario di previsione (Esercitazione intermedia sul data mining)
  In qualità di analista delle vendite di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], si supponga di aver ricevuto la richiesta di stimare le vendite dei prodotti del prossimo anno. In particolare, viene richiesto di confrontare le previsioni per le diverse regioni e linee di prodotti. È stato inoltre richiesto di determinare se le vendite dei singoli prodotti sono da mettere in relazione al periodo dell'anno.  
  
 Per trovare le informazioni richieste, in questa lezione si riepilogano i dati di vendita mensili dell'azienda e le cifre sulle vendite verranno suddivise in tre regioni: Europa, America del nord e Pacifico.  
  
 Dopo aver completato le attività di questa lezione, sarà possibile rispondere alle domande seguenti:  
  
-   In che modo le vendite di modelli diversi di biciclette cambiano nel corso del tempo?  
  
-   Esistono differenze tra i modelli di vendita nelle tre aree?  
  
-   È possibile prevedere i periodi di massima vendita?  
  
 È possibile completare la lezione in due parti:  
  
-   Nella prima parte si illustrano i concetti di base relativi alla creazione e all'utilizzo di un modello Time Series.  
  
-   Nella seconda parte viene illustrata la creazione di un modello Time Series generale, basato su tutte le aree. È possibile utilizzare questo modello generale per la *stima incrociata*.  
  
 Per completare le attività di questa lezione, elencate di seguito, verrà utilizzata l' [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] origine dati creata nella [lezione 1: creazione della soluzione intermedia di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md).  
  
> [!WARNING]  
>  Le date nel database di esempio [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] sono state aggiornate per questa versione. Se si utilizza una versione precedente di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], è possibile compilare il modello seguendo questi passaggi, ma è possibile che vengano visualizzati risultati diversi.  
  
 **Creazione di un modello di stima semplice**  
  
-   [Aggiunta di una vista origine dati per la previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [Creazione di una struttura e di un modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Modifica della struttura di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [Personalizzazione ed elaborazione del modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [Esplorazione del modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [Creazione di stime basate su serie temporali &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **Creazione di un modello di stima generico per l'esecuzione di stime incrociate**  
  
-   [Stime avanzate basate su serie temporali &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [Stime basate su serie temporali che utilizzano dati aggiornati &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [Stime basate su serie temporali che utilizzano dati sostitutivi &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [Confronto delle stime per i modelli di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Aggiunta di una vista origine dati per la previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [Informazioni sui requisiti per un modello Time Series &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>Tutte le lezioni  
 [Lezione 1: creazione della soluzione intermedia di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 Lezione 2: Scenario di previsione (Esercitazione intermedia sul data mining)  
  
 [Lezione 3: creazione di uno scenario Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lezione 4: compilazione di uno scenario di clustering delle sequenze &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [Lezione 5: creazione di modelli di rete neurale e di regressione logistica &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
