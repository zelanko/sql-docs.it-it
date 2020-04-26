---
title: Elaborazione di modelli nella struttura di mailing diretto (esercitazione di base sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188232"
---
# <a name="processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Elaborazione di modelli nella struttura di mailing diretto (Esercitazione di base sul data mining)
  Per poter esplorare o utilizzare i modelli di data mining creati, è necessario distribuire il progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ed elaborare la struttura e i modelli di data mining.  
  
-   La *distribuzione* invia il progetto a un server e crea qualsiasi oggetto in tale progetto nel server.  
  
-   L' *elaborazione* popola [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gli oggetti con dati provenienti da origini dati relazionali.  
  
 Per utilizzare i modelli, è innanzitutto necessario distribuirli ed elaborarli. Inoltre, quando si apportano modifiche al modello, ad esempio se si aggiungono nuovi dati, è necessario ridistribuire e rielaborare i modelli.  
  
## <a name="ensuring-consistency-with-holdoutseed"></a>Verifica della coerenza con HoldoutSeed  
 Quando si distribuisce un progetto e si elaborano la struttura e i modelli, singole righe nella struttura dei dati vengono assegnate ai set di training o di testing sulla base di un valore di inizializzazione numerico. Per impostazione predefinita, il valore di inizializzazione numerico viene calcolato in base agli attributi della struttura dei dati. Tuttavia, se si modificano alcuni aspetti del modello, il valore di inizializzazione può cambiare determinando risultati lievemente diversi. Pertanto, per garantire che i risultati corrispondano a quelli descritti in questo articolo, verrà assegnato arbitrariamente un valore di *inizializzazione* di un `12`dato di lavoro fisso. Il valore di inizializzazione dei dati di controllo viene utilizzato per inizializzare l'algoritmo di campionamento e garantisce che i dati vengano partizionati approssimativamente nello stesso modo per tutte le strutture di data mining e i relativi modelli.  
  
 Questo valore non influisce sul numero di case nel set di training, ma garantisce semplicemente che venga utilizzato lo stesso metodo di partizionamento ogni volta che si compila il modello.  
  
 Per ulteriori informazioni sul valore di inizializzazione di [controllo, vedere set di dati di training e di testing](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-set-the-holdout-seed"></a>Per impostare il valori di inizializzazione di controllo  
  
1.  Fare clic sulla scheda **struttura** di data mining o modelli di data **mining** in Progettazione modelli [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]di data mining in.  
  
     **Targeted Mailing MiningStructure** viene visualizzato nel riquadro **Proprietà** .  
  
2.  Verificare che il riquadro **Proprietà** sia aperto premendo **F4**.  
  
3.  Verificare che **CacheMode** sia impostato su **KeepTrainingCases**.  
  
4.  Immettere `12` per **HoldoutSeed**.  
  
## <a name="deploying-and-processing-the-models"></a>Distribuzione ed elaborazione dei modelli  
 In Progettazione modelli di data mining è possibile decidere quali oggetti elaborare, a seconda dell'ambito delle modifiche apportate al modello o ai dati sottostanti:  
  
 Per questa attività, poiché i dati e i modelli sono nuovi, sarà necessario elaborare contemporaneamente la struttura e tutti i modelli.  
  
#### <a name="to-deploy-the-project-and-process-all-the-mining-models"></a>Per distribuire il progetto ed elaborare tutti i modelli di data mining  
  
1.  Scegliere **Elabora struttura di data mining e tutti i modelli**dal menu **modello di data mining** .  
  
     Se sono state apportate modifiche alla struttura, prima di elaborare i modelli verrà richiesto di compilare e distribuire il progetto. Fare clic su **Sì**.  
  
2.  Fare clic su **Esegui** nella finestra di dialogo **Elabora struttura di data mining-Targeted Mailing** .  
  
     Verrà aperta la finestra di dialogo **Stato elaborazione** in cui vengono visualizzate informazioni sull'elaborazione dei modelli. L'elaborazione dei modelli potrebbe richiedere tempi lunghi, a seconda del computer in uso.  
  
3.  Fare clic su **Chiudi** nella finestra di dialogo **Stato elaborazione** dopo che l'elaborazione dei modelli è stata completata.  
  
4.  Fare clic su **Chiudi** nella finestra di dialogo **Elabora struttura di data \<mining-struttura>** .  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Aggiunta di nuovi modelli alla struttura Targeted Mailing &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: esplorazione dei modelli di mailing diretto &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
