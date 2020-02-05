---
title: Aggiunta di dati a un'area dati Tablix (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 847e3f6e7e76041749b0588bff510caebed11817
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581891"
---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>Aggiunta di dati a un'area dati Tablix (Generatore report e SSRS)
Nei report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , per visualizzare i dati di un set di dati del report in una tabella o una matrice, specificare in ogni cella dati il nome di un campo del set di dati da visualizzare. È possibile visualizzare dati dettaglio o dati raggruppati. Se si aggiungono gruppi a una tabella o una matrice, vengono automaticamente aggiunte le righe e le colonne per i valori e i dati di gruppo. È quindi possibile aggiungere subtotali e totali per i dati.  
  
 Tutti i dati di un'area dati appartengono almeno a un gruppo. I dati dettaglio appartengono al gruppo dettagli. Per altre informazioni sui dati dettaglio e i dati raggruppati, vedere [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>Aggiunta di dati dettaglio  
 Per dati dettaglio si intendono tutti i dati di un set di dati del report dopo l'applicazione dei filtri al set di dati, all'area dati e al gruppo dettagli. Tutti i dati dettaglio visualizzati in un'area dati Tablix devono provenire dallo stesso set di dati del report.  
  
 Per aggiungere dati dettaglio da un set di dati del report a un'area dati Tablix, trascinare un campo del set di dati dal riquadro dei dati del report in ogni cella della riga di dettaglio. Per le celle presenti in un'area dati Tablix è possibile aggiungere o modificare un'espressione del campo del set di dati tramite il selettore del campo in ogni cella o trascinando un campo dal riquadro dei dati del report nella cella. Per creare colonne aggiuntive, è possibile trascinare il campo dal riquadro dei dati del report e inserirlo in un'area dati Tablix esistente.  
  
 Per impostazione predefinita, in fase di esecuzione una cella della riga di dettaglio visualizza dati dettaglio mentre una cella di una riga di gruppo visualizza un valore di aggregazione. Per altre informazioni sulle righe e le colonne Tablix, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Un modello di tabella e un modello di elenco forniscono una riga di dettaglio. Un modello di matrice non contiene invece righe di questo tipo. Se l'area dati Tablix non presenta righe di dettagli, è possibile aggiungerne definendo un gruppo dettagli. Per altre informazioni, vedere [Aggiungere un gruppo dettagli &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="adding-grouped-data"></a>Aggiunta di dati raggruppati  
 Per dati raggruppati si intendono tutti i dati dettaglio specificati da un'espressione di raggruppamento dopo l'applicazione dei filtri al set di dati, all'area dati e al gruppo. Per organizzare i dati dettaglio in gruppi, trascinare i campi dal riquadro dei dati del report nel riquadro di raggruppamento. Quando si aggiunge un gruppo, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiunge automaticamente le righe e le colonne correlate all'area dati Tablix nella quale visualizzare i dati raggruppati. Le celle presenti in tali righe o colonne sono associate ai dati raggruppati. Per altre informazioni, vedere [Aggiunta o eliminazione di un gruppo in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Per impostazione predefinita, quando si aggiunge un campo del set di dati che rappresenta dati numerici a una cella di una riga o una colonna del gruppo, il valore della cella corrisponde alla somma dei dati raggruppati che hanno come ambito le appartenenze al gruppo di righe e colonne più interno della cella. È possibile impostare la funzione di aggregazione predefinita Sum su qualsiasi altra funzione di aggregazione, ad esempio Avg o Count. È inoltre possibile modificare l'ambito predefinito di un calcolo di aggregazione, ad esempio, per calcolare la percentuale con cui un valore contribuisce a un gruppo di righe. Per altre informazioni, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)sottostante.  
  
 Per impostazione predefinita, tutti i dati raggruppati provengono dallo stesso set di dati del report. In un'area dati Tablix è possibile includere valori di aggregazione provenienti da un altro set di dati specificando il nome del set di dati come ambito. È possibile specificare più valori di aggregazione provenienti da più set di dati all'interno di una sola area dati Tablix. Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="adding-subtotals-and-totals"></a>Aggiunta di subtotali e totali  
 Per aggiungere i subtotali di un gruppo e i totali complessivi dell'area dati, utilizzare la caratteristica Aggiungi totale del menu di scelta rapida in una cella o nel riquadro di raggruppamento. Verranno aggiunte automaticamente le righe e le colonne nelle quali visualizzare i totali. Per impostazione predefinita, nelle espressioni di totali e subtotali viene usata la funzione di aggregazione [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) . Dopo aver aggiunto l'espressione, è possibile modificare la funzione predefinita. Per altre informazioni, vedere [Aggiungere un totale a un gruppo o a un'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="adding-labels"></a>Aggiunta di etichette  
 Per aggiungere etichette per un gruppo o per l'area dati, aggiungere una riga o una colonna esternamente al gruppo da etichettare. Le righe e le colonne di etichette sono simili a quelle aggiunte per la visualizzazione dei totali. Per altre informazioni, vedere [Inserire o eliminare una riga &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md) o [Inserire o eliminare una colonna &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>Aggiunta di un'area dati Tablix esistente da un altro report  
 È possibile copiare un'area dati da un altro report e incollarla in un report nuovo o esistente. Dopo avere incollato l'area dati, è necessario verificare che venga definito il set di dati utilizzato dall'area dati e che i campi del set di dati abbiano gli stessi nomi e tipi di dati presenti nel report originale. I set di dati di un report non possono essere copiati in un altro report, ma se nei report vengono utilizzati origini dati condivise, il set di dati può essere duplicato rapidamente nell'altro report. Inoltre è possibile importare il testo della query per le query che recuperano i dati per il set di dati, rendendo così semplice la duplicazione delle query nei report. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [Aggiungere un'espressione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
