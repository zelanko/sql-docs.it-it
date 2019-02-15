---
title: Esportazione di report (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8ef4cfaec1b66c9840d0dcf08d788b66b7107190
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291900"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>Esportazione di report (Generatore report e SSRS)
  Dopo avere eseguito un report, è possibile esportarlo in un altro formato, ad esempio Excel o PDF, oppure esportarlo generando un documento di servizio Atom, elencando tutti i feed di dati conformi ad Atom disponibili dal report.  
  
 Esportare un report per effettuare le operazioni seguenti:  
  
-   Usare i dati del report in un'altra applicazione. Ad esempio, è possibile esportare il report in Excel e continuare a lavorare con i dati in questa applicazione.  
  
-   Stampare il report in un formato diverso. Ad esempio, è possibile esportare il report nel formato di file PDF e quindi stamparlo.  
  
-   Salvare una copia del report come un altro tipo di file. Ad esempio, è possibile esportare un report in Word e salvarlo, creando una copia del report.  
  
-   Usare i dati del report come feed di dati nelle applicazioni. Ad esempio, è possibile generare feed di dati conformi ad Atom utilizzabili dal client [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e quindi usare i dati in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 L'opzione di esportazione è disponibile sulla barra degli strumenti del visualizzatore di report di Gestione report, disponibile nella parte superiore di ogni report quando si visualizza un report nel server di report e sulla barra multifunzione di Generatore report quando si visualizza l'anteprima di un report. L'opzione feed di dati è disponibile unicamente in Gestione report.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono disponibili molte estensioni per il rendering che consentono di esportare i report in formati di file comuni. Le estensioni per il rendering supportano i formati di file con interruzioni di pagina automatiche, ad esempio Word o Excel, interruzioni di pagina manuali, ad esempio PDF o TIFF, o solo dati, ad esempio CSV o XML conformi ad Atom.  
  
 Per iniziare rapidamente a esportare report e la generazione di feed di dati conformi ad Atom da report, vedere [esportare un Report in un altro tipo di File &#40;Generatore Report e SSRS&#41; ](../export-a-report-as-another-file-type-report-builder-and-ssrs.md) e [generare feed di dati da un Report &#40;Report e SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RendererTypes"></a> Tipi di estensioni per il rendering  
 Sono disponibili tre tipi di estensioni per il rendering [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   **Estensioni per il renderer di dati** Le estensioni per il rendering di dati rimuovono tutte le informazioni di formattazione e layout dal report e visualizzano solo i dati. Il file risultante può essere usato per importare i dati del report non elaborati in un altro tipo di file, ad esempio Excel, in un altro database, in un messaggio di dati XML o in un'applicazione personalizzata. I renderer di dati non supportano le interruzioni di pagina.  
  
     Sono supportate le estensioni seguenti per il rendering di dati: CSV, XML e Atom.  
  
-   **Estensioni per il renderer interruzione di pagina automatica** Le estensioni per il rendering di interruzioni di pagina automatiche mantengono il layout e la formattazione del report. Il file risultante è ottimizzato per la visualizzazione su schermo e il recapito, ad esempio in una pagina Web o nei controlli **ReportViewer** .  
  
     Sono supportate le estensioni per il rendering di interruzioni di pagina automatiche: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word e Archivio Web (MHTML).  
  
-   **Estensioni per il renderer interruzione di pagina manuale** Le estensioni per il rendering di interruzioni di pagina manuali mantengono il layout e la formattazione del report. Il file risultante è ottimizzato per garantire una stampa coerente o per la visualizzazione del report online in formato libro.  
  
     Sono supportate le estensioni per il rendering di interruzioni di pagina manuali: TIFF e PDF.  
  
##  <a name="ExportFormats"></a> Formati di esportazione  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono disponibili estensioni per il rendering per l'esecuzione del rendering dei report in formati diversi. Se si intende usare questa caratteristica, sarà necessario ottimizzare la progettazione del report per il formato di file scelto. L'argomento relativo a ogni estensione per il rendering contiene informazioni dettagliate sul rendering del report in tale formato.  
  
 Nella tabella seguente sono elencati i formati disponibili.  
  
|Formato|Tipi di estensione per il rendering|Descrizione|  
|------------|------------------------------|-----------------|  
|CSV|Dati|L'estensione per il rendering CSV (Comma-Separated Value) consente di eseguire il rendering di report come rappresentazione bidimensionale dei dati di un report in un formato di testo normale standardizzato, facilmente leggibile e interscambiabile con numerose applicazioni.<br /><br /> Per altre informazioni, vedere [Esportazione in un file CSV &#40;Generatore report e SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md).|  
|Excel|Interruzione di pagina automatica|L'estensione per il rendering di Excel esegue il rendering di un report come documento di Excel compatibile con [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010 e con [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 con Microsoft Office Compatibility Pack per i formati di file Word, Excel e PowerPoint. Nel report che viene esportato in un foglio di lavoro di Excel vengono rimossi alcuni elementi di layout e della progettazione originale. È possibile impostare proprietà del report e dei gruppi all'interno del report in modo da assegnare nomi alle schede dei fogli di lavoro quando si esporta il report in Excel. L'estensione dei nomi file generato dal renderer è xlsx.<br /><br /> Per altre informazioni, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md).<br /><br /> Nota: L'estensione per il rendering di Excel 2003 che esegue il rendering nel formato nativo di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 è disponibile in alcuni scenari di report.|  
|Word|Interruzione di pagina automatica|L'estensione per il rendering di Word esegue il rendering di un report come documento di Word compatibile con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 e con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Compatibility Pack per i formati di file Word, Excel e PowerPoint. Dopo l'esportazione del report in un documento di Word, è possibile modificarne il contenuto e progettare report in formato documento, ad esempio etichette di indirizzi, ordini di acquisto o lettere tipo. L'estensione dei file generati da questo renderer è docx.<br /><br /> Per altre informazioni, vedere [Esportazione in Microsoft Word &#40;Generatore report e SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md).<br /><br /> Nota: L'estensione per il rendering di Word 2003 che esegue il rendering nel formato nativo di [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 è disponibile in alcuni scenari di report.|  
|Archivio Web|Interruzione di pagina automatica|L'estensione per il rendering HTML consente di eseguire il rendering di un report in formato HTML. Può inoltre generare pagine HTML complete o frammenti di HTML da incorporare in altre pagine HTML. Tutto il codice HTML viene generato con la codifica UTF-8.<br /><br /> L'estensione per il rendering HTML è l'estensione per il rendering predefinita per i report dei quali viene visualizzata l'anteprima in Generatore report e che vengono visualizzati in un browser, inclusi quelli eseguiti in Gestione report.<br /><br /> Per altre informazioni, vedere [Rendering in formato HTML &#40;Generatore report e SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md).|  
|File Acrobat (PDF)|Interruzione di pagina manuale|L'estensione per il rendering PDF consente di eseguire il rendering di un report in file che possono essere aperti in Adobe Acrobat e in altri visualizzatori PDF di terze parti che supportano il formato PDF 1.3. Anche se PDF 1.3 è compatibile con Adobe Acrobat 4.0 e versioni successive, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta Adobe Acrobat 6 e versioni successive. Non è necessaria l'applicazione Adobe per convertire i report mediante l'estensione per il rendering. I visualizzatori PDF, ad esempio Adobe Acrobat, sono tuttavia necessari per visualizzare o stampare un report in formato PDF.<br /><br /> Per altre informazioni, vedere [Esportazione in un file PDF &#40;Generatore report e SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md).|  
|File TIFF|Interruzione di pagina manuale|L'estensione per il rendering delle immagini genera bitmap o metafile dei report. Per impostazione predefinita, l'estensione per il rendering delle immagini crea un file TIFF del report, che può essere visualizzato in più pagine. Nel client l'immagine può essere visualizzata in un visualizzatore di immagini e stampata.<br /><br /> L'estensione per il rendering delle immagini permette di generare file in tutti i formati supportati da [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG e TIFF.<br /><br /> Per altre informazioni, vedere [Esportazione in un file di immagine &#40;Generatore report e SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md).|  
|XML|Dati|L'estensione per il rendering XML genera report in formato XML. Lo schema per il report XML è specifico del report e contiene solo dati. Il rendering delle informazioni di layout non viene eseguito e la paginazione non viene mantenuta dall'estensione per il rendering XML. Il codice XML generato da questa estensione può essere importato in un database, usato come messaggio di dati XML o inviato a un'applicazione personalizzata.<br /><br /> Per altre informazioni, vedere [Esportazione in XML &#40;Generatore report e SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md).|  
|Atom|Dati|L'estensione per il rendering Atom genera feed di dati conformi ad Atom dai report. I feed di dati sono leggibili e interscambiabili con applicazioni come il client [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in grado di usare i feed di dati conformi ad Atom.<br /><br /> L'output è un documento di servizio Atom in cui sono elencati i feed di dati disponibili in un report. Per ogni area dati di un report viene creato almeno un feed di dati. A seconda del tipo di area dati e dei dati in essa contenuti, potrebbero essere generati più feed di dati.<br /><br /> Per altre informazioni, vedere [Generazione di feed di dati dai report &#40;Generatore report e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).|  
  
##  <a name="ExportingReport"></a> Esportazione di un Report  
 Per esportare un report, eseguirlo in Gestione report o Generatore report, quindi selezionare un formato nell'elenco a discesa Esporta. Verrà chiesto se si desidera salvare o aprire il file. Se si sceglie **Apri**, il report verrà aperto nell'applicazione associata al formato di rendering selezionato. Ad esempio, se si seleziona **Excel** , il report verrà aperto in Excel. Se si sceglie **Salva**, il report verrà salvato. Ad esempio, se si sta esportando in formato Excel, il report verrà salvato come file con estensione xls. Le associazioni tra tipi di file e programmi impostate per il computer locale determinano l'applicazione usata per un determinato formato di rendering. Per altre informazioni, vedere [esportare un Report in un altro tipo di File &#40;Generatore Report e SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md).  
  
 Il server di report esporta il report con le caratteristiche presenti nella sessione utente corrente. Se un altro utente pubblica una versione aggiornata del report mentre questo è aperto o vengono apportate modifiche ai dati visualizzati dal report, il report esportato non verrà aggiornato.  
  
 È probabile che l'impaginazione del report possa subire variazioni quando si esporta un report in un formato diverso. Quando si esegue l'anteprima di un report, si visualizza il report sottoposto a rendering dall'estensione per il rendering HTML che si basa sulle regole dell'interruzione di pagina automatica. Quando si esporta un report in un formato di file diverso, ad esempio Adobe Acrobat (PDF), l'impaginazione si basa sulle dimensioni fisiche della pagina che segue le regole dell'interruzione di pagina manuale. Le pagine possono anche essere separate da interruzioni di pagina logiche aggiunte a un report, ma la lunghezza effettiva delle pagine varia in base al tipo di renderer utilizzato. Per modificare l'impaginazione del report, è necessario comprendere il comportamento dell'impaginazione dell'estensione per il rendering scelto. Potrebbe essere necessario modificare la progettazione del layout del report per questa estensione del rendering. Per altre informazioni, vedere [Layout e rendering della pagina &#40;Generatore report e SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
##  <a name="GeneratingDataFeedsFromReport"></a> Generazione di feed di dati da un report  
 Per generare feed di dati da un report, eseguire il report in Gestione report, quindi fare clic sull'icona **Generazione di feed di dati** sulla barra degli strumenti di Gestione report. Verrà chiesto se si desidera salvare o aprire il file. Se si sceglie **Apri**, il documento di servizio Atom verrà aperto nell'applicazione associata all'estensione di file atomsvc. Se si sceglie **Salva**, il documento verrà salvato come file con estensione atomsvc. Per impostazione predefinita, il nome del file corrisponde al nome del report. È possibile modificare il nome per renderlo più descrittivo.  
  
 Salvare il documento di servizio Atom nel computer. In un secondo momento sarà possibile caricarlo in un server di report o in un altro server per renderlo disponibile ad altri utenti. Per altre informazioni, vedere [Generazione di feed di dati dai report &#40;Generatore report e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md) e [Generare i feed di dati da un report &#40;Generatore report e SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
##  <a name="Troubleshooting"></a> Risoluzione dei problemi relativi ai report esportati  
 Dopo averli esportati in un formato diverso, i report possono presentare un aspetto diverso o non funzionare nel modo desiderato. Questo dipende dal fatto che al renderer potrebbero applicarsi determinate regole e limitazioni. È possibile superare molte limitazioni semplicemente tenendole presenti durante la creazione del report. Potrebbe essere necessario utilizzare un layout leggermente diverso nel report, allineare con cura gli elementi all'interno del report, limitare i piè di pagina del report a una sola riga di testo e così via.  
  
 Se il report include testo Unicode con numeri arabi o include date in arabo, il rendering di date e numeri non sarà eseguito correttamente quando si esporta il report in uno dei formati seguenti o si stampa il report.  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   Image/TIFF  
  
 Se si esporta il report in HTML, il rendering di date e numeri sarà eseguito correttamente.  
  
 Negli argomenti relativi a renderer specifici vengono illustrate le modalità di rendering degli elementi e delle aree dati del report, nonché le limitazioni e le soluzioni per ogni renderer.  
  
-   [Esportazione in un file CSV &#40;Generatore report e SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Esportazione in Microsoft Word &#40;Generatore report e SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [Rendering in formato HTML &#40;Generatore report e SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [Esportazione in un file PDF &#40;Generatore report e SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [Esportazione in un file di immagine &#40;Generatore report e SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [Esportazione in XML &#40;Generatore report e SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [Generazione di feed di dati dai report &#40;Generatore report e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] rende disponibili caratteristiche aggiuntive che consentono di creare report utilizzabili in modo ottimale in altri formati. Le interruzioni di pagina nelle aree dati Tablix (tabella, matrice ed elenco), nei gruppi e nei rettangoli consentono di controllare meglio la paginazione del report. Le pagine del report, delimitate da interruzioni di pagina, possono disporre di nomi diversi ed è possibile anche reimpostarne la numerazione. Tramite le espressioni, i nomi e i numeri delle pagine possono essere aggiornati dinamicamente in fase di esecuzione del report. Per altre informazioni, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 È inoltre possibile utilizzare l'elemento globale predefinito RenderFormat per applicare in modo condizionale differenti layout del report per renderer diversi. Per altre informazioni, vedere [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
##  <a name="OtherWaysExportingReports"></a> Altri modi di esportare report  
 L'esportazione di un report è un'attività su richiesta che viene eseguita con il report aperto in Gestione report o Generatore report. Se si desidera automatizzare un'operazione di esportazione, ad esempio per esportare un report in una cartella condivisa con un tipo di file specifico su base periodica, sarà necessario creare una sottoscrizione per il recapito del report nella cartella condivisa. Per ulteriori informazioni, vedere [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
 Dei report visualizzati in anteprima negli strumenti per la creazione di report o aperti in un browser, ad esempio Gestione report, viene sempre eseguito il rendering in HTML. Non è possibile specificare un'estensione di rendering diversa come impostazione predefinita per la visualizzazione. È tuttavia possibile creare una sottoscrizione che generi un report nel formato di rendering desiderato per il successivo recapito nella Posta in arrivo o in una cartella condivisa. Per altre informazioni, vedere [creare, modificare ed eliminare sottoscrizioni Standard &#40;Reporting Services in modalità nativa&#41; ](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) e [creare, modificare ed eliminare una sottoscrizione guidata dai dati](../subscriptions/data-driven-subscriptions.md).  
  
 È inoltre possibile accedere a un report tramite un URL che specifica un'estensione per il rendering come parametro URL ed eseguire il rendering direttamente nel formato specificato senza prima eseguirlo in HTML. Nell'esempio seguente viene eseguito il rendering di un report nel formato Excel:  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 Per altre informazioni, vedere [Export a Report Using URL Access](../export-a-report-using-url-access.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Controllo di interruzioni di pagina, intestazioni, colonne e righe &#40;Generatore report e SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Stampare report &#40;Generatore report e SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [Salvataggio di report &#40;Generatore report&#41;](saving-reports-report-builder.md)  
  
  
