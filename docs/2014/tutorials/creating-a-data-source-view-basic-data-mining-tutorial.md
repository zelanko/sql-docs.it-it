---
title: Creazione di una vista origine dati (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888643"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Creazione di una vista origine dati (Esercitazione di base sul data mining)
  Una vista origine dati si basa su un'origine dati e definisce un subset dei dati che è possibile utilizzare nelle strutture di data mining. È inoltre possibile utilizzare la vista origine dati per aggiungere colonne, creare aggregazioni e colonne calcolate nonché aggiungere viste denominate. Le viste origine dati consentono di selezionare i dati correlati al progetto, stabilire relazioni tra tabelle e modificare la struttura dei dati senza modificare l'origine dati originale. Per altre informazioni, vedere [Viste origine dati in modelli multidimensionali](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models).  
  
### <a name="to-create-a-data-source-view"></a>Per creare una vista origine dati  
  
1.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **viste origine dati**e scegliere **nuova vista origine dati**.  
  
2.  Nella pagina iniziale di **Creazione guidata vista origine dati** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione origine dati** , in **origini dati relazionali**, selezionare l'origine dati Adventure Works DW 2012 creata nell'ultima attività. Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Se si desidera creare un'origine dati, fare clic con il pulsante destro del mouse su **origini dati** e scegliere **nuova origine dati** per avviare la creazione guidata origine dati.  
  
4.  Nella pagina **Selezione tabelle e viste** selezionare gli oggetti seguenti, quindi fare clic sulla freccia destra per includerli nella nuova vista origine dati:  
  
    -   **ProspectiveBuyer (dbo)** -tabella dei potenziali acquirenti di biciclette  
  
    -   **vTargetMail (dbo)** -visualizzazione dei dati cronologici sugli acquirenti di biciclette precedenti  
  
5.  Fare clic su **Avanti**.  
  
6.  Per impostazione predefinita, nella pagina **Completamento procedura guidata** la vista origine dati è denominata Adventure Works DW 2012. Modificare il nome in `Targeted Mailing`, quindi fare clic su **fine**.  
  
     La nuova vista origine dati verrà visualizzata nella scheda **Targeted mailing. dsv [Design]** .  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esercitazione sulla creazione di &#40;un'origine dati di base sul data mining&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Creazione di una struttura &#40;di mailing mirata esercitazione di base sul data mining&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione di una vista origine dati &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
