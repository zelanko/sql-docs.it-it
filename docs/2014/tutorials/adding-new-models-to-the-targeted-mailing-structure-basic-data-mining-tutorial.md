---
title: Aggiunta di nuovi modelli alla struttura Targeted Mailing (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822638"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>Aggiunta di nuovi modelli alla struttura Targeted Mailing (Esercitazione di base sul data mining)
  In questa attività verranno definiti due modelli aggiuntivi utilizzando la scheda modelli di data mining di progettazione **modelli** di data mining. Per creare i modelli, verranno utilizzati gli algoritmi Microsoft Clustering e Microsoft Naive Bayes, per la loro capacità di stimare un valore discreto (ad esempio, l'acquisto di una bicicletta). Per ulteriori informazioni su questi algoritmi, vedere [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) e [algoritmo Microsoft Naive Bayes](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>Per creare un modello di data mining Clustering  
  
1.  Passare alla scheda **modelli** di data mining in Progettazione modelli di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]data mining in.  
  
     Si noti che nella finestra di progettazione vengono visualizzate due colonne, una per la struttura di `TM_Decision_Tree` data mining e una per il modello di data mining creato nella lezione precedente.  
  
2.  Fare clic con il pulsante destro del mouse sulla colonna **struttura** e scegliere **nuovo modello di data mining**.  
  
3.  Nella finestra di dialogo **nuovo modello di data mining** , in **nome modello**, digitare `TM_Clustering`.  
  
4.  In **Nome algoritmo**selezionare **clustering Microsoft**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 Il nuovo modello verrà ora visualizzato nella scheda modelli di data mining di progettazione **modelli** di data mining. Questo modello, creato con l' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Clustering, raggruppa i clienti con caratteristiche simili in cluster e prevede l'acquisto di biciclette per ogni cluster. Sebbene sia possibile modificare l'utilizzo e le proprietà delle colonne per il nuovo modello, per questa `TM_Clustering` esercitazione non sono necessarie modifiche al modello.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Per creare un modello di data mining Naive Bayes  
  
1.  Nella scheda **modelli** di data mining di progettazione modelli di data mining, colonna **struttura** clickthe e selezionare **nuovo modello di data mining**.  
  
2.  Nella finestra di dialogo **nuovo modello di data mining** , in **nome modello**, digitare `TM_NaiveBayes`.  
  
3.  In **Nome algoritmo**selezionare **Microsoft Naive Bayes**, quindi fare clic su **OK**.  
  
     Viene visualizzato un messaggio che informa che [!INCLUDE[msCoName](../includes/msconame-md.md)] l'algoritmo Naive Bayes non supporta le colonne **Age** e **Yearly Income** , che sono continue.  
  
4.  Fare clic su **Sì** per confermare il messaggio e continuare.  
  
 Un nuovo modello verrà visualizzato nella scheda modelli di data mining di progettazione **modelli** di data mining. Sebbene sia possibile modificare l'utilizzo e le proprietà delle colonne per tutti i modelli in questa scheda, per questa `TM_NaiveBayes` esercitazione non sono necessarie modifiche al modello.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Elaborazione di modelli nella struttura di mailing diretto &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta di modelli di data mining a una struttura &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [Progettazione modelli di data mining](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Spostamento di oggetti di data mining](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
