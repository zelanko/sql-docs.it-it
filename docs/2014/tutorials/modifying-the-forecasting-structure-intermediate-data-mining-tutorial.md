---
title: Modifica della struttura di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301295"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modifica della struttura di previsione (Esercitazione intermedia sul data mining)
  La struttura di data mining creata nell'attività precedente contiene un singolo modello di previsione. Prima di elaborare ed esaminare il modello, è necessario alterarne leggermente la struttura e modificarne una proprietà.  
  
## <a name="modifying-the-mining-structure"></a>Modifica della struttura di data mining  
 È possibile modificare la struttura di data mining utilizzando la scheda **struttura** di data mining di progettazione modelli di data mining. Quando è stato creato il modello con Creazione guidata modello di data mining, sono state utilizzate solo tre colonne: ReportingDate, ModelRegion e Quantity. Tuttavia, la tabella **Forecasting** contiene anche una colonna Amount, che è possibile utilizzare per prevedere la quantità di vendite. Utilizzando la scheda **struttura di data mining** , è possibile aggiungere questa colonna dalla vista origine dati alla struttura di data mining.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Per aggiungere la colonna Amount alla struttura di data mining Forecasting  
  
1.  Nel riquadro **vista origine dati** della scheda **struttura** di data mining di progettazione modelli di data mining selezionare la colonna Amount nella tabella vTimeSeries.  
  
2.  Trascinare la colonna Amount dal riquadro **vista origine dati** nell'elenco di colonne per la struttura di **previsione** .  
  
     La colonna Amount è ora inclusa nella struttura di data mining **Forecasting** .  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modifica delle colonne del modello di data mining  
 Dato che alla struttura è stata aggiunta una nuova colonna, è necessario definire in che modo la colonna verrà utilizzata dal modello. È possibile specificare il modo in cui la colonna verrà utilizzata nella scheda modelli di data mining di progettazione **modelli** di data mining.  
  
 Nella scheda **modelli di data mining** sono elencate le colonne contenute nella struttura di data mining nella colonna **struttura** della griglia ed elencate le colonne contenute nel modello di data mining nella colonna con il nome del modello, in questo caso la **previsione**. Fare clic sui nomi delle colonne per apportare modifiche. Nel modello di data mining **Forecasting** la colonna Amount viene utilizzata come colonna di input e viene utilizzata anche per prevedere le vendite future. È pertanto necessario impostare le proprietà della colonna in modo che possa essere utilizzata sia come colonna di input che come colonna stimabile.  
  
> [!NOTE]  
>  Nella scheda **modelli di data mining** è inoltre possibile creare nuovi modelli basati sulla stessa struttura ed è possibile modificare le proprietà dell'algoritmo e della colonna per ogni modello. È tuttavia necessario elaborare il modello prima che queste modifiche diventino effettive.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Per definire in che modo verrà utilizzata la colonna Amount  
  
1.  Nella colonna **Forecasting** della griglia nella scheda modelli di **data mining** fare clic sulla cella nella riga Amount.  
  
2.  Selezionare **stima** dall'elenco.  
  
     La colonna Amount è ora sia una colonna di input che una colonna stimabile.  
  
 È inoltre possibile modificare le proprietà delle singole colonne selezionando la colonna e aprendo la finestra **Proprietà** . Per aprire la finestra **Proprietà** , fare clic con il pulsante destro del mouse sul nome della colonna, quindi scegliere **Proprietà**. Se si modifica una proprietà di un singolo modello all'interno della colonna, è possibile modificare le proprietà solo di quel modello. Tuttavia, quando si modifica una proprietà all'interno della colonna della **struttura** , la modifica influiscono su tutti i modelli associati alla struttura. Ogni qualvolta si apportano modifiche al modello o alla struttura, è necessario ripetere l'elaborazione per osservarne gli effetti.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Personalizzazione ed elaborazione del modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelli di data mining &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
