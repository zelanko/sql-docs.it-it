---
title: 'Lezione 3: compilazione di uno scenario Market Basket (Esercitazione intermedia sul data mining) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2f1c5a8ae897284f07c3fd6c65d9735099a41fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042787"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>Lezione 3: Compilazione di uno scenario Market Basket (Esercitazione intermedia sul data mining)
  Il reparto marketing di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] intende migliorare il sito Web aziendale per promuovere le vendite. Durante l'aggiornamento del sito, si desidera essere in grado di prevedere quali siano i prodotti che i clienti potrebbero essere interessati ad acquistare sulla base dei prodotti già inclusi tra i rispettivi acquisti. Il reparto marketing desidera inoltre capire meglio il comportamento di acquisto del cliente, in modo da poter progettare il sito Web in modo da visualizzare nella stessa area gli elementi che tendono a essere acquistati insieme. Il team sa che il data mining è particolarmente utile per questo tipo di *Market basket analysis* e chiede di sviluppare un modello di data mining.  
  
 Dopo aver completato le attività di questa lezione, si otterrà un modello di data mining in cui saranno visualizzati i gruppi di articoli riferiti a precedenti transazioni del cliente. Inoltre, è possibile utilizzare il modello di data mining per prevedere gli ulteriori articoli che un cliente può essere interessato ad acquistare.  
  
 Per completare le attività in questa lezione, si utilizzeranno la soluzione e l'origine dati create nella prima lezione dell' [esercitazione intermedia sul data mining &#40;Analysis Services-Data mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Sarà possibile modificare la soluzione aggiungendo una vista origine dati che contiene le tabelle sul cliente, inclusa una tabella nidificata degli acquisti del cliente.  Si compilerà quindi un modello di data mining che utilizza l'algoritmo Microsoft Association Rules, indicato per gli scenari Market Basket.  
  
 In questa lezione sono inclusi gli argomenti seguenti:  
  
-   [Aggiunta di una vista origine dati con tabelle nidificate &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [Creazione di una struttura e di un modello di Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Modifica ed elaborazione del modello Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [Esplorazione dei modelli Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [Applicazione di filtri a una tabella nidificata in un modello di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [Stima delle associazioni &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Aggiunta di una vista origine dati con tabelle nidificate &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>Tutte le lezioni  
 [Lezione 1: creazione della soluzione intermedia di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 Lezione 3: Scenario Market basket (Esercitazione intermedia sul data mining)  
  
 [Lezione 4: compilazione di uno scenario di clustering delle sequenze &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [Lezione 5: creazione di modelli di rete neurale e di regressione logistica &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [Lezione 4: compilazione di uno scenario di clustering delle sequenze &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  
