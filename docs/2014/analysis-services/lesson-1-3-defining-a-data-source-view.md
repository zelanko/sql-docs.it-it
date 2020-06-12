---
title: Definizione di una vista origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9b1810eb23a8d0d0541606cb69197b8030463748
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543653"
---
# <a name="defining-a-data-source-view"></a>Definizione di una vista origine dati
  Dopo aver definito le origini dati che si utilizzeranno in un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , il passaggio successivo consiste in genere nella definizione di una vista origine dati per il progetto. Una vista origine dati è una vista singola unificata dei metadati delle tabelle e delle viste specificate definite dall'origine dati nel progetto. L'archiviazione dei metadati nella vista origine dati consente di lavorare con i metadati durante lo sviluppo senza una connessione aperta con un'origine dati sottostante. Per altre informazioni, vedere [Viste origine dati in modelli multidimensionali](multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Nell'attività che segue si definirà una vista origine dati che include cinque tabelle dell'origine dati **AdventureWorksDW2012** .  
  
### <a name="to-define-a-new-data-source-view"></a>Per definire una nuova vista origine dati  
  
1.  In Esplora soluzioni (a destra della finestra di Microsoft Visual Studio) fare clic con il pulsante destro del mouse su **Viste origine dati**, quindi scegliere **Nuova vista origine dati**.  
  
2.  Nella pagina **Creazione guidata vista origine dati** fare clic su **Avanti**. Viene visualizzata la pagina **Selezione origine dati** .  
  
3.  In **Origine dati relazionali**è selezionata l'origine dati **Adventure Works DW 2012** . Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Per creare una vista origine dati basata su più origini dati, definire innanzitutto una vista origine dati basata su una singola origine dati che viene chiamata origine dati primaria. Successivamente, è possibile aggiungere tabelle e viste di un'origine dati secondaria. Quando si progettano dimensioni contenenti attributi basati su tabelle correlate in più origini dati, potrebbe essere necessario definire un'origine dati di [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] come origine dati primaria allo scopo di usare le funzionalità del motore delle query distribuite.  
  
4.  Nella pagina **Selezione tabelle e viste** selezionare le tabelle e le viste nell'elenco di oggetti disponibili nell'origine dati selezionata. Questo elenco può essere filtrato in modo da agevolare la selezione di tabelle e viste.  
  
    > [!NOTE]  
    >  Fare clic sul pulsante di ingrandimento nell'angolo superiore destro in modo da visualizzare la finestra a schermo intero. In questo modo risulterà più semplice visualizzare l'elenco completo di oggetti disponibili.  
  
     Nell'elenco **Oggetti disponibili** selezionare gli oggetti seguenti. Per selezionare più tabelle, fare clic su ognuna di esse tenendo premuto CTRL:  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  Fare clic su questo pulsante **>** per aggiungere le tabelle selezionate all'elenco **oggetti inclusi** .  
  
6.  Fare clic su **Avanti.**  
  
7.  Nel campo Nome assicurarsi che sia visualizzato **Adventure Works DW 2012** , quindi fare clic su **Fine**.  
  
     La vista origine dati **Adventure Works DW 2012** viene visualizzata nella cartella **Viste origine dati** in Esplora soluzioni. Il contenuto della vista origine dati verrà inoltre visualizzato in Progettazione vista origine dati in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Questa finestra di progettazione contiene i seguenti elementi:  
  
    -   Un riquadro **Diagramma** in cui sono rappresentate graficamente le tabelle e le relative relazioni.  
  
    -   Un riquadro **Tabelle** in cui le tabelle e i relativi elementi di schema sono visualizzati in una visualizzazione albero.  
  
    -   Un riquadro **Libreria diagrammi** in cui è possibile creare diagrammi secondari che consentono di visualizzare subset della vista origine dati.  
  
    -   Una barra degli strumenti specifica di Progettazione vista origine dati.  
  
8.  Per ingrandire l'ambiente di sviluppo di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , fare clic sul pulsante **Ingrandisci** .  
  
9. Per visualizzare le tabelle nel riquadro **Diagramma** al 50%, fare clic sull'icona **Zoom** sulla barra degli strumenti di Progettazione vista origine dati. In questo modo i dettagli delle colonne di ogni tabella verranno nascosti.  
  
10. Per nascondere Esplora soluzioni, fare clic sul pulsante **Nascondi automaticamente** , ovvero l'icona con la puntina sulla barra del titolo. Per visualizzare nuovamente Esplora soluzioni, posizionare il puntatore sulla scheda corrispondente sul lato destro dell'ambiente di sviluppo. Per scoprire Esplora soluzioni, fare di nuovo clic sul pulsante **Nascondi automaticamente** .  
  
11. Se le finestre non sono nascoste per impostazione predefinita, fare clic su **Nascondi automaticamente** sulla barra del titolo delle finestre Proprietà ed Esplora soluzioni.  
  
     A questo punto è possibile visualizzare tutte le tabelle e le relative relazioni nel riquadro **Diagramma** . Si noti che tra la tabella FactInternetSales e la tabella DimDate esistono tre relazioni. A ogni vendita sono associate tre date: data di ordine, di scadenza e di spedizione. Per visualizzare i dettagli di una relazione, fare doppio clic sulla relativa freccia nel riquadro **Diagramma** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica dei nomi predefiniti delle tabelle](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
