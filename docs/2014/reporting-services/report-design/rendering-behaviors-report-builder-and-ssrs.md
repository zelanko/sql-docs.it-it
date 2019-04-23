---
title: Tipi di rendering (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: effd50dc38610b4a3f059df8609cb9279e268b13
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967429"
---
# <a name="rendering-behaviors-report-builder--and-ssrs"></a>Tipi di rendering (Generatore report e SSRS)
  A seconda del renderer selezionato, vengono applicate regole specifiche al corpo del report e al relativo contenuto durante il rendering di un report. La disposizione degli elementi del report in una pagina dipende dalla combinazione dei seguenti fattori:  
  
-   Regole di rendering.  
  
-   Larghezza e altezza degli elementi del report.  
  
-   Dimensioni del corpo del report.  
  
-   Larghezza e altezza della pagina.  
  
-   Supporto specifico del renderer per la paginazione.  
  
 In questo argomento vengono illustrate le regole generali applicate da Reporting Services. Per altre informazioni, vedere [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md), [Rendering delle aree dati &#40;Generatore report e SSRS&#41;](rendering-data-regions-report-builder-and-ssrs.md), e [Rendering dei dati &#40;Generatore report e SSRS&#41;](rendering-data-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="general-behaviors-for-html-mhtml-word-and-excel-soft-page-break-renderers"></a>Comportamenti generali per HTML, MHTML, Word e Excel (renderer di interruzioni di pagina automatiche)  
 I report esportati utilizzando i formati HTML e MHTML sono ottimizzati per la visualizzazione sullo schermo di un computer di pagine di lunghezze diverse. Le interruzioni di pagina vengono inserite verticalmente solo in punti approssimativi all'interno del corpo del report. Tali punti approssimativi dipendono dall'impostazione relativa all'altezza interattiva nel riquadro Proprietà. Si supponga ad esempio che l'altezza interattiva sia impostata su 12 centimetri. Quando si esegue il rendering del report, l'altezza della pagina corrisponderà a 12 centimetri. In Word ed Excel l'impaginazione è basata su interruzioni di pagina logiche, pertanto l'impostazione relativa all'altezza interattiva viene ignorata.  
  
> [!NOTE]  
>  Per determinare la modalità di visualizzazione di un report in un renderer di interruzioni di pagina automatiche, utilizzare Anteprima report. Il report verrà visualizzato come in formato HTML, MHTML, Word o Excel.  
  
 In caso di esportazione di un report in HTML, MHTML, Word o Excel, vengono adottate le seguenti regole generali:  
  
-   Agli elementi del report vengono applicate interruzioni di pagina logiche, ovvero interruzioni di pagina inserite in modo esplicito. Se ad esempio si inserisce un'interruzione di pagina tra ogni gruppo, le interruzioni verranno applicate durante il rendering del report.  
  
-   Viene creato un layout approssimativo utilizzando l'altezza della pagina e il numero di occorrenze dell'elemento nel report. Se ad esempio una casella di testo è alta 1,2 centimetri e si ripete cinque volte nel report, verranno riservati 6,3 centimetri.  
  
-   Vengono inserite più interruzioni di pagina automatiche in base all'impostazione relativa all'altezza interattiva. Per eliminarle nel formato HTML e nei controlli ReportViewer e controllare la paginazione solo con interruzioni di pagina esplicite, impostare il valore **altezza interattiva** su 0 o su un valore estremamente elevato.  
  
    > [!NOTE]  
    >  L'impostazione relativa alla larghezza interattiva non viene utilizzata nei renderer con interruzioni di pagina automatiche.  
  
-   La dimensione delle pagine del report può aumentare per consentire l'inserimento di righe isolate, righe orfane ed elementi del report che è necessario mantenere uniti. Il report può pertanto estendersi oltre la larghezza dello schermo ed essere visualizzato utilizzando barre di scorrimento.  
  
-   La paginazione viene applicata solo verticalmente ai report.  
  
-   I margini di pagina non vengono applicati.  
  
## <a name="general-behaviors-for-pdf-image-and-print-hard-page-break-renderers"></a>Comportamenti generali per i formati PDF, immagine e stampa (renderer di interruzioni di pagina manuali)  
 I report esportati utilizzando i formati PDF e immagine sono ottimizzati per la stampa o la visualizzazione di documenti formattati come libri in cui le dimensioni delle pagine sono uniformi. Le interruzioni di pagina vengono inserite verticalmente e orizzontalmente in punti specifici all'interno del corpo del report. Tali punti specifici dipendono dalle impostazioni relative alla larghezza e all'altezza della pagina.  
  
> [!NOTE]  
>  Per determinare la modalità di visualizzazione di un report in un renderer di interruzioni di pagina manuali, utilizzare Anteprima di stampa. Il report verrà visualizzato come in formato PDF o immagine.  
  
-   Le pagine sono numerate in sequenza da sinistra verso destra e quindi dall'alto verso il basso.  
  
-   Agli elementi del report vengono applicate interruzioni di pagina logiche, ovvero interruzioni di pagina inserite in modo esplicito. Tali interruzioni di pagina possono comportare lo spostamento di elementi nella pagina successiva.  
  
-   Se si verifica un'interruzione di pagina fisica in elementi del report che devono essere mantenuti uniti, tutti gli elementi da mantenere uniti vengono spostati nella pagina successiva.  
  
-   A causa di vincoli relativi alle dimensioni della pagina, potrebbe non essere possibile mantenere uniti tutti gli elementi o ripetere elementi. In tale circostanza, il renderer potrebbe ignorare determinate regole per la ripetizione con un altro elemento allo scopo di consentire l'inserimento dell'elemento del report nella pagina.  
  
-   Se un elemento non può essere mantenuto unito, ad esempio una casella di testo che diventa troppo grande per essere inserita nell'area utilizzabile della pagina verticale, l'elemento verrà tagliato in corrispondenza del limite della pagina fisica e continuerà nella pagina successiva.  
  
-   La paginazione viene applicata verticalmente e orizzontalmente ai report.  
  
    > [!NOTE]  
    >  L'impostazione relativa alla larghezza interattiva non viene utilizzata nei renderer di interruzioni di pagina manuali.  
  
## <a name="minimum-spacing-between-report-items"></a>Spaziatura minima tra gli elementi del report  
 Gli elementi del report si espandono all'interno del corpo del report per consentire l'inserimento del relativo contenuto. Durante il rendering del report un'area dati della matrice, ad esempio, si espande in genere in larghezza e in lunghezza nella pagina e l'altezza di una casella di testo viene regolata in base ai dati restituiti da un'espressione.  
  
 I renderer mantengono lo spazio minimo tra gli elementi del report definiti nel layout del report. Quando si posiziona un elemento del report accanto a un altro nel layout del report, la distanza tra gli elementi diventa la distanza minima da mantenere quando le dimensioni del report aumentano in orizzontale o in verticale. Se ad esempio si aggiunge un'area dati della matrice a un report e quindi si aggiunge un rettangolo da 0,06 centimetri a destra della matrice, tale spazio verrà mantenuto anche in caso di aumento delle dimensioni della matrice. Ogni elemento si sposta verso destra in modo da mantenere la distanza minima dagli elementi che terminano alla sua sinistra.  
  
## <a name="page-headers-and-footers"></a>Intestazioni di pagina e piè di pagina  
 Le intestazioni e i piè di pagina appaiono nella parte superiore e inferiore di ogni pagina di cui viene eseguito il rendering. È possibile formattare l'intestazione e il piè di pagina in modo da includere un colore, uno stile e una larghezza per il bordo. È inoltre possibile aggiungere un colore o un'immagine di sfondo. A seconda del formato scelto, viene eseguito il rendering di tutte queste opzioni di formattazione.  
  
 Alle intestazioni e ai piè di pagina di cui viene eseguito il rendering in formato HTML o MHTML si applicano le seguenti regole:  
  
> [!NOTE]  
>  Per informazioni sul rendering di intestazioni e piè di pagina in Excel, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md). Per informazioni sul rendering di intestazioni e piè di pagina in Word, vedere [Esportazione in Microsoft Word &#40;Generatore report e SSRS&#41;](../report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
-   Il rendering delle eventuali intestazioni e piè di pagina viene eseguito nella parte superiore e inferiore di ogni pagina all'interno dell'area utilizzabile della pagina.  
  
-   Nelle pagine in cui l'intestazione o il piè di pagina è nascosto, l'altezza dell'intestazione o del piè di pagina rimane riservata all'interno dell'area utilizzabile della pagina anche se il rendering dell'intestazione o del piè di pagina non viene eseguito.  
  
-   Se il contenuto dell'intestazione o del piè di pagina si estende oltre i limiti dell'intestazione o del piè di pagina, le dimensioni dell'intestazione o del piè di pagina vengono aumentate per consentire l'inserimento del contenuto.  
  
 Alle intestazioni e ai piè di pagina di cui viene eseguito il rendering in formato PDF o immagine si applicano le seguenti regole:  
  
-   Il rendering delle intestazioni e dei piè di pagina viene eseguito nella parte superiore e inferiore di ogni pagina all'interno dell'area utilizzabile della pagina.  
  
-   Nelle pagine in cui l'intestazione o il piè di pagina è nascosto, l'altezza dell'intestazione o del piè di pagina rimane riservata all'interno dell'area utilizzabile della pagina anche se il rendering dell'intestazione o del piè di pagina non viene eseguito.  
  
-   L'intestazione e il piè di pagina non vengono espansi o ridotti di dimensione, ma ne viene eseguito il rendering in ogni pagina con l'altezza specificata al momento della creazione.  
  
-   Indipendentemente dal numero di colonne all'interno del report, è presente una sola intestazione e un solo piè di pagina per pagina.  
  
-   Se il contenuto dell'intestazione o il piè di pagina si estende oltre i limiti dell'intestazione o del piè di pagina, il contenuto viene tagliato.  
  
-   Il rendering di intestazioni e piè di pagina definiti nel file RDL originale non viene eseguito quando il rendering del report viene eseguito come sottoreport.  
  
## <a name="logical-page-breaks"></a>Interruzioni di pagina logiche  
 Le interruzioni di pagina logiche sono interruzioni di pagina inserite prima o dopo elementi del report o gruppi. Consentono di adattare i contenuti alle pagine dei report in modo da ottenere una visualizzazione ottimale quando si esegue l'esportazione o il rendering del report.  
  
 Per il rendering delle interruzioni di pagina logiche si applicano le seguenti regole:  
  
-   Le interruzioni di pagina logiche vengono ignorate per gli elementi del report che rimangono sempre nascosti e per gli elementi del report la cui visibilità viene controllata facendo clic su un altro elemento del report.  
  
-   Le interruzioni di pagina logiche vengono applicate agli elementi visibili in base a determinate condizioni se sono visibili nel momento in cui viene eseguito il rendering del report.  
  
-   Tra l'elemento del report contenente l'interruzione di pagina logica e i relativi elementi di pari livello viene mantenuto lo spazio originale.  
  
-   Le interruzioni di pagina logiche inserite prima di un elemento del report comportano lo spostamento verso il basso dell'elemento del report nella pagina successiva. Il rendering dell'elemento del report viene eseguito all'inizio della pagina successiva.  
  
-   Le interruzioni di pagina logiche definite su elementi contenuti in celle di tabella o matrice non vengono mantenute. Questo comportamento non viene applicato agli elementi negli elenchi.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering in formato HTML &#40;Generatore report e SSRS&#41;](../report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [Layout e rendering della pagina &#40;Generatore report e SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
