---
title: Convalida di modelli e utilizzo di modelli per la stima (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97268dac1fef029bc35ff702ace0d422ee296d65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065494"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>Convalida e utilizzo dei modelli per le stime (componenti aggiuntivi Data Mining per Excel)
  Il test e la convalida del modello rappresentano un passaggio importante del processo di data mining. Prima di distribuire i modelli in un ambiente di produzione, è fondamentale conoscerne l'efficacia in caso di applicazione a dati reali.  
  
 I componenti aggiuntivi Data mining includono strumenti che consentono di testare i modelli compilati e di creare stime e indicazioni utilizzando i modelli.  
  
## <a name="accuracy-chart"></a>Grafico di accuratezza  
 La procedura guidata **grafico di accuratezza** consente di creare una query di stima e di valutare le prestazioni di un modello di data mining creando un grafico di accuratezza o un grafico a dispersione. I grafici di accuratezza consentono di distinguere modelli quasi identici presenti in una struttura e di determinare quale sia il modello in grado di offrire le stime più accurate.  
  
 [Grafico di accuratezza &#40;SQL Server componenti aggiuntivi Data mining&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>Matrice di classificazione  
 La procedura guidata **matrice di classificazione** consente di creare una query di stima per valutare le prestazioni di un modello di classificazione. L'output è rappresentato da un grafico di riepilogo delle stime accurate e non accurate eseguite dal modello. Tale matrice è uno strumento estremamente utile in quanto mostra non soltanto la frequenza dei valori stimati correttamente dal modello, ma anche i valori che il modello stima con maggiore frequenza in modo non corretto.  
  
 [Matrice di classificazione &#40;SQL Server i componenti aggiuntivi Data mining&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>Grafico profitti  
 La procedura guidata **grafico dei profitti** consente di valutare i vantaggi derivanti dall'utilizzo di un modello di data mining e di valutare i costi di falsi positivi e falsi negativi  
  
 Questo tipo di grafico misura l'accuratezza della stima del modello e incorpora i costi unitari e totali specificati.  
  
 [Grafico dei profitti &#40;SQL Server i componenti aggiuntivi Data Mining&#41;](profit-chart-sql-server-data-mining-add-ins.md).  
  
## <a name="cross-validation"></a>Convalida incrociata  
 La convalida incrociata è una tecnica consolidata di data mining utilizzata per valutare la validità di un set di dati e l'accuratezza di un modello di data mining nel set di dati. Consente di dividere un set di dati in subset e quindi di creare in modo iterativo modelli in ogni subset e di eseguirne il training e il testing.  
  
 La procedura guidata **convalida incrociata** consente di specificare il numero di riduzioni per cui dividere i dati, quindi fornisce un report di convalida incrociata che descrive statisticamente le differenze tra queste sezioni incrociate. In base al report, è possibile determinare se il modello è efficace per tutti i dati di training o se è appropriato per un particolare subset.  
  
 [Convalida incrociata &#40;SQL Server componenti aggiuntivi Data mining&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>Procedura guidata Query  
 La procedura guidata **query** è uno strumento interattivo che consente di compilare una query di stima. Le query rappresentano il modo in cui vengono generare indicazioni, previsioni future e così via.  
  
 Nella procedura guidata **query** è possibile selezionare un modello e quindi fornire dati di input, come singoli valori o da una tabella o un intervallo, e la procedura guidata consente di selezionare le colonne da restituire. È inoltre possibile aggiungere le funzioni alla query per generare i punteggi di probabilità e altre statistiche utili.  
  
 [&#40;di query SQL Server componenti aggiuntivi Data mining&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>Editor query avanzata  
 L' **editor di query avanzato** è un set interattivo di finestre di dialogo che consente di compilare tutti i tipi di istruzioni DMX, dall'esecuzione di query personalizzate per la creazione e il training di nuovi modelli, l'eliminazione di modelli o la creazione di nuovi set di dati.  
  
 [Editor avanzato query di data mining](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione e pulizia dei dati](exploring-and-cleaning-data.md)   
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Distribuzione e scalabilità di modelli di data mining &#40;componenti aggiuntivi Data mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
