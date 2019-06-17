---
title: Elaborazione di modelli nella struttura Targeted Mailing (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9d8233bb-117e-4563-9302-8a5a8ad1fae2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 605088d405cbd2dcfba92a2da5fa4e07c38d8f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188232"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Elaborazione di modelli nella struttura di mailing diretto (Esercitazione di base sul data mining)
  Per poter esplorare o utilizzare i modelli di data mining creati, è necessario distribuire il progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ed elaborare la struttura e i modelli di data mining.  
  
-   *Distribuzione* invia il progetto a un server e crea gli oggetti in tale progetto nel server.  
  
-   *L'elaborazione* Popola [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oggetti con i dati da origini dati relazionali.  
  
 Per utilizzare i modelli, è innanzitutto necessario distribuirli ed elaborarli. Inoltre, quando si apportano modifiche al modello, ad esempio se si aggiungono nuovi dati, è necessario ridistribuire e rielaborare i modelli.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>Verifica della coerenza con HoldoutSeed  
 Quando si distribuisce un progetto e si elaborano la struttura e i modelli, singole righe nella struttura dei dati vengono assegnate ai set di training o di testing sulla base di un valore di inizializzazione numerico. Per impostazione predefinita, il valore di inizializzazione numerico viene calcolato in base agli attributi della struttura dei dati. Tuttavia, se si modificano alcuni aspetti del modello, il valore di inizializzazione può cambiare determinando risultati lievemente diversi. Pertanto, per assicurarsi che i risultati corrispondano a quelli descritti in questo caso, si assegnerà arbitrariamente fisse *seed holdout* di `12`. Il valore di inizializzazione dei dati di controllo viene utilizzato per inizializzare l'algoritmo di campionamento e garantisce che i dati vengano partizionati approssimativamente nello stesso modo per tutte le strutture di data mining e i relativi modelli.  
  
 Questo valore non influisce sul numero di case nel set di training, ma garantisce semplicemente che venga utilizzato lo stesso metodo di partizionamento ogni volta che si compila il modello.  
  
 Per altre informazioni sul valore di inizializzazione dei dati di controllo, vedere [Training e Testing Data Sets](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-set-the-holdout-seed"></a>Per impostare il valori di inizializzazione di controllo  
  
1.  Fare clic sui **struttura di Data Mining** scheda o il **modelli di Data Mining** scheda Progettazione modelli di Data Mining in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     **Targeted Mailing MiningStructure** vengono visualizzati nei **proprietà** riquadro.  
  
2.  Verificare che il **delle proprietà** riquadro sia aperto premendo **F4**.  
  
3.  Assicurarsi che **CacheMode** è impostata su **KeepTrainingCases**.  
  
4.  Immettere `12` per **HoldoutSeed**.  
  
## <a name="deploying-and-processing-the-models"></a>Distribuzione ed elaborazione dei modelli  
 Progettazione modelli di Data Mining, è possibile decidere quali oggetti da elaborare, a seconda della portata delle modifiche apportate al modello o i dati sottostanti:  
  
 Per questa attività, poiché i dati e i modelli sono nuovi, sarà necessario elaborare contemporaneamente la struttura e tutti i modelli.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>Per distribuire il progetto ed elaborare tutti i modelli di data mining  
  
1.  Nel **modello di Data Mining** dal menu **Elabora struttura di Data Mining e tutti i modelli**.  
  
     Se sono state apportate modifiche alla struttura, prima di elaborare i modelli verrà richiesto di compilare e distribuire il progetto. Scegliere **Sì**.  
  
2.  Fare clic su **eseguiti** nel **elaborazione struttura di Data Mining - Targeted Mailing** nella finestra di dialogo.  
  
     Verrà aperta la finestra di dialogo **Stato elaborazione** in cui vengono visualizzate informazioni sull'elaborazione dei modelli. L'elaborazione dei modelli potrebbe richiedere tempi lunghi, a seconda del computer in uso.  
  
3.  Fare clic su **Chiudi** nella finestra di dialogo **Stato elaborazione** dopo che l'elaborazione dei modelli è stata completata.  
  
4.  Fare clic su **Close** nel **Processing Mining Structure - \<struttura >** nella finestra di dialogo.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Aggiunta di nuovi modelli alla struttura di Mailing diretto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Esplorazione dei modelli di Mailing diretto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
