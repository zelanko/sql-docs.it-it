---
title: Filtro, raggruppamento e ordinamento di dati (Generatore report e SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0012f01fead8d6890f8e593f4991cbb0252e3dd6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65576522"
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>Filtro, raggruppamento e ordinamento di dati (Generatore report e SSRS)
  In un report le espressioni vengono usate per facilitare il controllo, l'organizzazione e l'ordinamento di dati del report. Per impostazione predefinita, mentre si creano set di dati e si progetta il layout del report, le proprietà degli elementi del report vengono impostate automaticamente su espressioni basate su campi del set di dati, parametri e altri elementi visualizzati nel riquadro dei dati del report. È inoltre possibile aggiungere un pulsante di ordinamento interattivo a una tabella o una cella della matrice, in modo da consentire a un utente di modificare in modo interattivo l'ordinamento della riga per gruppi o righe all'interno di gruppi.  
  
-   **Espressioni di filtro** Un'espressione di filtro consente di verificare l'inclusione o l'esclusione di dati in base a un confronto specificato dall'utente. I filtri vengono applicati ai dati in un report dopo essere stati recuperati da una connessione dati. È possibile aggiungere qualsiasi combinazione di filtri agli elementi seguenti: una definizione del set di dati condiviso nel server di report, un'istanza del set di dati condiviso o un set di dati incorporato in un report, un'area dati quale una tabella o un grafico oppure un gruppo di aree dati quale un gruppo di righe in una tabella o un gruppo di categorie in un grafico.  
  
-   **Espressioni di raggruppamento** Un'espressione di raggruppamento consente di organizzare dati in base a un campo del set di dati o un altro valore. Le espressioni di raggruppamento vengono create automaticamente mentre si compila il layout del report. L'elaboratore di report valuta le espressioni di raggruppamento dopo l'applicazione dei filtri ai dati e mentre vengono combinati i dati del report e le aree dati. È possibile personalizzare un'espressione di raggruppamento dopo che è stata creata.  
  
-   **Espressioni di ordinamento** Un'espressione di ordinamento consente di controllare l'ordine in cui i dati vengono visualizzati in un'area dati. Le espressioni di ordinamento vengono create automaticamente mentre si compila il layout del report. Per impostazione predefinita, un'espressione di ordinamento per un gruppo viene impostata sullo stesso valore dell'espressione di raggruppamento. È possibile personalizzare un'espressione di ordinamento dopo che è stata creata.  
  
-   **Ordinamento interattivo** Per consentire a un utente di ordinare o invertire l'ordinamento di una colonna, è possibile aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna o una cella di intestazione del gruppo in una tabella o una matrice.  
  
 Per consentire agli utenti di personalizzare le espressioni di filtro, raggruppamento o ordinamento, è possibile modificare un'espressione in modo che venga aggiunto un riferimento a un parametro del report. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Per ulteriori informazioni ed esempi, vedere gli argomenti seguenti:  
  
-   [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Esercitazioni di Generatore report](../../reporting-services/report-builder-tutorials.md)  
  
-   [Esercitazioni su Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [Esempi di report (Generatore report e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> Filtro di dati nel report  
 I filtri sono parti di un report che consentono di controllare i dati del report dopo che sono stati recuperati dalla connessione dati. Usare filtri quando non è possibile modificare una query del set di dati per filtrare i dati prima che vengano recuperati da un'origine dati esterna.  
  
 Quando è possibile, compilare query del set di dati che restituiscono solo i dati che è necessario visualizzare nel report. Riducendo la quantità di dati da recuperare ed elaborare, si migliorano le prestazioni del report. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Dopo avere recuperato i dati dall'origine dati esterna, è possibile aggiungere filtri a set di dati, aree dati e gruppi di aree dati, inclusi gruppi di dettagli. In fase di esecuzione, i filtri vengono applicati prima al set di dati, poi all'area dati e infine al gruppo procedendo dall'alto verso il basso per le gerarchie di gruppi. In una tabella, una matrice o un elenco i filtri per gruppi di righe, gruppi di colonne e gruppi adiacenti vengono applicati in modo indipendente. Anche in un grafico i filtri per gruppi di categorie e gruppi di serie vengono applicati in modo indipendente. Per altre informazioni, vedere [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Specificare un' *equazione di filtro*per ogni filtro. Un'equazione di filtro include un campo del set di dati o un'espressione che specifica i dati da filtrare, un operatore e un valore da confrontare. Quando l'elemento viene elaborato, vengono inclusi solo i valori dei dati che corrispondono alla condizione di filtro.  
  
 Per consentire agli utenti di controllare i dati in un report, è possibile includere parametri nelle espressioni di filtro. Per altre informazioni, vedere [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).  
  
 Per personalizzare una vista per ogni utente, è possibile includere un riferimento al campo predefinito UserID in un filtro. Per altre informazioni, vedere [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
  
##  <a name="Grouping"></a> Raggruppamento di dati nel report  
 I gruppi consentono di organizzare dati in un report per visualizzare o calcolare valori di aggregazione. La comprensione delle modalità di definizione dei gruppi e di utilizzo delle caratteristiche di gruppo consente di progettare report più concisi.  
  
 Le espressioni di raggruppamento vengono create automaticamente quando si effettuano le operazioni seguenti:  
  
-   Disporre campi del set di dati in una Creazione guidata tabella, matrice o grafico o campi di corrispondenza nella Creazione guidata mappa.  
  
-   In una tabella, una matrice o un elenco aggiungere un campo all'area Gruppi di righe o Gruppi di colonne nel riquadro di raggruppamento.  
  
-   In un grafico aggiungere un campo a Gruppi di categorie o Gruppi di serie nel riquadro Dati grafico.  
  
-   In una mappa specificare un campo per la corrispondenza degli elementi della mappa con i dati analitici nell'elemento del menu di scelta rapida Dati livello.  
  
 Un gruppo è una parte della definizione del report. Ogni gruppo ha un nome. Per impostazione predefinita, il nome del gruppo corrisponde al campo del set di dati sul quale è basato.  
  
 In un'area dati tabella o matrice è possibile creare più gruppi di righe e di colonne. È possibile visualizzare i dati in una gerarchia visiva organizzando gruppi nidificati, gruppi adiacenti e gruppi di gerarchie ricorsivi, ad esempio un organigramma.  
  
 Il nome del gruppo identifica l'ambito di un'espressione. È possibile specificare il nome di un gruppo come un ambito nel quale calcolare aggregazioni, organizzare gerarchicamente dati e attivare o disattivare la visualizzazione di nodi figlio da nodi padre in un report drill-down, visualizzare viste diverse degli stessi dati in più aree dati e visualizzare dati riepilogativi in una tabella, una matrice, un grafico, un misuratore o una mappa. Per altre informazioni, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)sottostante.  
  
 Per raggruppare diversi campi del set di dati, aggiungere ogni campo al set di espressioni di raggruppamento. È anche possibile scrivere espressioni di raggruppamento personalizzate in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. È possibile ad esempio eseguire il raggruppamento in base a un intervallo di valori oppure usando un parametro del report per consentire all'utente di selezionare la modalità di raggruppamento dei dati in un'area dati. Per altre informazioni, vedere [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 Per la presentazione del report è possibile aggiungere interruzioni di pagina prima e dopo ogni gruppo o istanza di un gruppo, in modo da ridurre la quantità di dati presenti in ogni pagina e gestire le prestazioni di rendering del report. Per altre informazioni, vedere [Aggiungere un'interruzione di pagina &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md).  
  
 La creazione di gruppi di aree dati è un modo utile per organizzare dati in un report. Sono disponibili diversi altri modi per organizzare dati, ognuno con vantaggi specifici. Per altre informazioni, vedere [Drill-through, drill-down, sottoreport e aree dati nidificate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
### <a name="defining-group-variables"></a>Definizione delle variabili di gruppo  
 Quando si definisce un gruppo, è possibile creare una variabile di gruppo da usare nelle espressioni che hanno come ambito il gruppo e sono accessibili dai gruppi nidificati. Una variabile di gruppo viene calcolata una volta per istanza di gruppo ed è possibile accedervi da espressioni in gruppo figlio. Ad esempio, per dati raggruppati per area e area secondaria, è possibile calcolare una tassa per ogni area e usare tale tassa nei calcoli dal gruppo di aree secondarie.  
  
 Per altre informazioni, vedere [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
### <a name="groups-and-scope-in-data-regions"></a>Gruppi e ambito in aree dati  
 Per fornire più viste dei dati dallo stesso set di dati, è possibile specificare le stesse espressioni di raggruppamento per ogni area dati. È ad esempio possibile visualizzare dati suddivisi in categorie in una tabella per mostrare tutti i dati di dettaglio sotto forma di grafico a torta, in modo da visualizzare le aggregazioni e ogni categoria in relazione all'intero set di dati. Per altre informazioni, vedere [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
 Quando si nidifica un'area dati in una cella di una tabella, una matrice o un elenco, viene definito automaticamente l'ambito dei dati nelle appartenenze ai gruppi più interni della cella. Si supponga, ad esempio, di aggiungere un grafico a una cella presente sia in un gruppo di righe che in un gruppo di colonne. In fase di esecuzione i dati disponibili per il grafico avranno come ambito l'istanza del gruppo di righe più interno e l'istanza del gruppo di colonne più interno. Per altre informazioni, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)sottostante.  
  
  
##  <a name="Sorting"></a> Ordinamento di dati nel report  
 Per controllare l'ordinamento di dati nel report, è possibile ordinarli in una query del set di dati o definire un'espressione di ordinamento per un'area o un gruppo di dati. È inoltre possibile aggiungere pulsanti di ordinamento interattivi a tabelle e matrici per consentire agli utenti di modificare l'ordinamento per le righe.  
  
 Tutti e tre i tipi di ordinamento possono essere combinati nello stesso report. Per impostazione predefinita, l'ordinamento è determinato dall'ordine in cui i dati vengono restituiti dalla query del set di dati. Le espressioni di ordinamento vengono applicate nell'area dati e nel gruppo di aree dati. Gli ordinamenti interattivi vengono applicati dopo le espressioni di ordinamento.  
  
 Per le espressioni contenenti funzioni di aggregazione, la maggior parte dei risultati non è interessata dall'ordinamento. I valori restituiti per le funzioni di aggregazione seguenti sono interessati dall'ordinamento: First, Last e Previous. Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
### <a name="sorting-data-in-a-dataset-query"></a>Ordinamento dei dati di una query del set di dati  
 Includere l'ordinamento nella query del set di dati per eseguire un preordinamento dei dati prima che vengano recuperati per un report. Quando si ordinano i dati nella query, l'operazione di ordinamento viene eseguita dall'origine dati anziché dal componente Elaborazione report.  
  
 Per un tipo di origine dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile aggiungere una clausola ORDER BY alla query del set di dati. La query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente, ad esempio, di disporre in ordine decrescente le colonne Sales e Region della tabella SalesOrders in base alle vendite: `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`.  
  
> [!NOTE]  
>  Non tutte le origini dati consentono di specificare l'ordinamento nella query.  
  
### <a name="sorting-data-with-sort-expressions"></a>Ordinamento dei dati mediante le espressioni di ordinamento  
 Per ordinare i dati nel report dopo averli recuperati dall'origine dati, è possibile impostare espressioni di ordinamento in un'area dati o in un gruppo Tablix, incluso il gruppo dettagli. Nell'elenco seguente viene descritto l'effetto dell'impostazione delle espressioni di ordinamento sugli elementi del report:  
  
-   **Area dati Tablix.** Impostare espressioni di ordinamento in un'area dati tabella, matrice o elenco per controllare l'ordinamento dei dati nell'area dati, dopo aver applicato i filtri del set di dati e dell'area dati in fase di esecuzione.  
  
-   **Gruppo dell'area dati Tablix.** Impostare espressioni di ordinamento per ogni gruppo, incluso il gruppo dettagli, per controllare l'ordinamento delle istanze di gruppo. Per il gruppo dettagli, ad esempio, si controlla l'ordine delle righe di dettaglio. Per un gruppo figlio, si controlla l'ordine delle istanze di gruppo per il gruppo figlio all'interno del gruppo padre. Per impostazione predefinita, quando si crea un gruppo, l'espressione di ordinamento viene impostata sull'espressione di raggruppamento e sull'ordinamento crescente.  
  
     Se si dispone di un solo gruppo dettagli, è possibile definire un'espressione di ordinamento nella query, sull'area dati o sul gruppo dettagli e ottenere lo stesso risultato.  
  
-   **Area dati del grafico.** Impostare un'espressione di ordinamento per i gruppi di categorie e di serie in modo da controllare l'ordinamento dei punti dati. Per impostazione predefinita, l'ordine dei punti dati è anche l'ordine dei colori nella legenda del grafico. Per altre informazioni, vedere [Formattazione dei colori delle serie in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   **Elemento di report mappa.** Non è in genere necessario ordinare dati per un'area dati della mappa, perché nella mappa vengono raggruppati dati da visualizzare negli elementi della mappa.  
  
-   **Area dati del misuratore.** In genere non è necessario ordinare i dati per un'area dati del misuratore in quanto nel misuratore viene visualizzato un solo valore relativo a un intervallo. Se non si devono ordinare i dati in un misuratore, è innanzitutto necessario definire un gruppo e quindi impostare un'espressione di ordinamento per il gruppo.  
  
#### <a name="sorting-by-a-different-value"></a>Ordinamento in base a un valore diverso  
 È opportuno ordinare le righe in un'area dati in base a un valore diverso dal valore del campo. Si supponga ad esempio che il campo Size contenga valori di testo che corrispondono a piccolo, medio, grande e molto grande. Per impostazione predefinita, anche l'espressione di ordinamento per un gruppo di righe basato su Size è [Size]. Per avere maggiore controllo sulla modalità di ordinamento dei dati, è possibile aggiungere un campo alla query del set di dati che definisca l'ordinamento desiderato.  
  
 In alternativa è possibile definire un set di dati in cui siano inclusi solo le dimensioni e un valore che specifica l'ordinamento desiderato. È possibile modificare l'espressione di ordinamento in modo che utilizzi la funzione Ricerca per il valore di ordinamento.  
  
 Si supponga ad esempio che la query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente definisca un set di dati denominato Sizes. La query utilizza un'istruzione CASE per definire un valore di ordinamento SizeSortOrder per ogni valore Size:  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 In una tabella che dispone di un gruppo di righe basato su `[Size]`, è possibile modificare l'espressione di ordinamento del gruppo in modo che venga usata una funzione Ricerca per trovare il campo numerico che corrisponde al valore della dimensione. L'espressione sarà simile alla seguente:  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 Per altre informazioni, vedere [Ordinare i dati in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md) e [Funzione Lookup &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md).  
  
###  <a name="Interactive"></a> Aggiunta di ordinamento interattivo per l'utente  
 Per consentire a un utente di modificare l'ordinamento dei dati del report in una tabella o una matrice, è possibile aggiungere pulsanti di ordinamento interattivi a intestazioni di colonna o di gruppo. Gli utenti possono fare clic sul pulsante per attivare o disattivare l'ordinamento. L'ordinamento interattivo è disponibile solo nei formati di rendering che consentono l'interazione dell'utente, ad esempio HTML.  
  
 È possibile aggiungere pulsanti di ordinamento interattivo a una casella di testo in una cella dell'area dati Tablix. Per impostazione predefinita, in ogni cella è contenuta una casella di testo. Nelle proprietà della casella di testo si specifica la parte di un'area dati di tabella o matrice da ordinare (i valori di un gruppo padre, i valori di un gruppo figlio o le righe di dettaglio), l'elemento in base al quale eseguire l'ordinamento e se applicare l'espressione di ordinamento agli altri elementi del report con una relazione di tipo peer. Se, ad esempio, una tabella e un grafico che forniscono viste sullo stesso set di dati sono contenuti in un rettangolo, avranno aree dati peer. Quando un utente attiva l'ordinamento nella tabella, viene attivato anche l'ordinamento del grafico. Per altre informazioni, vedere [Ordinamento interattivo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
  
##  <a name="HowTo"></a> Procedure  
 [Visualizzazione delle intestazioni durante lo scorrimento di un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [Visualizzare intestazioni e piè di pagina con un gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Aggiungere un ordinamento interattivo a una tabella o a una matrice &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [Impostare una proprietà NoDataMessage per un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Creare un gruppo di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [Aggiunta o eliminazione di un gruppo in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [Visualizzare intestazioni e piè di pagina con un gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Aggiungere o eliminare un gruppo in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [Aggiungere un totale a un gruppo o a un'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> Contenuto della sezione  
 [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> Sezioni correlate  
 [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [Visualizzazione di una serie con più intervalli di dati in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Mappe &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [Indicatori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
