---
title: Aggiunta di dati di un vista di origine per la previsione (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f60ea2b2a642cf9435ed8366c42e43abb927e426
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034802"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>Aggiunta di una vista origine dati per la previsione (Esercitazione intermedia sul data mining)
  In questa attività verrà aggiunta una vista origine dati da utilizzare per lo scenario di previsione. I modelli di previsione richiedono che i dati contengano una colonna che può essere utilizzata per identificare gli intervalli di una serie temporale. Se si prevede di analizzare più serie di dati, è necessario che tutte le serie terminino alla stessa data o intervallo temporale.  
  
### <a name="to-add-a-data-source-view"></a>Per aggiungere una vista origine dati  
  
1.  In Esplora soluzioni fare doppio clic su **viste origine dati**, quindi selezionare **nuova vista origine dati**.  
  
2.  Nella pagina iniziale di **Creazione guidata vista origine dati** fare clic su **Avanti**.  
  
3.  Nel **Vybrat Zdroj** nella pagina **origini dati relazionali**, selezionare il [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] zdroj dat. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  Se non hai questa origine dati, è possibile trovare i passaggi per creare l'origine dati nel [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
4.  Nel **selezione tabelle e viste** pagina, selezionare la tabella vTimeSeries (dbo) e quindi fare clic sulla freccia a destra per aggiungerla alla vista origine dati.  
  
5.  Scegliere **Avanti**.  
  
6.  Nel **Completamento procedura guidata** pagina, per impostazione predefinita la vista origine dati è denominata [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Modificare il nome in **SalesByRegion**, quindi fare clic su **fine**.  
  
     Verrà visualizzata la finestra di progettazione vista origine dati e il **SalesByRegion** vista origine dati viene visualizzata.  
  
## <a name="working-with-the-data-source-view"></a>Utilizzo della vista origine dati  
 Dopo aver creato la vista origine dati, è possibile esplorarne i dati nei modi seguenti:  
  
-   La tabella vTimeSeries nella finestra di progettazione e scegliere **Esplora dati** per aprire la tabella selezionata in una griglia.  
  
-   Fare clic su **opzioni di campionamento** e quindi utilizzare il **opzioni di esplorazione dati** finestra di dialogo per modificare il metodo di campionamento. Fare clic su **Aggiorna** per caricare i dati nella tabella utilizzando le nuove impostazioni delle opzioni. Ad esempio, è possibile specificare il numero di righe da restituire nel campione o scegliere le prime n righe.  
  
-   Fare clic sulla tabella vTimeSeries e selezionare **proprietà** per assegnare un nuovo nome alla tabella. È anche possibile selezionare singole colonne dalla vista origine dati e, successivamente, modificare le proprietà delle colonne.  
  
-   Fare clic in un punto qualsiasi dell'area di progettazione della vista origine dati per creare una nuova query e assegnarvi un nome, per creare relazioni tra tabelle o per modificare il layout dell'area di progettazione.  
  
-   Fare doppio clic su una tabella e selezionare **nuovo calcolo denominato** creare colonne derivate, incluse le aggregazioni. È inoltre possibile aggiungere nuove tabelle e viste dall'origine dati della vista corrente.  
  
 Nell'attività successiva verranno esplorati i dati della serie temporale e verrà determinata la colonna migliore da utilizzare come identificatore della serie temporale. Verrà anche descritto come gestire i gap nei dati della serie temporale.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Informazioni sui requisiti per una serie temporale del modello &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
