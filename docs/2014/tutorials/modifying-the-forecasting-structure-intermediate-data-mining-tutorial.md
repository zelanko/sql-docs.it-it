---
title: Modifica della struttura di previsione (esercitazione intermedia di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030592"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modifica della struttura di previsione (Esercitazione intermedia sul data mining)
  La struttura di data mining creata nell'attività precedente contiene un singolo modello di previsione. Prima di elaborare ed esaminare il modello, è necessario alterarne leggermente la struttura e modificarne una proprietà.  
  
## <a name="modifying-the-mining-structure"></a>Modifica della struttura di data mining  
 È possibile modificare la struttura di data mining utilizzando il **struttura di Data Mining** scheda della finestra di progettazione modelli di Data Mining. Una volta creato il modello con Creazione guidata di Data Mining, è stato usato tre colonne: ReportingDate, ModelRegion e Quantity. Tuttavia, il **Forecasting** tabella contiene anche una colonna quantità che è possibile usare per prevedere l'importo delle vendite. Tramite il **struttura di Data Mining** scheda, è possibile aggiungere questa colonna dalla vista origine dati alla struttura di data mining.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Per aggiungere la colonna Amount alla struttura di data mining Forecasting  
  
1.  Nel **struttura di Data Mining** scheda della finestra di progettazione modelli di Data Mining, nelle **vista origine dati** riquadro, selezionare la colonna Amount nella tabella vTimeSeries.  
  
2.  Trascinare la colonna Amount dal **vista origine dati** riquadro dell'elenco di colonne per il **Forecasting** struttura.  
  
     La colonna Amount è ora incluso nel **Forecasting** struttura di data mining.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modifica delle colonne del modello di data mining  
 Dato che alla struttura è stata aggiunta una nuova colonna, è necessario definire in che modo la colonna verrà utilizzata dal modello. È possibile specificare come la colonna verrà utilizzata nel **modelli di Data Mining** scheda della finestra di progettazione modelli di Data Mining.  
  
 Il **modelli di Data Mining** scheda sono elencate le colonne contenenti la struttura di data mining nel **struttura** colonna della griglia e gli elenchi di colonne modello di data mining contenute nella colonna che contiene il nome del in questo caso modellare **Forecasting**. Fare clic sui nomi delle colonne per apportare modifiche. Nel **Forecasting** modello di data mining, la colonna Amount viene utilizzata come colonna di input e viene usata anche per stimare le vendite future. È pertanto necessario impostare le proprietà della colonna in modo che possa essere utilizzata sia come colonna di input che come colonna stimabile.  
  
> [!NOTE]  
>  Nel **modelli di Data Mining** scheda, è anche possibile creare nuovi modelli basati sulla stessa struttura ed è possibile modificare le proprietà di algoritmo e di colonna per ogni modello. È tuttavia necessario elaborare il modello prima che queste modifiche diventino effettive.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Per definire in che modo verrà utilizzata la colonna Amount  
  
1.  Nel **Forecasting** colonna della griglia nella **modelli di Data Mining** scheda, fare clic nella cella della riga Amount nella.  
  
2.  Selezionare **Predict** dall'elenco.  
  
     La colonna Amount è ora sia una colonna di input che una colonna stimabile.  
  
 È anche possibile modificare le proprietà delle singole colonne selezionando la colonna e aprendo la **proprietà** finestra. Per aprire la **delle proprietà** finestra, il nome della colonna e quindi scegliere **proprietà**. Se si modifica una proprietà di un singolo modello all'interno della colonna, è possibile modificare le proprietà solo di quel modello. Tuttavia, quando si modifica una proprietà all'interno di **struttura** colonna, la modifica influisce su tutti i modelli associati alla struttura. Ogni qualvolta si apportano modifiche al modello o alla struttura, è necessario ripetere l'elaborazione per osservarne gli effetti.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Personalizzazione ed elaborazione del modello di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelli di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
