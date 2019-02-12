---
title: Specifica un Set di dati di Testing per la struttura (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21eaa86fb1ff594e8b9d2b779b787276ee13ab4b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028892"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>Specifica di un set di dati di testing per la struttura (Esercitazione di base sul data mining)
  Nelle schermate finali della Creazione guidata modello di data mining si suddivideranno i dati in un set di testing e un set di training. Si assegnerà quindi un nome alla struttura e si abiliterà il drill-through sul modello.  
  
## <a name="specifying-a-testing-set"></a>Specifica di un set di testing  
 La separazione dei dati in set di training e set di testing durante la creazione di una struttura di data mining consente di determinare facilmente l'accuratezza dei modelli di data mining che verranno creati successivamente. Per altre informazioni sui set di testing, vedere [Training e Testing Data Sets](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-specify-the-testing-set"></a>Per specificare il set di testing  
  
1.  Nel **crea Set di Testing** pagina, per **percentuale dei dati per i test**, lasciare il valore predefinito di `30`.  
  
2.  Per la **numero massimo di case nel set di dati**, tipo `1000`.  
  
3.  Scegliere **Avanti**.  
  
## <a name="specifying-drillthrough"></a>Specifica del drill-through  
 Il drill-through può essere abilitato sui modelli e sulle strutture. La casella di controllo in questa finestra di dialogo abilita il drill-through nel modello denominato. Dopo l'elaborazione del modello sarà possibile recuperare le informazioni dettagliate dai dati di training utilizzati per creare il modello.  
  
 Se anche la struttura di data mining sottostante è stata configurata per consentire il drill-through, è possibile recuperare informazioni dettagliate dai case del modello e dalla struttura di data mining, comprese le colonne non incluse nel modello di data mining. Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>Per assegnare un nome al modello e alla struttura e specificare il drill-through  
  
1.  Nel **Completamento procedura guidata** nella pagina **nome struttura di Data Mining**, tipo `Targeted Mailing`.  
  
2.  Nelle **nome del modello di Data Mining**, tipo `TM_Decision_Tree`.  
  
3.  Selezionare il **Consenti drill-through** casella di controllo.  
  
4.  Rivedere le **Preview** riquadro. Si noti che solo le colonne selezionate come **Key**, **Input** oppure **stimabile** vengono visualizzati. Le altre colonne selezionate (ad esempio, AddressLine1) non vengono utilizzate per la compilazione del modello, ma saranno disponibili nella struttura sottostante e possono essere sottoposte a query una volta che il modello viene elaborato e distribuito.  
  
5.  Scegliere **Fine**.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Specifica il tipo di dati e il tipo di contenuto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: Aggiunta ed elaborazione di modelli](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare il drill-through per un modello di Data Mining](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [Query drill-through &#40;Data mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Specificare i dati di Training &#40;Creazione guidata di Data Mining&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
