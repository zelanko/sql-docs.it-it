---
title: Controllare la visualizzazione dell'area dati Tablix in una pagina del Report (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f81c48cc-f038-4f57-988d-e9a3cbb46424
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6fd4b09947bc10a9e4e960ca1097f807a47c14f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106205"
---
# <a name="controlling-the-tablix-data-region-display-on-a-report-page-report-builder-and-ssrs"></a>Controllo della visualizzazione dell'area dati Tablix in una pagina del report (Generatore report e SSRS)
  In questo argomento vengono descritte le proprietà di un'area dati Tablix che è possibile modificare per cambiare l'aspetto di tale area quando visualizzata in un report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="controlling-the-appearance-of-data"></a>Controllo dell'aspetto dei dati  
 Le caratteristiche seguenti consentono di controllare l'aspetto di un'area dati Tablix:  
  
-   **Formattazione dei dati.** Per formattare i dati in una tabella, una matrice o un elenco, impostare le proprietà relative al formato della casella di testo nella cella. È possibile impostare contemporaneamente proprietà per più celle. Per formattare i dati in un grafico, impostare le proprietà di formattazione sulla serie. Per altre informazioni, vedere [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md) e [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md).  
  
-   **Scrittura di espressioni**. Per altre informazioni, vedere [Uso delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) ed [Esempi di espressione &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
-   **Controllo dell'ordinamento**. Per controllare l'ordinamento, è necessario definire espressioni di ordinamento nell'area dati. Per controllare l'ordinamento di righe e colonne associate a un gruppo, è necessario definire espressioni di ordinamento nel gruppo includendo i gruppi di dettagli. È possibile aggiungere anche pulsanti di ordinamento interattivi per consentire all'utente di ordinare un'area dati Tablix o i rispettivi gruppi. Per altre informazioni, vedere [Ordinare i dati in un'area dati &#40;Generatore report e SSRS& #41;](sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Visualizzazione di un messaggio quando non sono presenti dati**. Quando per un set di dati del report non esistono dati in fase di esecuzione, è possibile scrivere un messaggio personalizzato da visualizzare in sostituzione dell'area dati. Per altre informazioni, vedere [Impostazione di una proprietà NoDataMessage per un'area dati &#40;Generatore report e SSRS&#41;](../report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md).  
  
-   **Nascondere i dati in modo condizionale**. Per controllare in modo condizionale se mostrare o nascondere parti di un'area dati o un'area dati, è possibile impostare la proprietà Hidden `True` o su un'espressione. Le espressioni possono includere riferimenti ai parametri di report. È inoltre possibile specificare un elemento Toggle in modo da consentire all'utente di visualizzare i dati di dettaglio. Per altre informazioni, vedere [Azione di drill-down &#40;Generatore report e SSRS&#41;](drilldown-action-report-builder-and-ssrs.md).  
  
-   **Unione di celle.** È possibile combinare più celle contigue di una tabella in un'unica cella. Questa operazione viene denominata estensione su più colonne o unione di celle. Le celle possono essere combinate solo orizzontalmente o verticalmente. Quando si uniscono le celle, vengono mantenuti soltanto i dati della prima cella, mentre i dati delle altre celle vengono rimossi. Le celle unite possono essere nuovamente suddivise nelle colonne originali. Per altre informazioni, vedere [Unire le celle in un'area dati &#40;Generatore report e SSRS& #41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="controlling-tablix-data-region-position-and-expansion-on-a-page"></a>Controllo dell'espansione e della posizione dell'area dati Tablix in una pagina  
 Le caratteristiche seguenti consentono di controllare la modalità di visualizzazione di un'area dati Tablix in un report visualizzabile:  
  
-   **Controllo della posizione di un'area dati Tablix in relazione agli altri elementi del report**. Un'area dati Tablix può essere posizionata al di sopra, accanto o al di sotto degli altri elementi del report nell'area di progettazione del report. In fase di esecuzione l'area dati Tablix viene espansa da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per essere adattata ai dati recuperati per il set di dati collegato e gli elementi del report di pari livello vengono spostati in base alle necessità. Per ancorare una Tablix accanto a un altro elemento del report, è necessario rendere di pari livello gli elementi del report e regolarne le posizioni relative. Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
-   **Modifica della direzione dell'espansione**. Per controllare se un'area dati Tablix si espande sulla pagina da sinistra a destra o da destra a sinistra, usare la proprietà Direction disponibile nella finestra Proprietà. Per altre informazioni, vedere [Rendering delle aree dati &#40;Generatore report e SSRS&#41;](rendering-data-regions-report-builder-and-ssrs.md).  
  
## <a name="controlling-how-a-tablix-data-region-renders-on-a-page"></a>Controllo della visualizzazione di un'area dati Tablix in una pagina  
 Nell'elenco seguente vengono descritte le modalità che è possibile usare per controllare come un'area dati Tablix viene visualizzata in un report:  
  
-   **Controllo della paginazione**. Per controllare la quantità di dati visualizzata in ogni pagina del report, è possibile impostare interruzioni di pagina nelle aree dati. È inoltre possibile impostare interruzioni di pagina nei gruppi. Le interruzioni di pagina possono influire sulle prestazioni del rendering su richiesta riducendo la quantità di dati da elaborare in ogni pagina. Per altre informazioni, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md) e [Aggiungere un'interruzione di pagina &#40;Generatore report e SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md).  
  
-   **Visualizzazione di dati su entrambi i lati delle intestazioni di riga**. Non è obbligatorio visualizzare le intestazioni di riga di fianco a un'area dati Tablix. È possibile spostare le intestazioni di riga tra le colonne e visualizzare le colonne di dati prima delle intestazioni di riga. A tale scopo, modificare la proprietà GroupsBeforeRowHeaders per la matrice. È possibile accedere a questa proprietà nella finestra Proprietà. Il valore per questa proprietà è un numero intero. Un valore pari a 2, ad esempio, consentirà di visualizzare due istanze di gruppo dei dati di colonna dell'area dati prima di visualizzare la colonna contenente le intestazioni di riga.  
  
## <a name="controlling-how-tablix-row-and-column-groups-render"></a>Controllo della visualizzazione di gruppi di colonne e righe Tablix  
 Per controllare come vengono visualizzati i gruppi di aree dati Tablix occorre considerare la struttura di gruppo. Un'area dati Tablix può disporre di quattro aree, come mostrato nella figura seguente:  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 L'area del gruppo di righe e l'area del gruppo di colonne contengono intestazioni di gruppo. Quando per un'area dati Tablix sono previste intestazioni di gruppo, è possibile controllare come le righe e le colonne vengono ripetute impostando proprietà nella pagina **Generale** della finestra di dialogo **Proprietà Tablix** .  
  
 Se in un'area dati Tablix è presente solo un'area del corpo della Tablix, non sono disponibili intestazioni di gruppo. Sono disponibili solo membri Tablix statici e dinamici. Un membro statico viene visualizzato una volta in relazione a un gruppo di righe o di colonne Tablix. Un membro dinamico si ripete una volta per ogni valore di gruppo univoco. Ad esempio, in un'area dati Tablix che visualizza un ordine di vendita, è possibile visualizzare i nomi della colonna nell'ordine di vendita in un membro della riga statico. Ogni riga nell'ordine di vendita viene visualizzata in un membro della riga dinamico.  
  
 È possibile controllare come viene visualizzato un membro Tablix impostando le proprietà nel riquadro Proprietà. Per altre informazioni, vedere "Modalità avanzata" in [Riquadro di raggruppamento &#40;Generatore report&#41;](grouping-pane-report-builder.md).  
  
 Nell'elenco seguente vengono descritte le modalità che è possibile usare per controllare come un'area dati Tablix viene visualizzata in un report:  
  
-   **Ripetizione di intestazioni di riga e colonna su più pagine**. È possibile visualizzare intestazioni di riga e colonna in ogni pagina su cui si estende un'area dati Tablix. Per altre informazioni, vedere [Visualizzazione delle intestazioni di riga e colonna in più pagine &#40;Generatore report e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
-   **Visualizzazione delle intestazioni di riga e di colonna durante lo scorrimento**. È possibile controllare se visualizzare le intestazioni delle righe e delle colonne quando si scorre un report usando un browser. Per altre informazioni, vedere [Visualizzazione delle intestazioni durante lo scorrimento di un report &#40;Generatore report e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md).  
  
 Per altre informazioni sull'impatto dell'esportazione di un report in formati diversi sulla modalità di visualizzazione di un'area dati Tablix in una pagina, vedere [Tipi di rendering &#40;Generatore report e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Controllo di interruzioni di pagina, intestazioni, colonne e righe &#40;Generatore report e SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
