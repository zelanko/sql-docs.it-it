---
title: Riferimento ai parametri di accesso con URL | Microsoft Docs
description: Usare i parametri in questo articolo come parte di un URL per configurare l'aspetto dei report di Reporting Services.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ac67de4831d1785f17029bc6c68fa6f7d8aeb16
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77147380"
---
# <a name="url-access-parameter-reference"></a>Riferimento ai parametri di accesso con URL

  È possibile usare i parametri seguenti come parte di un URL per configurare l'aspetto dei report di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. I parametri più comuni sono elencati in questa sezione: I parametri rilevano la distinzione tra maiuscole e minuscole e iniziano con i prefissi di parametro *rs:* se indirizzati al server di report e *rc:* se indirizzati a un visualizzatore HTML. È inoltre possibile specificare parametri specifici per dispositivi o estensioni per il rendering. Per altre informazioni sui parametri specifici per il dispositivo, vedere [Specificare le impostazioni relative alle informazioni sul dispositivo in un URL](../reporting-services/specify-device-information-settings-in-a-url.md).
  
> [!IMPORTANT]  
>  Per un server di report in modalità SharePoint è importante che l'URL includa la sintassi proxy `_vti_bin` per indirizzare la richiesta attraverso SharePoint e il proxy HTTP di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Il proxy aggiunge alla richiesta HTTP il contesto necessario a garantire l'esecuzione corretta dei report per i server di report in modalità SharePoint. Per gli esempi, vedere [Accesso agli elementi del server di report usando l'accesso tramite URL](../reporting-services/access-report-server-items-using-url-access.md).
> 
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  

##  <a name="html-viewer-commands-rc"></a><a name="bkmk_htmlviewer"></a> Comandi del visualizzatore HTML (rc:)
 - I comandi del visualizzatore HTML vengono usati per usare il visualizzatore HTML come destinazione e sono preceduti dal prefisso *rc:* :
  
-   **Barra degli strumenti**: Visualizza o nasconde la barra degli strumenti. Se il valore di questo parametro è **false**, tutte le opzioni rimanenti vengono ignorate. Se si omette questo parametro, la barra degli strumenti viene visualizzata automaticamente nei formati di rendering che la supportano. Il valore predefinito di questo parametro è **true**.
  
    > [!IMPORTANT]  
    >  *rc:Toolbar*=**false** non funziona per stringhe di accesso con URL che usano un indirizzo IP, invece un nome di dominio, per fare riferimento a un report ospitato in un sito di SharePoint.
  
-   **Parametri**: Visualizza o nasconde l'area dei parametri sulla barra degli strumenti. Se si imposta questo parametro su **true**, viene visualizzata l'area dei parametri sulla barra degli strumenti. Se si imposta questo parametro su **false**, l'area dei parametri non viene visualizzata e non può essere visualizzata dall'utente. Se si imposta questo parametro sul valore **Collapsed**, l'area dei parametri non viene visualizzata, ma può essere visualizzata o nascosta dall'utente. Il valore predefinito di questo parametro è **true**.  
  
     Ad esempio, in modalità nativa:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Parameters=Collapsed  
    ```  
  
     Ad esempio, in modalità SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Parameters=Collapsed  
    ```  
  
-   **Zoom**: Imposta il valore di zoom del report come percentuale con valore intero o come costante di stringa. I valori stringa standard comprendono **Page Width** e **Whole Page**. Questo parametro viene ignorato dalle versioni di Internet Explorer precedenti a Internet Explorer 5.0 e da tutti i browser non[!INCLUDE[msCoName](../includes/msconame-md.md)] . Il valore predefinito di questo parametro è **100**.
  
     Ad esempio, in modalità nativa:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Zoom=Page Width  
    ```  
  
     Ad esempio, in modalità SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Zoom=Page Width  
    ```  
  
-   **Section**: Imposta la pagina del report da visualizzare. Se il valore è superiore al numero di pagine nel report viene visualizzata l'ultima pagina. Se il valore è inferiore a **0** viene visualizzata la pagina 1 del report. Il valore predefinito di questo parametro è **1**.
  
     Ad esempio, per visualizzare la pagina 2 del report in modalità nativa:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:Section=2  
    ```  
  
     Ad esempio, per visualizzare la pagina 2 del report in modalità SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:Section=2  
    ```  
  
-   **FindString**: Individuare un set di testo specifico in un report.
  
     Ad esempio, in modalità nativa:
  
    ```  
    https://myrshost/reportserver?/Sales&rc:FindString=Mountain-400  
    ```  
  
     Ad esempio, in modalità SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rc:FindString=Mountain-400  
    ```  
  
-   **StartFind**: Specifica l'ultima sezione in cui cercare. Il valore predefinito di questo parametro è l'ultima pagina del report.  
  
     Per un esempio in modalità nativa in cui viene cercata la prima occorrenza del testo "Mountain-400" nel report di esempio Product Catalog a partire da pagina 1 fino a pagina 5:
  
    ```  
    https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
    ```  
  
-   **EndFind**: Imposta il numero dell'ultima pagina da utilizzare nella ricerca. Ad esempio, il valore **5** indica che l'ultima pagina in cui cercare è la pagina 5 del report. Il valore predefinito è il numero della pagina corrente. Utilizzare questo parametro con il parametro *StartFind* . Vedere l'esempio precedente.
  
-   **FallbackPage**: Imposta il numero della pagina da visualizzare se si verifica un errore durante una ricerca o la selezione di una mappa documento. Il valore predefinito è il numero della pagina corrente.
  
-   **GetImage**: Ottiene una determinata icona per l'interfaccia utente del visualizzatore HTML.
  
-   **Icon**: Ottiene l'icona di una determinata estensione per il rendering.
  
-   **Foglio di stile**: Consente di specificare un foglio di stile da applicare al visualizzatore HTML.
  
-   **Impostazione relativa alle informazioni sul dispositivo**: Specifica un'impostazione relativa alle informazioni sul dispositivo nel formato `rc:tag=value`, dove *tag* è il nome di un'impostazione relativa alle informazioni sul dispositivo specifica dell'estensione per il rendering attualmente usata. (Vedere la descrizione del parametro *Format*.) Ad esempio, è possibile usare l'impostazione relativa alle informazioni sul dispositivo *OutputFormat* in modo tale che l'estensione per il rendering IMAGE esegua il rendering del report in un'immagine JPEG usando i parametri seguenti nella stringa di accesso con URL: `...&rs:Format=IMAGE&rc:OutputFormat=JPEG`. Per altre informazioni sulle impostazioni relative alle informazioni sul dispositivo specifiche per l'estensione, vedere [Impostazioni relative alle informazioni sul dispositivo per le estensioni per il rendering &#40;Reporting Services&#41;](../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md).
  
##  <a name="report-server-commands-rs"></a><a name="bkmk_reportserver"></a> Comandi del server di report (rs:)
 I comandi del server di report hanno il prefisso *rs:* e vengono usati sul server di report:
  
-   **Comando**: Esegue un'azione su un elemento del catalogo, a seconda del tipo di elemento. Il valore predefinito è determinato dal tipo dell'elemento del catalogo a cui viene fatto riferimento nella stringa di accesso con URL. I valori validi sono:
  
    -   **ListChildren** e **GetChildren**: consentono di visualizzare il contenuto di una cartella. Gli elementi della cartella sono visualizzati in una pagina generica di navigazione degli elementi.
  
         Ad esempio, in modalità nativa:
  
        ```  
        https://myrshost/reportserver?/Sales&rs:Command=GetChildren  
        ```  
  
         Ad esempio, un'istanza denominata in modalità nativa:
  
        ```  
        https://myssrshost/Reportserver_THESQLINSTANCE?/reportfolder&rs:Command=listChildren  
        ```  
  
         Ad esempio, in modalità SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales&rs:Command=GetChildren  
        ```  
  
    -   **Render**: il rendering del report viene eseguito nel browser, per consentire la visualizzazione del report.
  
         Ad esempio, in modalità nativa:
  
        ```  
        https://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
         Ad esempio, in modalità SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render  
        ```  
  
    -   **GetSharedDatasetDefinition**: consente di visualizzare la definizione XML associata a un set di dati condiviso. Le proprietà dei set di dati condivisi, che includono query, parametri del set di dati, valori predefiniti, filtri del set di dati e opzioni dei dati, ad esempio regole di confronto e distinzione tra maiuscole e minuscole, vengono salvate nella definizione. Per utilizzare questo valore, è necessario disporre dell'autorizzazione per la **lettura delle definizioni dei report** su un set di dati condiviso.
  
         Ad esempio, in modalità nativa:
  
        ```  
        https://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
        ```  
  
    -   **GetDataSourceContents**: consente di visualizzare le proprietà di una determinata origine dati condivisa come XML. Se il browser supporta XML e se l'utente autenticato ha l'autorizzazione **Read Contents** per l'origine dati, viene visualizzata l'origine dati.
  
         Ad esempio, in modalità nativa:
  
        ```  
        https://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
         Ad esempio, in modalità SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents  
        ```  
  
    -   **GetResourceContents**: viene eseguito il rendering di una risorsa che viene visualizzata in una pagina HTML, se la risorsa è compatibile con il browser. In caso contrario, viene chiesto di aprire oppure salvare il file o la risorsa su disco.  
  
         Ad esempio, in modalità nativa:
  
        ```  
        https://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents  
        ```  
  
         Ad esempio, in modalità SharePoint:
  
        ```  
        https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents  
        ```  
  
    -   **GetComponentDefinition**: consente di visualizzare la definizione XML associata a un elemento del report pubblicato. Per utilizzare questo valore, è necessario disporre dell'autorizzazione per la **lettura del contenuto** per un elemento del report pubblicato.
  
-   **Format**: Specifica il formato da usare per il rendering e la visualizzazione di un report. Valori comuni:
  
    -   **HTML5**  
  
    -   **PPTX**  
  
    -   **ATOM**  
  
    -   **HTML4.0**  
  
    -   **MHTML**  
  
    -   **IMAGE**  
  
    -   **EXCEL** (per l'estensione xls)
    
    -   **EXCELOPENXML** (per l'estensione xlsx)
  
    -   **WORD** (per l'estensione doc)
    
    -   **WORDOPENXML** (per l'estensione docx)
  
    -   **CSV**  
  
    -   **PDF**  
  
    -   **XML**  
  
     Il valore predefinito è **HTML5**. Per altre informazioni, vedere [Esportare un report tramite l'accesso con URL](../reporting-services/export-a-report-using-url-access.md).
  
     Per l'elenco completo, vedere la sezione relativa all'estensione **\<Render>** del file rsreportserver.config del server di report. Per informazioni su dove trovare il file, vedere [File di configurazione RsReportServer.config](../reporting-services/report-server/rsreportserver-config-configuration-file.md).
  
     Ad esempio per ottenere una copia PDF di un report direttamente da un server di report in modalità nativa:
  
    ```  
    https://myrshost/ReportServer?/myreport&rs:Format=PDF  
    ```  
  
     Ad esempio, per ottenere una copia PDF di un report direttamente da un server di report in modalità SharePoint:
  
    ```  
    https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
    ```  
  
-   **ParameterLanguage**: specifica una lingua indipendente dalla lingua del browser per i parametri passati in un URL. Il valore predefinito è la lingua del browser. Il valoe può essere un valoe di impostazioni cultura, ad esempio **it-IT** o **en-US**.
  
     Ad esempio, in modalità nativa, per ignorare la lingua del browser e specificare il valore di impostazioni cultura de-DE:
  
    ```  
    https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
    ```  
  
-   **Snapshot**: Esegue il rendering di un report in base a uno snapshot della cronologia del report. Per altre informazioni, vedere [Eseguire il rendering degli snapshot della cronologia dei report tramite l'accesso con URL](../reporting-services/render-a-report-history-snapshot-using-url-access.md).
  
     Ad esempio, in modalità nativa, per recuperare uno snapshot della cronologia del report datato 2003-04-07 con un timestamp 13.40.02:
  
    ```  
    https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
    ```  
  
-   **PersistStreams**: Esegue il rendering di un report in un solo flusso persistente. Questo parametro viene utilizzato dal renderer di immagini per trasmettere il report visualizzabile un blocco alla volta. Dopo avere utilizzato il parametro in una stringa di accesso URL, utilizzare la stessa stringa di accesso con URL, sostituendo il parametro *GetNextStream* con il parametro *PersistStreams* per ottenere il blocco successivo nel flusso persistente. È possibile che questo comando dell'URL restituisca un flusso di 0 byte per indicare la fine del flusso persistente. Il valore predefinito è **false**.
  
-   **GetNextStream**: ottiene il blocco di dati successivo in un flusso persistente al quale è possibile accedere tramite il parametro *PersistStreams*. Per ulteriori informazioni, vedere la descrizione relativa a *PersistStreams*. Il valore predefinito è **false**.
  
-   **SessionID**: Specifica una sessione di report attiva stabilita tra l'applicazione client e il server di report. Il valore di questo parametro viene impostato sull'identificatore della sessione.
  
     È possibile specificare l'ID di sessione come cookie o come parte dell'URL. Nel caso in cui il server di report sia stato configurato per non utilizzare i cookie di sessione, la prima richiesta senza un ID di sessione specificato comporta un reindirizzamento con un ID di sessione. Per altre informazioni sulle sessioni del server di report, vedere [Identificazione dello stato di esecuzione](../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).
  
-   **ClearSession**: Il valore **true** indica al server di report di rimuovere un report dalla sessione di report. Tutte le istanze del report associate a un utente autenticato vengono rimosse dalla sessione di report. Un'istanza di un report viene definita quando lo stesso report viene eseguito più volte con valori dei parametri del report diversi. Il valore predefinito è **false**.
  
-   **ResetSession**: Il valore **true** richiede al server di report di reimpostare la sessione del report rimuovendone l'associazione a tutti gli snapshot del report. Il valore predefinito è **false**.
  
-   **ShowHideToggle**: Visualizza o nasconde una sezione del report. Specificare un integer positivo per rappresentare la sezione da attivare o disattivare.
  
##  <a name="report-viewer-web-part-commands-rv"></a><a name="bkmk_webpart"></a> Comandi Web part del visualizzatore di report (rv:)
 I seguenti nomi dei parametri di report riservati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono usati per individuare la web part Visualizzatore di report integrata con SharePoint. Questi nomi di parametro sono preceduti dal prefisso *rv:* . La web part Visualizzatore di report accetta inoltre il parametro *rs:ParameterLanguage*.
  
-   **Barra degli strumenti**: determina la visualizzazione della barra degli strumenti per la web part Visualizzatore di report. Il valore predefinito è **Full**. I valori possibili sono:
  
    -   **Full**: visualizza la barra degli strumenti completa.
  
    -   **Navigation**: visualizza solo la paginazione nella barra degli strumenti.
  
    -   **Nessuna**: non visualizza la barra degli strumenti.
  
     Ad esempio, in modalità SharePoint, per visualizzare solo la paginazione nella barra degli strumenti:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation  
    ```  
  
-   **HeaderArea**: determina la visualizzazione dell'intestazione per la web part Visualizzatore di report. Il valore predefinito è **Full**. I valori possibili sono:
  
    -   **Full**: visualizza l'intestazione completa.
  
    -   **BreadCrumbsOnly**: visualizza solo il percorso di navigazione nell'intestazione per segnalare all'utente la relativa posizione nell'applicazione.
  
    -   **Nessuna**: non visualizza l'intestazione.
  
     Ad esempio, in modalità SharePoint, per visualizzare solo il percorso di navigazione nell'intestazione:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly  
    ```  
  
-   **DocMapAreaWidth**: determina la larghezza di visualizzazione, in pixel, dell'area dei parametri nella web part Visualizzatore di report. Il valore predefinito è uguale a quello della web part Visualizzatore di report. Deve essere un valore intero non negativo.
  
-   **AsyncRender**: Determina se il rendering di un report viene eseguito in modo asincrono. Il valore predefinito è **true**con cui si specifica che il rendering di un report viene eseguito in modo asincrono. Deve essere un valore booleano **true** o **false**.
  
-   **ParamMode**: determina come appare l'area dei messaggi di richiesta del parametro della web part Visualizzatore di report nella visualizzazione Pagina intera. Il valore predefinito è **Full**. I valori validi sono:
  
    -   **Full**: visualizza l'area dei messaggi di richiesta del parametro.
  
    -   **Collapsed**: comprime l'area dei messaggi di richiesta del parametro.
  
    -   **Hidden**: nasconde l'area dei messaggi di richiesta del parametro.
  
     Ad esempio, in modalità SharePoint , per comprimere l'area dei messaggi di richiesta del parametro:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed  
    ```  
  
-   **DocMapMode**: determina come appare l'area mappa documento della web part Visualizzatore di report nella visualizzazione Pagina intera. Il valore predefinito è **Full**. I valori validi sono:
  
    -   **Full**: visualizza l'area mappa documento.
  
    -   **Collapsed**: comprime l'area mappa documento.
  
    -   **Hidden**: nasconde l'area mappa documento.
  
-   **DockToolBar**: determina se la barra degli strumenti della web part Visualizzatore di report è ancorata alla parte superiore o inferiore. I valori validi sono **Top** e **Bottom**. Il valore predefinito è **Top**.
  
     Ad esempio, in modalità SharePoint, per ancorare la barra degli strumenti alla parte inferiore:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom  
    ```  
  
-   **ToolBarItemsDisplayMode**: Determina gli elementi della barra degli strumenti che vengono visualizzati. Si tratta di un valore di enumerazione bit per bit. Per includere un elemento della barra degli strumenti, aggiungere il valore dell'elemento al valore totale. Ad esempio, per non visualizzare il menu **Azioni**, usare *rv:ToolBarItemsDisplayMode=63* (or 0x3F), ovvero 1+2+4+8+16+32. Per visualizzare solo le voci del menu **Azioni**, usare *rv:ToolBarItemsDisplayMode=960* (or 0x3C0). Il valore predefinito è **-1**che include tutti gli elementi della barra degli strumenti. I valori validi sono:
  
    -   **1 (0x1)** : pulsante **Indietro**  
  
    -   **2 (0x2)** : controlli di ricerca del testo  
  
    -   **4 (0x4)** : controlli per gli spostamenti tra le pagine  
  
    -   **8 (0x8)** : pulsante **Aggiorna**  
  
    -   **16 (0x10)** : casella di riepilogo **Zoom**  
  
    -   **32 (0x20)** : pulsante **Feed Atom**  
  
    -   **64 (0x40)** : opzione **Stampa** del menu **Azioni**  
  
    -   **128 (0x80)** : sottomenu **Esporta** del menu **Azioni**  
  
    -   **256 (0x100)** : opzione di menu **Apri con Generatore report** del menu **Azioni**  
  
    -   **512 (0x200)** : Opzione **Sottoscrivi** del menu **Azioni**  
  
    -   **1024 (0x400)** : Opzione **Nuovo avviso dati** del menu **Azioni**  
  
     Ad esempio in modalità SharePoint per visualizzare solo il pulsante **Indietro**, i controlli di ricerca del testo, i controlli per gli spostamenti tra le pagine e il pulsante **Aggiorna**:
  
    ```  
    https://myspsite/_vti_bin/reportserver?https://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15  
    ```  
  
## <a name="see-also"></a>Vedere anche
 - [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)
 - [Esportare un report tramite l'accesso con URL](../reporting-services/export-a-report-using-url-access.md)
  
  
