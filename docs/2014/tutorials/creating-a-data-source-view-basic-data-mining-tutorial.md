---
title: Creazione di un tipo di dati di origine vista (esercitazione di base di Data Mining) | Microsoft Docs
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
ms.openlocfilehash: b11844e6b184099a9c6146d290a0dc081429f5d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273403"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Creazione di una vista origine dati (Esercitazione di base sul data mining)
  Una vista origine dati si basa su un'origine dati e definisce un subset dei dati che è possibile utilizzare nelle strutture di data mining. È inoltre possibile utilizzare la vista origine dati per aggiungere colonne, creare aggregazioni e colonne calcolate nonché aggiungere viste denominate. Le viste origine dati consentono di selezionare i dati correlati al progetto, stabilire relazioni tra tabelle e modificare la struttura dei dati senza modificare l'origine dati originale. Per altre informazioni, vedere [Viste origine dati in modelli multidimensionali](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
### <a name="to-create-a-data-source-view"></a>Per creare una vista origine dati  
  
1.  Nelle **Esplora soluzioni**, fare doppio clic su **viste origine dati**e selezionare **nuova vista origine dati**.  
  
2.  Nella pagina iniziale di **Creazione guidata vista origine dati** fare clic su **Avanti**.  
  
3.  Nel **Vybrat Zdroj** nella pagina **origini dati relazionali**, selezionare l'origine dati Adventure Works DW 2012 creata nell'ultima attività. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se si desidera creare un'origine dati, fare doppio clic su **Zdroje dat** e quindi fare clic su **nuova origine dati** per avviare la creazione guidata origine dati.  
  
4.  Nel **selezione tabelle e viste** pagina, selezionare gli oggetti seguenti e quindi fare clic sulla freccia a destra per includerle nella nuova vista origine dati:  
  
    -   **ProspectiveBuyer (dbo)** -tabella di potenziali acquirenti di biciclette  
  
    -   **vTargetMail (dbo)** -visualizzazione dei dati cronologici relativi precedenti acquirenti di biciclette  
  
5.  Scegliere **Avanti**.  
  
6.  Nel **Completamento procedura guidata** pagina, per impostazione predefinita la vista origine dati è denominata Adventure Works DW 2012. Modificare il nome in `Targeted Mailing`, quindi fare clic su **fine**.  
  
     La nuova vista origine dati viene aperto nel **destinazione DSV [Progettazione]** scheda.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di un'origine dati &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Compilazione di una struttura di Mailing diretto &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione di una vista origine dati &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)  
  
  
