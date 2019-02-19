---
title: Visualizzare dati identici in una matrice e in un grafico (Generatore report) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1262f283-9fc2-4bc1-9c79-457f7642abc7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3d3e1eca43d386a11955eac7974baaf4a1d7282a
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292582"
---
# <a name="display-the-same-data-on-a-matrix-and-a-chart-report-builder"></a>Visualizzare dati identici in una matrice e in un grafico (Generatore report)
  Se si desidera visualizzare gli stessi dati in una matrice e in un grafico, è necessario impostare determinate proprietà su entrambe le aree dati per specificare lo stesso set di dati, nonché le stesse espressioni per filtri, gruppi, ordinamenti e dati.  
  
 Poiché entrambe le aree dati disporranno dello stesso predecessore per i dati (il set di dati del report), è possibile aggiungere alla matrice un pulsante di ordinamento interattivo che consente di modificare l'ordinamento sia per la matrice che per il grafico quando l'utente vi fa clic sopra. Per altre informazioni, vedere [Aggiungere un ordinamento interattivo a una tabella o a una matrice &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Per utilizzare i valori di gruppo delle colonne della matrice come legenda per il grafico, è necessario specificare i colori per i dati della serie sul grafico e quindi utilizzare gli stessi colori come colori di riempimento per lo sfondo delle caselle di testo nella cella della matrice in cui sono visualizzati i valori di gruppo. Per altre informazioni, vedere [Specifica di colori coerenti in più grafici con forme &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md).  
  
 In fase di esecuzione, il report potrebbe apparire poco chiaro se il numero dei valori di gruppo per le definizioni di gruppo è eccessivo. In questo caso, potrebbe essere necessario filtrare i valori, combinare i gruppi o regolare la soglia in modo che il grafico combini i gruppi automaticamente. Per altre informazioni, vedere [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-matrix-and-chart-to-display-the-same-data"></a>Per aggiungere una matrice e un grafico in cui visualizzare gli stessi dati  
  
1.  Aprire un report in visualizzazione Progettazione.  
  
2.  Nel gruppo **Aree dati** della scheda **Inserisci** fare clic su **Matrice**e quindi fare clic nel corpo del report o in un rettangolo nel corpo del report. Verrà aggiunta una matrice al report.  
  
3.  Nel gruppo **Aree dati** della scheda **Inserisci** fare clic su **Grafico**e quindi selezionare il tipo di grafico. Verrà aggiunto un grafico al report.  
  
4.  (Facoltativo) Nel gruppo **Elementi del report** della scheda **Inserisci** fare clic su **Rettangolo**e quindi sul report. Verrà aggiunto un rettangolo al report. Trascinare nel rettangolo la matrice e il grafico creati ai passaggi 2 e 3.  
  
     Mediante il posizionamento di più aree dati nel contenitore rettangolare, è possibile controllare la modalità di rendering della matrice e del grafico durante la visualizzazione del report.  
  
     Nei passaggi successivi si sceglierà lo stesso campo del set di dati da visualizzare nella matrice e nel grafico.  
  
5.  Dal riquadro dei dati del report trascinare un campo del set di dati numerici nella cella di dati della matrice.  
  
     Per impostazione predefinita, la funzione di aggregazione Sum viene usata per calcolare il valore di gruppo. Se si modifica la funzione di aggregazione nella matrice, è necessario modificarla anche nel grafico.  
  
6.  Nella matrice fare clic con il pulsante destro del mouse sulla cella contenente i dati, scegliere **Proprietà casella di testo**e quindi fare clic su **Numero**. Scegliere un formato adatto per il valore del campo del set di dati.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Trascinare lo stesso campo del set di dati scelto nel passaggio 3 nell'area **Valori** del grafico.  
  
9. Nel grafico fare clic con il pulsante destro del mouse sull'asse Y, scegliere **Proprietà asse**e quindi fare clic su **Numero**. Scegliere per i dati lo stesso formato selezionato nel passaggio 4.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nei passaggi successivi il gruppo di righe della matrice e il gruppo di serie del grafico verranno impostati sulla stessa espressione. Verrà inoltre impostato l'ordinamento per il gruppo di serie del grafico.  
  
11. Dal riquadro dei dati del report trascinare sul riquadro Gruppi di righe il campo del set di dati in base al quale si desidera eseguire il raggruppamento delle righe della matrice.  
  
     Per impostazione predefinita, il gruppo di righe della matrice aggiunge un'espressione di ordinamento che equivale all'espressione di raggruppamento.  
  
12. Trascinare lo stesso campo del set di dati usato nel passaggio 9 nell'area **Gruppi di serie** del grafico.  
  
13. Fare clic con il pulsante destro del mouse sul gruppo nell'area **Gruppi di serie** e quindi scegliere **Proprietà gruppo serie**.  
  
14. Fare clic su **Ordinamento**.  
  
15. Scegliere **Aggiungi**. Nella griglia delle espressioni di ordinamento verrà visualizzata una nuova riga.  
  
16. Nell'elenco a discesa **Ordina per**selezionare il campo del set di dati scelto nel passaggio 9 per il raggruppamento.  
  
17. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nei passaggi successivi il gruppo di colonne della matrice e il gruppo di categorie del grafico verranno impostati sulla stessa espressione. Verrà inoltre impostato l'ordinamento per il gruppo di categorie del grafico.  
  
18. Dal riquadro dei dati del report trascinare sul riquadro Gruppi di colonne il campo del set di dati in base al quale si desidera eseguire il raggruppamento delle colonne della matrice.  
  
     Per impostazione predefinita, il gruppo di colonne della matrice aggiunge un'espressione di ordinamento che equivale all'espressione di raggruppamento.  
  
19. Trascinare lo stesso campo del set di dati usato nel passaggio 16 nell'area **Gruppi di categorie** del grafico.  
  
20. Fare clic con il pulsante destro del mouse sul gruppo nell'area **Gruppi di categorie** e quindi scegliere **Proprietà gruppo categorie**.  
  
21. Fare clic su **Ordinamento**.  
  
22. Scegliere **Aggiungi**. Nella griglia delle espressioni di ordinamento verrà visualizzata una nuova riga.  
  
23. Nell'elenco a discesa **Ordina per**selezionare il campo del set di dati scelto nel passaggio 16 per il raggruppamento.  
  
24. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
25. Visualizzare il risultato nell'anteprima. Nei gruppi di righe e di colonne della matrice verranno visualizzati gli stessi dati dei gruppi di categorie e di serie del grafico.  
  
## <a name="see-also"></a>Vedere anche  
 [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
