---
title: Esercitazione su DMX per la stima basata su serie temporali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1623f824c062c270268323fd45ebf0e9533c8788
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044186"
---
# <a name="time-series-prediction-dmx-tutorial"></a>Esercitazione su DMX per le stime basate su serie temporali
  In questa esercitazione verrà illustrato come creare una struttura di data mining Time Series e tre modelli di data mining Time Series personalizzati, quindi eseguire stime tramite tali modelli.  
  
 I modelli di data mining si basano sui dati contenuti nel database di esempio [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], in cui sono memorizzati i dati relativi alla società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] è una grande società multinazionale.  
  
## <a name="tutorial-scenario"></a>Scenario dell'esercitazione  
 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha deciso di utilizzare il data mining per generare proiezioni di vendita. Sono già stati compilati alcuni modelli di previsione regionali; Per ulteriori informazioni, vedere [lezione 2: compilazione di uno scenario di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md). Il reparto vendite deve essere tuttavia in grado di aggiornare periodicamente il modello di data mining con i nuovi dati sulle vendite. Desidera inoltre personalizzare i modelli per fornire proiezioni diverse.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in sono disponibili diversi strumenti che possono essere utilizzati per completare questa [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attività:  
  
-   Linguaggio di query DMX (Data Mining Extensions)  
  
-   Algoritmo Microsoft Time Series  
  
-   L'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series consente di creare modelli che possono essere utilizzati per la stima di dati temporali. DMX (Data Mining Extensions) è un linguaggio di query incluso in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che è possibile utilizzare per creare modelli di data mining e query di stima.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Questa esercitazione presuppone che l'utente abbia già familiarità con gli oggetti utilizzati in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per creare modelli di data mining. Se in precedenza non è stata creata una struttura di data mining o un modello di data mining tramite DMX, vedere l' [esercitazione DMX Bike Buyer](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
 L'esercitazione è suddivisa nelle lezioni seguenti:  
  
 [Lezione 1: Creazione di un modello di data mining Time Series e di una struttura di data mining](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 In questa lezione verrà illustrato come utilizzare l'istruzione `CREATE MINING MODEL` per aggiungere un nuovo modello di previsione e un modello di data mining correlato.  
  
 [Lezione 2: Aggiunta di modelli di data mining alla struttura di data mining Time Series](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 In questa lezione verrà illustrato come utilizzare l'istruzione ALTER MINING STRUCTURE per aggiungere nuovi modelli di data mining a una struttura di serie temporali. Verrà inoltre illustrato come personalizzare l'algoritmo utilizzato per l'analisi di una serie temporale.  
  
 [Lezione 3: Elaborazione di strutture e modelli Time Series](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 In questa lezione verrà illustrato come eseguire il training dei modelli utilizzando l'istruzione `INSERT INTO` e popolando la struttura con i dati del database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
 [Lezione 4: Creazione di stime basate su serie temporali utilizzando DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 In questa lezione verrà illustrato come creare stime basate su serie temporali.  
  
 [Lezione 5: Estensione del modello Time Series](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 In questa lezione verrà illustrato come utilizzare il parametro `EXTEND_MODEL_CASES` per aggiornare il modello con nuovi dati durante l'esecuzione di stime.  
  
## <a name="requirements"></a>Requisiti  
 Prima di eseguire l'esercitazione, verificare che sia installato quanto segue:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   Il database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio ufficiali [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]per, vedere [http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417) o nel Microsoft SQL Server esempi e progetti della community Home page nella sezione Microsoft SQL Server esempi di prodotti. Fare clic su **database**, quindi fare clic sulla scheda **releases** e selezionare i database desiderati.  
  
> [!NOTE]  
>  Quando si esaminano le esercitazioni, è consigliabile aggiungere i pulsanti **argomento successivo** e **argomento precedente** alla barra degli strumenti del Visualizzatore di documenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione di base sul data mining](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
