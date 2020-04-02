---
title: Visualizzazione di progettazione report (Generatore report) | Microsoft Docs
description: Questo articolo descrive i controlli della finestra Generatore report usati per aggiungere, selezionare e organizzare le risorse del report e modificare le proprietà degli elementi del report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca82e7fa0a302c4156c56c2e5ff66ad0cc49da99
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290860"
---
# <a name="report-design-view-report-builder"></a>Visualizzazione di progettazione report (Generatore report)
  La finestra Generatore report è progettata per semplificare l'organizzazione delle risorse del report e per consentire una più rapida compilazione dei report impaginati necessari. L'area di progettazione si trova al centro della finestra ed è circondata dalla barra multifunzione e dai riquadri. Nell'area di progettazione vengono aggiunti e organizzati gli elementi del report. Questo articolo illustra i riquadri che consentono di aggiungere, selezionare e organizzare le risorse del report, nonché di modificare le proprietà degli elementi del report.  
  
 ![Visualizzazione Progettazione di Generatore report](../../reporting-services/report-builder/media/ssrb-designview.png "Visualizzazione Progettazione di Generatore report")  
  
1.  Barra multifunzione  
  
2.  [Riquadro Parametri](#Ribbon)  
  
3.  [Raccolta parti del report](#ReptPartGallery)  
  
4.  [riquadro Proprietà](#PropertiesPane)  
  
5.  [Area di progettazione del report](#RptDesignSurface)  
  
6.  [Riquadro Dati report](#ReptDataPane)  
  
7.  [Riquadro di raggruppamento](#GroupPane)  
  
8.  Barra di stato del report corrente  
  
##  <a name="parameters-pane"></a><a name="Ribbon"></a> Riquadro Parametri  
 I parametri del report consentono di controllare i dati del report, connettere report correlati e variare la presentazione del report. Il riquadro Parametri offre un layout flessibile per i parametri del report.  
  
 Per altre informazioni, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="the-report-design-surface"></a><a name="RptDesignSurface"></a> Area di progettazione del report  
 L'area di progettazione del report di Generatore report è l'area di lavoro principale per la progettazione dei report. Per inserire nel report elementi quali aree dati, sottoreport, caselle di testo, immagini, rettangoli e righe, è necessario aggiungerli dalla barra multifunzione o dalla Raccolta parti del report all'area di progettazione. dove è possibile aggiungere gruppi, espressioni, parametri, filtri, azioni, visibilità e formattazione agli elementi del report.  
  
 È inoltre possibile modificare gli elementi seguenti:  
  
-   Le proprietà del corpo del report, ad esempio il bordo e il colore di riempimento, facendo clic con il pulsante destro del mouse sull'area bianca dell'area di progettazione libera da qualsiasi elemento del report e scegliendo **Proprietà corpo**.  
  
-   Le proprietà intestazione e piè di pagina, ad esempio il bordo e il colore di riempimento, facendo clic con il pulsante destro del mouse sull'area bianca dell'area di progettazione nell'area dell'intestazione e piè di pagina libera da qualsiasi elemento del report e scegliendo **Proprietà intestazione** o **Proprietà piè di pagina**.  
  
-   Le proprietà del report stesso, ad esempio l'impostazione della pagina, facendo clic con il pulsante destro del mouse sull'area grigia intorno all'area di progettazione e scegliendo **Proprietà report**.  
  
-   Le proprietà degli elementi del report facendo clic con il pulsante destro del mouse sull'elemento e scegliendo **Proprietà**.  
  
 Per informazioni sull'uso della tastiera per modificare gli elementi nell'area di progettazione, vedere [Tasti di scelta rapida &#40;Generatore report&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
### <a name="design-surface-size-and-print-area"></a>Dimensioni dell'area di progettazione e area di stampa  
 Le dimensioni dell'area di progettazione potrebbero essere diverse da quelle dell'area di stampa della pagina specificata per stampare il report. La modifica delle dimensioni dell'area di progettazione non altera l'area di stampa del report. Indipendentemente dalle dimensioni impostate per l'area di stampa del report, le dimensioni totali dell'area di progettazione non vengono modificate. Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!TIP]  
>  Per visualizzare il righello, nella scheda **Visualizza** selezionare la casella di controllo **Righello**.  
  
  
##  <a name="the-report-data-pane"></a><a name="ReptDataPane"></a> The Report Data Pane  
 Nel riquadro Dati report è possibile definire le risorse e i dati relativi ai report necessari per un report prima di progettare il layout del report. È ad esempio possibile aggiungere origini dati, set di dati, campi calcolati, parametri del report e immagini al riquadro dei dati del report.  
  
 Dopo avere aggiunto elementi al riquadro dei dati del report, trascinare i campi negli elementi del report dell'area di progettazione per verificare in che punto del report vengono visualizzati i dati.  
  
> [!TIP]  
>  Se si trascina un campo dal riquadro dei dati del report direttamente nell'area di progettazione del report anziché posizionarlo in un'area dati quale una tabella o un grafico, durante l'esecuzione del report verrà visualizzato solo il primo valore dei dati in tale campo.  
  
 È anche possibile trascinare i campi predefiniti dal riquadro dei dati del report nell'area di progettazione del report. Quando vengono sottoposti a rendering, tali campi forniscono informazioni sul report, ad esempio il nome del report, il numero complessivo di pagine nel report e il numero di pagina corrente.  
  
 Alcuni elementi vengono aggiunti automaticamente al riquadro dei dati del report quando vengono effettuate delle aggiunte all'area di progettazione del report. Se ad esempio si aggiunge una parte del report dalla Raccolta parti del report e la parte del report si trova in un'area dati, il set di dati viene aggiunto automaticamente al riquadro dei dati del report. Per altre informazioni, vedere [Parti del report e set di dati in Generatore report](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md). Inoltre, se si incorpora un'immagine nel report, questa sarà aggiunta alla cartella Immagini nel riquadro dei dati del report.  
  
> [!NOTE]  
>  Per aggiungere un nuovo elemento al riquadro Dati report, usare il pulsante **Nuovo** . È possibile aggiungere al report più set di dati provenienti dalla stessa origine dati o da altre origini dati. I set di dati condivisi possono essere aggiunti dal server di report. Per aggiungere un nuovo set di dati dalla stessa origine dati, fare clic con il pulsante destro del mouse su un'origine dati e quindi scegliere **Aggiungi set di dati**.  
  
 Per altre informazioni sugli elementi nel riquadro Dati report, vedere gli argomenti seguenti:  
  
-   [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Immagini &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)  
  
-   [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
-   [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="the-report-part-gallery"></a><a name="ReptPartGallery"></a> Raccolta parti del report  
 Il modo più semplice per creare un report consiste nell'individuare una parte del report esistente, ad esempio una tabella o un grafico, nel server di report o in un server di report integrato in un sito di SharePoint.  
  
 Fare clic su **Parti del report** nella scheda Inserisci per aprire la Raccolta parti del report. Nella raccolta è possibile cercare le parti del report da aggiungere al report. Le parti del report possono essere filtrate in base al nome completo o parziale della relativa parte, all'autore di quest'ultima, all'utente che vi ha apportato l'ultima modifica, alla data dell'ultima modifica, alla posizione in cui è archiviata o in base al tipo di parte del report. Ad esempio, è possibile cercare tutti i grafici creati nell'ultima settimana da parte di uno dei colleghi.  
  
> [!NOTE]  
>  Per visualizzare la Raccolta parti del report è necessario essere connessi a un server.  
  
 È possibile visualizzare i risultati della ricerca come anteprime o come elenco e ordinare i risultati della ricerca in base al nome, alle date di creazione e di modifica e all'autore. Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
  
##  <a name="the-properties-pane-report-builder"></a><a name="PropertiesPane"></a> Riquadro Proprietà (Generatore report)  
 A ogni elemento di un report, inclusi le aree dati, le immagini, le caselle di testo e il corpo del report stesso, sono associate proprietà. La proprietà BorderColor di una casella di testo indica, ad esempio, il valore del colore del bordo della casella di testo, mentre la proprietà PageSize del report indica le dimensioni di pagina del report.  
  
 Queste proprietà vengono visualizzate nel riquadro Proprietà e variano a seconda dell'elemento del report selezionato.  
  
 Per visualizzare il riquadro Proprietà, fare clic su Proprietà nel gruppo Mostra/Nascondi della scheda Visualizza.  
  
### <a name="changing-property-values"></a>Modifica dei valori delle proprietà  
 In Generatore report è possibile modificare le proprietà degli elementi del report nei modi seguenti:  
  
-   Facendo clic sui pulsanti e negli elenchi sulla barra multifunzione.  
  
-   Modificando le impostazioni all'interno delle finestre di dialogo.  
  
-   Modificando i valori delle proprietà all'interno del riquadro Proprietà.  
  
 Le proprietà più comunemente usate sono disponibili nelle finestre di dialogo e sulla barra multifunzione.  
  
 A seconda della proprietà, è possibile impostare un valore per la proprietà in un elenco a discesa, digitare il valore oppure fare clic su `<Expression>` per creare un'espressione.  
  
### <a name="changing-the-properties-pane-view"></a>Modifica della vista del riquadro Proprietà  
 Per impostazione predefinita, le proprietà visualizzate nel riquadro Proprietà sono organizzate in ampie categorie, ad esempio Azione, Bordo, Riempimento, Carattere e Generale. A ogni categoria è associato un set di proprietà. Nella categoria Carattere vengono ad esempio elencate le proprietà seguenti: Color, FontFamily, FontSize, FontStyle, FontWeight, LineHeight e TextDecoration. Se lo si desidera, è possibile ordinare alfabeticamente tutte le proprietà elencate nel riquadro. In questo modo, le categorie verranno rimosse e tutte le proprietà verranno elencate in ordine alfabetico, indipendentemente dalla categoria a cui appartengono.  
  
 Nella parte superiore del riquadro Proprietà sono disponibili tre pulsanti, ovvero Per categoria, Per nome e Pagine delle proprietà. Fare clic sui pulsanti Categoria e Ordine alfabetico per passare da una vista all'altra del riquadro Proprietà. Fare clic sul pulsante **Pagine delle proprietà** per aprire la finestra di dialogo delle proprietà per l'elemento del report selezionato.  
  
  
##  <a name="the-grouping-pane-report-builder"></a><a name="GroupPane"></a> Riquadro di raggruppamento (Generatore report)  
 I gruppi vengono utilizzati per organizzare i dati del report in una gerarchia visiva e per calcolare i totali. È possibile visualizzare i gruppi di righe e di colonne inclusi in un'area dati nell'area di progettazione e nel riquadro di raggruppamento. Il riquadro di raggruppamento dispone di due riquadri: Gruppi di righe e Gruppi di colonne. Quando si seleziona un'area dati, nel riquadro di raggruppamento vengono visualizzati tutti i gruppi inclusi in tale area dati sotto forma di elenco gerarchico: i gruppi figlio vengono visualizzati rientrati sotto i relativi gruppi padre.  
  
 ![Gruppi di righe di Generatore report](../../reporting-services/report-builder/media/ssrb-rowgroups.png "Gruppi di righe di Generatore report")  
  
 È possibile creare gruppi trascinando i campi dal riquadro dei dati del report e rilasciandoli sull'area di progettazione o nel riquadro di raggruppamento. Nel riquadro di raggruppamento è possibile aggiungere gruppi padre, adiacenti e figlio, modificare le proprietà di gruppo ed eliminare gruppi.  
  
 Il riquadro di raggruppamento viene visualizzato per impostazione predefinita, ma è possibile chiuderlo deselezionando la casella di controllo Riquadro di raggruppamento nella scheda Visualizza. Il riquadro Raggruppamento non è disponibile per le aree dati Grafico e Misuratore.  
  
 Per altre informazioni, vedere [Riquadro di raggruppamento &#40;Generatore report&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md) e [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  
##  <a name="previewing-your-report-in-run-mode"></a><a name="RunMode"></a> Anteprima del report in modalità di esecuzione  
 Nella visualizzazione di progettazione report non si utilizzano i dati effettivi ma una rappresentazione degli stessi indicati tramite il nome del campo o l'espressione. Per vedere i dati effettivi nel contesto del report progettato, è possibile eseguire il report per visualizzare l'anteprima dei dati recuperati dal database sottostante visualizzato nel layout del report. È possibile passare dalla modalità progettazione a quella di esecuzione e viceversa per modificare la progettazione del report e visualizzarne i risultati immediatamente. Per visualizzare in anteprima il report, fare clic su **Esegui** nel gruppo **Viste** sulla barra multifunzione.  
  
 Quando si fa clic su **Esegui**, Generatore report si connette alle origini dati del report, memorizza i dati nella cache del computer, combina i dati e il layout ed esegue il rendering del report nel visualizzatore HTML. In fase di progettazione è possibile eseguire il report in qualsiasi momento. Dopo aver completato la progettazione del report e aver ottenuto il risultato desiderato, è possibile salvare il report nel server di report da cui gli utenti che dispongono delle autorizzazioni adeguate potranno visualizzarlo.  
   
 Per altre informazioni, vedere [Anteprima di report in Generatore report](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
### <a name="running-a-report-with-parameters"></a>Esecuzione di un report con parametri  
 Un report eseguito viene elaborato automaticamente. Se il report contiene parametri, tutti i parametri devono disporre di valori predefiniti prima che il report possa essere eseguito automaticamente. Se un parametro non ha un valore predefinito, quando si esegue il report è necessario scegliere un valore per il parametro e quindi fare clic su **Visualizza report** nella scheda Esegui. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="print-preview"></a>Anteprima di stampa  
 Quando un report visualizzato in anteprima in modalità di esecuzione assomiglia a un report prodotto in HTML. L'anteprima non è in formato HTML, ma il layout e la paginazione del report sono simili a quelli dell'output HTML. Se si passa alla modalità anteprima di stampa, è possibile visualizzare la rappresentazione del report stampato. Fare clic sul pulsante **Anteprima di stampa** nella scheda **Esegui** . Il report verrà visualizzato come in una pagina fisica. Questa visualizzazione assomiglia all'output generato dalle estensioni per il rendering delle immagini e PDF. L'anteprima di stampa non è un'immagine, né un file PDF, ma l'impaginazione e il layout del report sono simili a quelli dell'output in questi formati.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Generatore report in SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  
  
