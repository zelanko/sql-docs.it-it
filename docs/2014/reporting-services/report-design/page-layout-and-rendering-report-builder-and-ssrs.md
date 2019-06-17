---
title: Layout e rendering della pagina (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df28762c61f548b47c4da4a31fe1d1fd42fbf65a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105505"
---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>Layout e rendering della pagina (Generatore report e SSRS)
  Quando si creano report è importante capire il comportamento dei renderer di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per assicurarsi che il report visualizzabile corrisponda a quanto desiderato, inclusi il layout e le interruzioni di pagina. Sicuramente si desidera anche verificare che il report visualizzabile si adatti al formato della carta usato comunemente.  
  
 Quando i report vengono visualizzati in Gestione report o nel riquadro di anteprima di Generatore report o Progettazione report, il report viene innanzitutto sottoposto a rendering dal renderer HTML. Successivamente può essere esportato in formati diversi, ad esempio Excel o CSV (Comma Separated File, file con valori delimitati da virgole). Il report esportato può essere quindi usato per ulteriori analisi in Excel o come origine dati per applicazioni tramite cui è possibile importare e usare file di dati CSV.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un set di renderer per l'esportazione di report in formati diversi. Ogni renderer consente di applicare delle regole durante il rendering dei report. Quando si esporta un report in un formato di file diverso, soprattutto per renderer quali il renderer di Adobe Acrobat (PDF) che usa la paginazione in base alle dimensioni fisiche della pagina, potrebbe essere necessario modificare il layout del report affinché il report esportato venga visualizzato e stampato correttamente dopo aver applicato le regole di rendering.  
  
 L'ottenimento dei migliori risultati per i report esportati è spesso un processo iterativo; si crea e visualizza in anteprima il report in Generatore report o Progettazione report, si esporta il report nel formato preferito, si rivede il report esportato e infine si apportano le modifiche al report.  
  
 In questo argomento vengono fornite informazioni sulle estensioni per il rendering Reporting Services e sul relativo utilizzo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="PageLayout"></a> Layout di pagina e gli elementi del Report  
 Gli elementi del report sono elementi di layout associati a tipi diversi di dati del report. Tabella, Matrice, Elenco, Grafico e Misuratore sono elementi di report dell'area dati, ciascuno dei quali costituisce un collegamento a un set di dati del report. Durante l'elaborazione del report, l'area dati si espande nella pagina del report per visualizzare i dati. Gli altri elementi del report costituiscono un collegamento a un singolo elemento e consentono di visualizzare solo quest'ultimo. Un elemento del report **Immagine** costituisce un collegamento a un'immagine, mentre in un elemento del report **Casella di testo** è contenuto testo semplice, ad esempio un titolo o un'espressione in cui possono essere inclusi riferimenti a campi predefiniti, parametri di report o campi del set di dati. Gli elementi del report **Linea** e **Rettangolo** consentono di usare elementi grafici semplici nella pagina del report. L'elemento **Rettangolo** può inoltre essere usato come contenitore per altri elementi. In un report possono essere contenuti sottoreport.  
  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]è possibile inserire gli elementi del report in qualsiasi punto dell'area di progettazione. È possibile posizionare, espandere e comprimere in modo interattivo la forma iniziale dell'elemento di report usando guide di allineamento e quadratini di ridimensionamento. È possibile inoltre inserire aree dati affiancate con set di dati diversi o inserire gli stessi dati in formati diversi. Quando si inserisce un elemento del report nell'area di progettazione, all'elemento vengono associate una dimensione e una forma predefinite nonché una relazione iniziale con tutti gli altri elementi del report. È possibile inserire molti elementi del report l'uno nell'altro per creare strutture report più complesse. Ad esempio, grafici o immagini in celle della tabella, tabelle in celle della tabella e più immagini in un rettangolo. Oltre a fornire l'organizzazione e l'aspetto desiderato nel report, posizionando elementi del report in contenitori quali i rettangoli è possibile controllare la modalità di visualizzazione degli elementi del report nella pagina del report.  
  
 Un report può estendersi su più pagine. L'intestazione e il piè di pagina vengono ripetuti in ogni pagina. Un report può contenere elementi grafici diversi, ad esempio immagini e linee, e può essere caratterizzato da più tipi di carattere, colori e stili che possono essere basati sulle espressioni.  
  
##  <a name="ReportSections"></a> Sezioni del report  
 Un report è costituito da tre sezioni principali, ovvero un'intestazione di pagina e un piè di pagina facoltativi e un corpo del report. L'intestazione e il piè di pagina non rappresentano sezioni separate del report, ma sono inclusi tra gli elementi di report posizionati nella parte superiore e inferiore del corpo del report. L'intestazione e il piè di pagina consentono di ripetere lo stesso contenuto nella parte superiore e inferiore di ogni pagina del report. Nelle intestazioni e nei piè di pagina è possibile inserire immagini, caselle di testo e linee, mentre nel corpo del report è possibile inserire tutti i tipi di elementi di report.  
  
 È possibile impostare proprietà relative agli elementi di report per nasconderli o visualizzarli inizialmente nella pagina. È inoltre possibile impostare proprietà di visibilità per righe, colonne o gruppi per le aree dati e fornire interruttori per consentire all'utente di visualizzare o nascondere i dati del report in modo interattivo, nonché impostare la visibilità, iniziale o meno, usando espressioni, ad esempio quelle basate sui parametri di report.  
  
 Durante l'elaborazione del report, i relativi dati vengono combinati con gli elementi di layout del report e successivamente inviati a un renderer del report. In base a regole predefinite per l'espansione degli elementi di report, il renderer determina il livello di adattamento dei dati in ogni pagina. Per progettare un report leggibile ottimizzato per il renderer da utilizzare, è necessario comprendere le regole utilizzate per controllare la paginazione in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per altre informazioni, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="RenderingExtensions"></a> Renderer  
 In Reporting Services è disponibile un set di renderer, anche definiti estensioni per il rendering, che è possibile usare per esportare i report in formati diversi. Sono disponibili tre tipi di renderer:  
  
-   **Renderer di dati** I renderer di dati rimuovono tutte le informazioni di formattazione e layout dal report e visualizzano solo i dati. Il file risultante può essere usato per importare i dati del report non elaborati in un altro tipo di file, ad esempio Excel, in un altro database, in un messaggio di dati XML o in un'applicazione personalizzata. I renderer di dati disponibili sono: CSV e XML.  
  
    > [!NOTE]  
    >  Sebbene non fornisca un'esportazione diretta in un formato diverso, il rendering Atom genera file di dati dai report.  
  
-   **Renderer di interruzioni di pagina software** I renderer di interruzioni di pagina software mantengono il layout e la formattazione del report. Il file risultante è ottimizzato per la visualizzazione su schermo e il recapito, ad esempio in una pagina Web. I renderer di interruzioni pagina software disponibili sono: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, archivio Web (MHTML) e HTML.  
  
-   **Renderer di interruzioni di pagina manuali** I renderer di interruzioni di pagina manuali mantengono il layout e la formattazione del report. Il file risultante è ottimizzato per garantire una stampa coerente o per la visualizzazione del report online in formato libro. Sono supportati i renderer di interruzioni pagina manuali disponibili: TIFF e PDF.  
  
 Quando si visualizza un report in anteprima in Generatore report o Progettazione report oppure si esegue un report in Gestione report, il report viene sempre prima sottoposto a rendering in HTML. Dopo avere eseguito il report, sarà possibile esportarlo nei vari formati di file. Per altre informazioni, vedere [esportazione di report &#40;Generatore Report e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
  
  
##  <a name="RenderingBehaviors"></a> Tipi di rendering  
 A seconda del renderer selezionato, durante il rendering del report vengono applicate alcune regole. La disposizione degli elementi del report in una pagina dipende dalla combinazione dei seguenti fattori:  
  
-   Regole di rendering.  
  
-   Larghezza e altezza degli elementi del report.  
  
-   Dimensioni del corpo del report.  
  
-   Larghezza e altezza della pagina.  
  
-   Supporto specifico del renderer per la paginazione.  
  
 Ad esempio i report sottoposti a rendering nei formati HTML e MHTML vengono ottimizzati per la visualizzazione sullo schermo di un computer di pagine di lunghezze diverse.  
  
 Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
  
  
##  <a name="Pagination"></a> Paginazione  
 Il termine paginazione si riferisce al numero di pagine all'interno di un report e alla disposizione degli elementi del report in tali pagine. In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , la paginazione varia a seconda dell'estensione per il rendering utilizzata per visualizzare e recapitare il report, nonché delle opzioni di interruzione di pagina e raggruppamento configurate per il report.  
  
 Per progettare correttamente un report di facile lettura e ottimizzato per il renderer che si intende usare per recapitare il report, è necessario comprendere le regole usate per controllare la paginazione in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. I report esportati tramite le estensioni per il rendering di dati e di interruzioni di pagina software non sono generalmente influenzati dalla paginazione. Quando si usa un'estensione per il rendering di dati, il report viene sottoposto a rendering come set di righe tabulare in formato XML o CSV. Per assicurarsi che i dati del report esportati siano utilizzabili, è necessario comprendere le regole applicate per eseguire il rendering di un set di righe tabulare bidimensionale da un report.  
  
 Quando si usa un'estensione per il rendering di interruzioni di pagina software, ad esempio l'estensione per il rendering HTML, è possibile che si desideri conoscere l'aspetto del report stampato, nonché la relativa qualità di rendering usando un renderer di interruzioni di pagina manuali, ad esempio in PDF. Un report può essere visualizzato in anteprima ed esportato in Generatore report e Progettazione report durante la creazione o l'aggiornamento.  
  
 I renderer di interruzioni di pagina manuali influenzano soprattutto il layout del report e le dimensioni fisiche della pagina. Per sapere di più, vedere [Paginazione in Reporting Service &#40;Generatore report e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione vengono elencate le procedure in cui viene mostrato in dettaglio l'utilizzo della paginazione nei report.  
  
-   [Aggiungere un'interruzione di pagina &#40;Generatore report e SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md)  
  
-   [Visualizzare le intestazioni di riga e colonna in più pagine &#40;Generatore report e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [Aggiungere o rimuovere un'intestazione o un piè di pagina &#40;Generatore report e SSRS&#41;](add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [Visualizzazione delle intestazioni durante lo scorrimento di un report &#40;Generatore report e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [Visualizzare i numeri di pagina o altre proprietà del report &#40;Generatore report e SSRS&#41;](display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [Nascondere un'intestazione o un piè di pagina nella prima o nell'ultima pagina &#40;Generatore report e SSRS&#41;](hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
  
  
##  <a name="InThisSection"></a> Contenuto della sezione  
 Negli argomenti seguenti vengono fornite ulteriori informazioni sul layout e sul rendering della pagina.  
  
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sull'utilizzo di intestazioni e piè di pagina nei report e sul controllo della paginazione attraverso questi elementi.  
  
 [Controllo di interruzioni di pagina, intestazioni, colonne e righe &#40;Generatore report e SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sull'utilizzo delle interruzioni di pagina.  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Esportazione di report &#40;Report e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
