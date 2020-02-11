---
title: 'Lezione 4: compilazione di uno scenario di clustering delle sequenze (Esercitazione intermedia sul data mining) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d34125b7b750daa1da25c9e8788172b5d9ca2c35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62710603"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>Lezione 4: Compilazione di uno scenario di clustering delle sequenze (Esercitazione intermedia sul data mining)
  Il reparto marketing di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] intende comprendere in che modo i clienti visitano il sito Web di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . L'azienda ritiene che esista un modello in base al quale i clienti inseriscono i prodotti nei rispettivi carrelli della spesa. Desidera quindi analizzare l'ordine delle sequenze di acquisto per sapere in che modo i clienti includono i prodotti tra gli acquisti. L'azienda può quindi utilizzare queste informazioni per rendere il sito Web più efficiente in modo da indurre i clienti ad acquistare altri prodotti.  
  
 Dopo aver completato le attività incluse in questa lezione, si avrà creato un modello di data mining che utilizza l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering per prevedere quale sarà il prodotto successivo che il cliente inserirà tra gli acquisti. Verranno utilizzate due versioni del modello: una analizza solo l'ordine dei prodotti inclusi tra gli acquisti e l'altra contiene dati demografici aggiuntivi del cliente per il clustering. Infine, si utilizzeranno i modelli per creare stime da utilizzare per consigliare prodotti ai clienti.  
  
 Per completare le attività della lezione, si utilizzerà la struttura di data mining Market Basket creata nella [lezione 3: creazione di uno scenario Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md). In questa lezione sono incluse le attività seguenti:  
  
-   [Creazione di una struttura del modello di data mining Sequence Clustering &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [Elaborazione del modello Sequence Clustering](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [Esplorazione del modello Sequence Clustering &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Creazione di un modello Sequence Clustering correlato &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Creazione di stime in un modello Sequence Clustering &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di una struttura del modello di data mining Sequence Clustering &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Tutte le lezioni  
 [Lezione 1: creazione della soluzione intermedia di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lezione 3: creazione di uno scenario Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 Lezione 4: Scenario di clustering delle sequenze (Esercitazione intermedia sul data mining)  
  
 [Lezione 5: creazione di modelli di rete neurale e di regressione logistica &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
