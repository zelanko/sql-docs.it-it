---
title: Convalida dei modelli e utilizzo dei modelli per la stima (Data componenti aggiuntivi Data Mining per Excel) | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065494"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>Convalida e utilizzo dei modelli per le stime (componenti aggiuntivi Data Mining per Excel)
  Il test e la convalida del modello rappresentano un passaggio importante del processo di data mining. Prima di distribuire i modelli in un ambiente di produzione, è fondamentale conoscerne l'efficacia in caso di applicazione a dati reali.  
  
 I componenti aggiuntivi Data mining includono strumenti che consentono di testare i modelli compilati e di creare stime e indicazioni utilizzando i modelli.  
  
## <a name="accuracy-chart"></a>Grafico di accuratezza  
 Il **grafico di accuratezza** procedura guidata consente di creare una query di stima e valutare le prestazioni di un modello di data mining mediante la creazione di un grafico di accuratezza o un grafico a dispersione. I grafici di accuratezza consentono di distinguere modelli quasi identici presenti in una struttura e di determinare quale sia il modello in grado di offrire le stime più accurate.  
  
 [Grafico di accuratezza &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>Matrice di classificazione  
 Il **matrice di classificazione** procedura guidata consente di creare una query di stima per valutare le prestazioni di un modello di classificazione. L'output è rappresentato da un grafico di riepilogo delle stime accurate e non accurate eseguite dal modello. Tale matrice è uno strumento estremamente utile in quanto mostra non soltanto la frequenza dei valori stimati correttamente dal modello, ma anche i valori che il modello stima con maggiore frequenza in modo non corretto.  
  
 [Matrice di classificazione &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>Grafico profitti  
 Il **grafico dei profitti** procedura guidata consente di ponderare i vantaggi dell'uso di un modello di data mining e valutare i costi di falsi positivi e falsi negativi  
  
 Questo tipo di grafico misura l'accuratezza della stima del modello e incorpora i costi unitari e totali specificati.  
  
 [Grafico profitti &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md).  
  
## <a name="cross-validation"></a>Convalida incrociata  
 La convalida incrociata è una tecnica consolidata di data mining utilizzata per valutare la validità di un set di dati e l'accuratezza di un modello di data mining nel set di dati. Consente di dividere un set di dati in subset e quindi di creare in modo iterativo modelli in ogni subset e di eseguirne il training e il testing.  
  
 Il **la convalida incrociata** procedura guidata consente di specificare il numero di riduzioni in cui suddividere i dati e quindi fornisce un report di convalida incrociata che descrive statisticamente le differenze tra queste sezioni incrociate. In base al report, è possibile determinare se il modello è efficace per tutti i dati di training o se è appropriato per un particolare subset.  
  
 [La convalida incrociata &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>Procedura guidata Query  
 Il **Query** procedura guidata è uno strumento interattivo che consente di compilare una query di stima. Le query rappresentano il modo in cui vengono generare indicazioni, previsioni future e così via.  
  
 Nel **Query** procedura guidata, scegli un modello e quindi fornire i dati di input, come valori singoli o da una tabella o un intervallo e la procedura guidata consente di selezionare le colonne da restituire. È inoltre possibile aggiungere le funzioni alla query per generare i punteggi di probabilità e altre statistiche utili.  
  
 [Query &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>Editor avanzato query  
 Il **Editor avanzato Query di** è un set di finestre di dialogo interattivo che consente di compilare tutti i tipi di istruzioni DMX, dall'esecuzione di query personalizzate per la creazione e training di nuovi modelli, l'eliminazione di modelli o imposta la creazione di nuovi dati.  
  
 [Editor avanzato query di data mining](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione e pulizia dei dati](exploring-and-cleaning-data.md)   
 [Creazione di un modello di Data Mining](creating-a-data-mining-model.md)   
 [Distribuzione e scalabilità di modelli di Data Mining &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
