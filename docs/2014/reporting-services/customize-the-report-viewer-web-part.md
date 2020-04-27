---
title: Personalizzare la Web part Visualizzatore report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- Report Viewer Web Part [Reporting Services]
ms.assetid: 086d6546-7299-41bc-bca9-083a15a53679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 73fd65c8770d6e0c25232d727d56529910edc6cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109536"
---
# <a name="customize-the-report-viewer-web-part"></a>Personalizzare la web part Visualizzatore report
  È possibile utilizzare la web part Visualizzatore report per visualizzare report eseguiti in un server di report configurato per l'integrazione con SharePoint. I report che è possibile visualizzare includo file di definizione dei report, con estensione rdl, e report di Generatore report. I report vengono automaticamente aperti nella web part Visualizzatore report in una nuova pagina, tuttavia è possibile aggiungere la web part Visualizzatore report a una pagina Web o a un sito esistente se si desidera che il report risulti sempre visibile all'interno della pagina.  
  
 È possibile personalizzare la web part Visualizzatore report nei modi seguenti:  
  
-   Modificare l'aspetto della web part impostandone le proprietà.  
  
-   Scegliere le caratteristiche di report interattive disponibili sull'apposita barra degli strumenti.  
  
-   Specificare quali aree di visualizzazione rendere disponibili. La web part Visualizzatore report dispone di un'area di visualizzazione dei report, di un'area Parametri e di un'area Credenziali.  
  
 Non è possibile estendere la web part Visualizzatore report per supportare altri tipi di file, né sostituire la barra degli strumenti per report con una barra personalizzata o aggiungervi nuove funzionalità. Per personalizzare le caratteristiche standard, è necessario creare una web part personalizzata.  
  
## <a name="setting-web-part-properties"></a>Impostazione delle proprietà della web part  
 A una web part sono associate proprietà personalizzate utilizzate per configurare funzionalità specifiche. Le web part dispongono inoltre in genere di proprietà comuni a tutte le web part.  
  
### <a name="change-default-properties"></a>Modifica delle proprietà predefinite  
 La web part Visualizzatore report include proprietà predefinite idealmente adeguate per l'apertura di report a richiesta da una raccolta o cartella. Per impostazione predefinita, tutti i controlli disponibili si trovano sulla barra degli strumenti, mentre l'altezza e la larghezza vengono impostate per utilizzare tutto lo spazio disponibile nella pagina Web. Se si desidera modificare le proprietà predefinite, è possibile personalizzare la Web part tramite **Impostazioni sito**.  
  
1.  Scegliere **Impostazioni sito** dal menu **Azioni sito**.  
  
2.  In raccolte fare clic su **Web part**.  
  
3.  Fare clic su **ReportViewer.dwp**.  
  
4.  Aprire il riquadro degli strumenti e impostare le proprietà che si desidera utilizzare.  
  
### <a name="customize-an-embedded-report-viewer-in-a-web-page"></a>Personalizzazione di un visualizzatore report incorporato in una pagina Web  
 È possibile impostare le proprietà affinché Visualizzatore report si adatti alla pagina Web. Al visualizzatore possono essere applicati lo stesso stile e gli stessi colori della pagina che lo contiene. È possibile nascondere completamente o in parte la barra degli strumenti, la mappa documento e l'area dei parametri per sfruttare al massimo l'area di visualizzazione del report all'interno dello spazio assegnato. Il report utilizza sempre gli stili definiti al momento della sua creazione. Non è possibile personalizzare l'aspetto del report dopo la pubblicazione in una raccolta di SharePoint.  
  
 Se si incorpora la Web part Visualizzatore report in una pagina Web, è necessario impostare la proprietà **URL report** su un report specifico. In caso contrario, nel Visualizzatore report verranno visualizzate le istruzioni per il collegamento di un report. Non è possibile personalizzare o rimuovere le istruzioni.  
  
### <a name="custom-properties-of-the-report-viewer-web-part"></a>Proprietà personalizzate della web part Visualizzatore report  
 Ai fini dell'impostazione delle proprietà personalizzate, tenere presente che alcune di esse vengono utilizzate solo se la web part Visualizzatore report è incorporata in una pagina. Tra le proprietà personalizzabili ci sono il titolo, l'altezza, la larghezza, il tipo di colore e la zona. Altre proprietà, ad esempio le impostazioni relative alla barra degli strumenti e le impostazioni relative ai parametri, vengono utilizzate indipendentemente dal fatto che Visualizzatore report sia incorporato in una pagina o apra un report in modalità Pagina intera.  
  
 Le proprietà personalizzate della web part Visualizzatore report sono elencate di seguito.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|Report|Percorso completo di un report presente nel sito di SharePoint corrente oppure in un sito disponibile nella stessa farm o applicazione Web. Se si desidera impostare proprietà aggiuntive, per ottenere risultati ottimali fare clic su Applica dopo avere specificato l'URL del report.|  
|Destinazione collegamento ipertestuale|Codice HTML standard che specifica il frame di destinazione per la visualizzazione dei contenuti collegati nel documento corrente. Per i report che includono collegamenti ipertestuali a siti Web esterni, è possibile specificare se un documento di destinazione sostituisce il report esistente nella finestra corrente oppure viene aperto in una nuova finestra del browser. I valori validi includono `_Top`, `_Blank` e `_Self`. `_Top` utilizza la finestra corrente, `_Blank` carica il documento in una nuova finestra del browser e `_Self` apre il documento nel frame corrente. Anche se nel linguaggio HTML `_Parent` è un valore valido per l'attributo Target, non utilizzare tale valore per una web part Visualizzatore report incorporata in una pagina.|  
|Titolo web part generato automaticamente|Titolo generato che include il nome della web part Visualizzatore report seguito dal nome del report, separati da un trattino. Se il report non ha titolo, verrà utilizzato il nome di file del report. Tale titolo è visibile quando si aggiunge una web part a una pagina. Se questa casella di controllo è selezionata, il titolo verrà generato a ogni aggiornamento della pagina.|  
|Collegamento Dettagli per il titolo della web part generato automaticamente|Collegamento ipertestuale generato automaticamente e visualizzato sopra la web part. È possibile fare clic sul collegamento per aprire il report in una nuova pagina, in modalità Pagina intera.|  
|Mostra voce di menu Generatore report|Visualizza o nasconde l'opzione del menu **Azioni** che consente di aprire Generatore report.|  
|Mostra voce di menu di sottoscrizione|Visualizza o nasconde l'opzione del menu **Azioni** che consente di creare una sottoscrizione per il report.|  
|Mostra voce di menu di stampa|Visualizza o nasconde l'opzione del menu **Azioni** che consente di stampare il report.|  
|Mostra voce di menu di esportazione|Visualizza o nasconde l'opzione del menu **Azioni** che consente di esportare il report.|  
|Mostra pulsante di aggiornamento|Visualizza o nasconde il pulsante di aggiornamento sulla barra degli strumenti.|  
|Mostra controlli per la navigazione tra le pagine|Visualizza o nasconde i pulsanti per la navigazione nel report sulla barra degli strumenti. Questa opzione consente di modificare la visibilità di tutti i controlli per la navigazione.|  
|Mostra pulsante Indietro|Visualizza o nasconde il pulsante Indietro sulla barra degli strumenti.|  
|Mostra controlli di ricerca|Visualizza o nasconde i controlli di ricerca sulla barra degli strumenti. I controlli di ricerca consentono a un utente di cercare testo nel report di cui è stato eseguito il rendering. Questa opzione consente di modificare la visibilità di tutti i controlli di ricerca.|  
|Mostra controllo zoom|Visualizza o nasconde il controllo zoom sulla barra degli strumenti.|  
|Mostra pulsante feed ATOM|Visualizza o nasconde il pulsante del feed ATOM sulla barra degli strumenti.<br /><br /> ![htmlviewer_datafeed](media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|  
|Posizione barra degli strumenti|Determina la posizione della barra degli strumenti all'interno del visualizzatore di report. I valori validi includono `Top` e `Bottom`.|  
|Area dei messaggi di richiesta|I valori validi includono `Displayed`, `Collapsed` e `Hidden`. `Displayed` consente di visualizzare l'area Parametri per i report che includono valori con parametri e richiedono l'input dell'utente prima dell'esecuzione. Utilizzare `Hidden` se tutti i parametri del report sono specificati e non si desidera visualizzare l'area relativa.|  
|Larghezza area parametri|È possibile specificare l'unità di misura e il valore. Il valore predefinito è 200 pixel. L'unico requisito per questa proprietà è che il valore sia maggiore di zero.|  
|Mappa documento|Controllo per la navigazione del report che viene definito nel report e consente di accedere con un clic a sezioni specifiche del report. È disponibile nei report HTML. La mappa documento è visualizzata in un'area comprimibile accanto all'area di visualizzazione del report. I valori validi includono `Displayed`, `Collapsed` e `Hidden`. Se per un determinato report è definita una mappa documento, quest'area verrà espansa per impostazione predefinita, a meno che non sia contrassegnata come nascosta o compressa nelle proprietà della web part. Se la mappa documento è compressa, sarà possibile fare clic sulla freccia per espanderla.|  
|Larghezza area mappa documento|È possibile specificare l'unità di misura e il valore. Il valore predefinito è 200 pixel. L'unico requisito per questa proprietà è che il valore sia maggiore di zero.|  
|Carica parametri|Consente di recuperare le proprietà dei parametri per il report. Non tutti i report utilizzano parametri. Se il report non dispone di parametri, non verrà restituito alcun valore. Mentre si impostano le proprietà per un report appena caricato, è possibile che venga visualizzato un errore per segnalare che la connessione all'origine dei dati è stata eliminata. In questo caso, reimpostare la connessione e quindi completare l'impostazione delle proprietà dei parametri, dopo aver specificato la connessione. Per altre informazioni sull'impostazione della connessione, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).<br /><br /> Per ottenere risultati ottimali, fare clic su **Applica** prima di fare clic su Carica parametri.<br /><br /> Dopo il caricamento delle proprietà dei parametri, è possibile impostarle come avviene normalmente nella pagina delle proprietà dei parametri del report. Per altre informazioni sull'impostazione dei parametri, vedere [Impostare i parametri per un report pubblicato &#40;Reporting Services in modalità integrata SharePoint&#41;](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).|  
  
## <a name="customizing-the-toolbar"></a>Personalizzazione della barra degli strumenti  
 La barra degli strumenti è visualizzata sotto il titolo e si estende nella parte superiore del report. Include il menu **Azioni** , oltre a controlli per la navigazione dei report impaginati, l'aggiornamento e lo zoom. È disponibile anche un controllo mappa documento per i report che dispongono di una mappa documento. Nel menu **Azioni** sono disponibili comandi per l'esportazione del report, la ricerca di testo o numeri nel report, la stampa del report e l'apertura del report in Generatore report.  
  
 Non è possibile aggiungere nuovi comandi al menu  **Azioni** , ma è possibile personalizzare il menu modificando le opzioni visibili agli utenti. Per modificare la visibilità dei pulsanti e dei controlli della barra degli strumenti, è possibile modificare le opzioni nella sezione **visibilità degli elementi della barra** degli strumenti della web part. È inoltre possibile rimuovere il comando **Stampa** o formati di esportazione specifici, rendendo non disponibili tali caratteristiche sul server di report. I controlli per la navigazione tra le pagine sono disponibili solo per i report che includono interruzioni di pagina. In caso contrario il report è costituito da una singola pagina di lunghezza variabile. Il pulsante**Aggiorna** consente di rielaborare il report usando i parametri correnti. Per visualizzare tutti i controlli su una riga, impostare la larghezza complessiva della web part su almeno 400 pixel.  
  
## <a name="customizing-the-viewing-area"></a>Personalizzazione dell'area di visualizzazione  
 L'area di visualizzazione viene utilizzata per la visualizzazione dei report ed è condivisa con le aree Parametri e Credenziali, se vengono utilizzate. Se è necessario immettere credenziali, verrà visualizzata un'area di visualizzazione report vuota con accanto l'area Credenziali. Tale area viene chiusa dopo l'immissione delle credenziali e l'avvio del report. Il testo visualizzato per richiedere l'impostazione delle credenziali può essere personalizzato modificando le proprietà di connessione all'origine dei dati. Per altre informazioni, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
 L'area Parametri contiene alcuni campi in cui è possibile immettere valori prima dell'esecuzione del report e viene utilizzata solo se la definizione del report include parametri. Se è visualizzata l'area Parametri o l'area Credenziali, le dimensioni dell'area di visualizzazione del report verranno modificate in modo da utilizzare la parte rimanente della web part. È possibile personalizzare la larghezza dell'area Parametri impostando le proprietà della web part. È inoltre possibile specificare le etichette da visualizzare accanto ai singoli parametri della pagina. Per altre informazioni sulla modifica dei parametri, vedere [Impostare i parametri per un report pubblicato &#40;Reporting Services in modalità integrata SharePoint&#41;](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Web part Visualizzatore report in un sito di SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Aggiungere la web part Visualizzatore report a una pagina Web &#40;Reporting Services in modalità integrata SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
