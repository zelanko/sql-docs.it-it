---
title: Ordinare i dati in un'area dati (Generatore report) | Microsoft Docs
description: Informazioni su come modificare l'ordinamento dei dati in un'area dati quando un report viene eseguito per la prima volta in Generatore report.
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fecda4c838a5317bf87b50834152a3bb65f1d41b
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462205"
---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>Ordinamento dei dati in un'area dati (Generatore report e SSRS)
  Per modificare l'ordinamento dei dati in un'area dati quando si esegue un report per la prima volta, è necessario impostare l'espressione di ordinamento nel gruppo o nell'area dati. Per impostazione predefinita, l'espressione di ordinamento per un gruppo viene impostata automaticamente su un valore identico a quello dell'espressione di raggruppamento.  
  
-   In un'area dati Tablix impostare l'espressione di ordinamento per l'area dati o per ogni gruppo, incluso il gruppo di dettagli. Se in un'area dati Tablix è disponibile un solo gruppo di dettagli, è possibile definire un'espressione di ordinamento nella query, nell'area dati o nel gruppo di dettagli e ottenere lo stesso risultato.  
  
-   In un'area dati del grafico impostare l'espressione di ordinamento per i gruppi Categoria e Serie in modo da controllare l'ordinamento per ogni gruppo. L'ordine dei colori in una legenda del grafico viene determinato dall'espressione di ordinamento per i punti dati nel gruppo Categoria.  
  
-   In un'area dati del misuratore in genere non è necessario ordinare i dati, in quanto nel misuratore viene visualizzato un solo valore relativo a un intervallo. Se è necessario ordinare i dati in un misuratore, definire innanzitutto un gruppo e quindi impostare l'espressione di ordinamento per il gruppo.  
  
 Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Per un'area dati Tablix è inoltre possibile aggiungere un pulsante di ordinamento interattivo nella parte superiore di un'intestazione di colonna, in modo da consentire all'utente di modificare l'ordinamento di gruppi o righe di dettagli. Per altre informazioni, vedere [Ordinamento interattivo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>Per ordinare i dati in un'area dati Tablix  
  
1.  Nell'area di progettazione fare clic con il pulsante destro del mouse sull'handle di riga, quindi scegliere **Proprietà Tablix**.  
  
2.  Fare clic su **Ordinamento**.  
  
3.  Per ogni espressione di ordinamento, attenersi alla procedura seguente:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Digitare o selezionare un'espressione in base alla quale ordinare i dati.  
  
    3.  Nell'elenco a discesa della colonna **Ordine** scegliere la direzione di ordinamento per ogni espressione. L'opzione**A-Z** consente di disporre l'espressione in ordine crescente. L'opzione**Z-A** consente di disporre l'espressione in ordine decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>Per ordinare i valori di un gruppo, incluso il gruppo di dettagli, per una Tablix  
  
1.  Nell'area di progettazione fare clic nell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento vengono visualizzati i gruppi di righe e di colonne per l'area dati Tablix.  
  
2.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul nome del gruppo, quindi scegliere **Modifica gruppo**.  
  
3.  Nella finestra di dialogo **Gruppo Tablix** fare clic su **Ordina**.  
  
4.  Per ogni espressione di ordinamento, attenersi alla procedura seguente:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Digitare o selezionare un'espressione in base alla quale ordinare i dati.  
  
    3.  Nell'elenco a discesa della colonna **Ordine** scegliere la direzione di ordinamento per ogni espressione. L'opzione**A-Z** consente di disporre l'espressione in ordine crescente. L'opzione**Z-A** consente di disporre l'espressione in ordine decrescente.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>Per ordinare le etichette dell'asse X in ordine alfabetico su un grafico  
  
1.  Fare clic con il pulsante destro del mouse su un campo nell'area di rilascio dei campi categoria e scegliere **Proprietà gruppo categorie**.  
  
2.  Nella finestra di dialogo **Proprietà gruppo categorie** fare clic su **Ordinamento**.  
  
3.  Per ogni espressione di ordinamento, attenersi alla procedura seguente:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Selezionare l'espressione che corrisponde al campo di raggruppamento. È possibile verificare l'espressione per il campo di raggruppamento facendo clic su **Raggruppamento**.  
  
    3.  Nell'elenco a discesa della colonna **Ordine** scegliere la direzione di ordinamento per ogni espressione. L'opzione**A-Z** consente di disporre l'espressione in ordine alfabetico crescente. L'opzione**Z-A** consente di disporre l'espressione in ordine alfabetico decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>Per disporre i punti dati in ordine crescente o decrescente su un grafico  
  
1.  Fare clic con il pulsante destro del mouse su un campo nell'area di rilascio dei campi categoria e scegliere **Proprietà gruppo categorie**.  
  
2.  Nella finestra di dialogo **Proprietà gruppo categorie** fare clic su **Ordinamento**.  
  
3.  Per ogni espressione di ordinamento, attenersi alla procedura seguente:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Selezionare l'espressione che corrisponde al campo dati. Nella maggior parte dei casi si tratta di un valore aggregato, ad esempio `=Sum(Fields!Quantity.Value)`.  
  
    3.  Nell'elenco a discesa della colonna **Ordine** scegliere la direzione di ordinamento per ogni espressione. L'opzione**A-Z** consente di disporre l'espressione in ordine crescente. L'opzione**Z-A** consente di disporre l'espressione in ordine decrescente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>Per disporre i dati in ordine crescente o decrescente per la visualizzazione su un misuratore  
  
1.  Fare clic con il pulsante destro del mouse sul misuratore e scegliere **Aggiungi gruppo di dati**.  
  
2.  Nella finestra di dialogo **Proprietà gruppo di pannelli del misuratore** fare clic su **Generale** , se necessario.  
  
3.  In **Espressioni di raggruppamento**fare clic su **Aggiungi**.  
  
4.  Da **Raggruppa in base a**digitare o selezionare un'espressione in base alla quale raggruppare i dati.  
  
5.  Ripetere i passaggi da 3 a 4 finché non saranno state aggiunte tutte le espressioni di raggruppamento desiderate.  
  
6.  Fare clic su **Ordinamento**.  
  
7.  Per ogni espressione di ordinamento, attenersi alla procedura seguente:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Selezionare l'espressione che corrisponde al campo di raggruppamento. È possibile verificare l'espressione per il campo di raggruppamento facendo clic su **Raggruppamento**.  
  
    3.  Nell'elenco a discesa della colonna **Ordine** scegliere la direzione di ordinamento per ogni espressione. L'opzione**A-Z** consente di disporre l'espressione in ordine crescente. L'opzione**Z-A** consente di disporre l'espressione in ordine decrescente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Per altre informazioni sul raggruppamento dei dati in un misuratore, vedere [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Specificare i colori coerenti in più grafici con forme &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  
