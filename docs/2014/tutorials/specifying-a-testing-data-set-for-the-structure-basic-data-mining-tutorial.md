---
title: Specifica di un set di dati di testing per la struttura (esercitazione di base sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62720105"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>Specifica di un set di dati di testing per la struttura (Esercitazione di base sul data mining)
  Nelle schermate finali della Creazione guidata modello di data mining si suddivideranno i dati in un set di testing e un set di training. Si assegnerà quindi un nome alla struttura e si abiliterà il drill-through sul modello.  
  
## <a name="specifying-a-testing-set"></a>Specifica di un set di testing  
 La separazione dei dati in set di training e set di testing durante la creazione di una struttura di data mining consente di determinare facilmente l'accuratezza dei modelli di data mining che verranno creati successivamente. Per ulteriori informazioni sui set di testing, vedere [Training and testing data set](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-specify-the-testing-set"></a>Per specificare il set di testing  
  
1.  Nella `30`pagina **Crea set di testing** , per la **percentuale di dati per il testing**, lasciare il valore predefinito.  
  
2.  Per il **numero massimo di case nel set di dati di testing**, digitare `1000`.  
  
3.  Fare clic su **Avanti**.  
  
## <a name="specifying-drillthrough"></a>Specifica del drill-through  
 Il drill-through può essere abilitato sui modelli e sulle strutture. La casella di controllo in questa finestra di dialogo abilita il drill-through nel modello denominato. Dopo l'elaborazione del modello sarà possibile recuperare le informazioni dettagliate dai dati di training utilizzati per creare il modello.  
  
 Se anche la struttura di data mining sottostante è stata configurata per consentire il drill-through, è possibile recuperare informazioni dettagliate dai case del modello e dalla struttura di data mining, comprese le colonne non incluse nel modello di data mining. Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>Per assegnare un nome al modello e alla struttura e specificare il drill-through  
  
1.  Nella pagina **Completamento procedura guidata** Digitare `Targeted Mailing`in **Nome struttura di data mining**.  
  
2.  In **nome modello di data mining**Digitare `TM_Decision_Tree`.  
  
3.  Selezionare la casella di controllo **Consenti drill-through** .  
  
4.  Esaminare il riquadro di **Anteprima** . Si noti che vengono visualizzate solo le colonne selezionate come **chiave**, **input** o **stimabile** . Le altre colonne selezionate (ad esempio, AddressLine1) non vengono utilizzate per la compilazione del modello, ma saranno disponibili nella struttura sottostante e possono essere sottoposte a query una volta che il modello viene elaborato e distribuito.  
  
5.  Fare clic su **Fine**.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Impostazione del tipo di dati e del tipo di contenuto &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: Aggiunta ed elaborazione di modelli](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare il drill-through per un modello di data mining](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [Query drill-through &#40;&#41;di data mining](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Specificare i dati di training &#40;creazione guidata modello di data mining&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
