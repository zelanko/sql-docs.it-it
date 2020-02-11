---
title: Web part Visualizzatore report in un sito di SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: b6341a73-172f-4632-a9e9-cc79fed3f36b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ba8b23c800718d289b2a7a633d5244261b5ab8a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103044"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>Web part Visualizzatore report in un sito di SharePoint
  La web part Visualizzatore report è una web part personalizzata installata con il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per prodotti SharePoint. È possibile utilizzare questa web part per visualizzare, esplorare, stampare ed esportare report in un server di report configurato per l'esecuzione in modalità integrata SharePoint. La Web part Visualizzatore report è associata ai file di definizione del report (con estensione rdl) elaborati [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] da un server di report. Non è possibile utilizzarla con altri documenti di report creati con altri prodotti software.  
  
 Per installare la web part, è necessario eseguire il programma di installazione per il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . La Web part non deve essere installata in modo indipendente, poiché è inclusa nel componente aggiuntivo e può essere installata solo tramite il programma di installazione di quest'ultimo. Il nome di file della web part Visualizzatore report è ReportViewer.dwp. Il file si trova nella cartella Programmi\File comuni\Microsoft Shared\Web Server Extensions\12\template\features\reportserver. Il file non deve essere spostato in altre cartelle.  
  
 Per utilizzare la web part, è necessario che nel sistema sia installato e configurato il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e che il server di report sia configurato per l'integrazione con SharePoint. È inoltre necessario disporre di alcuni report da mostrare nel visualizzatore. Possono essere visualizzati solo report che si trovano in una raccolta, in una cartella all'interno di una raccolta o nella cronologia di un report oppure che sono collegati da una web part Raccolta a una web part Visualizzatore report. Non è possibile aprire report salvati come allegati a un elemento in un elenco personalizzato.  
  
 Impostando le proprietà della web part Visualizzatore report è possibile controllare l'aspetto della barra degli strumenti e delle aree di visualizzazione, nonché collegare la web part a un report specifico. Il Visualizzatore report può essere utilizzato per visualizzare un report esplicitamente collegato alla web part o qualsiasi file con estensione rdl aperto.  
  
 Non è possibile collegare più report a una singola istanza del Visualizzatore report, tuttavia se si desidera raggruppare i report, è possibile creare un dashboard o una pagina web part per incorporarvi più istanze della web part Visualizzatore report.  
  
 La web part include un'area di visualizzazione, una barra degli strumenti, proprietà e un'area comprimibile per l'impostazione di credenziali e parametri. Nell'immagine seguente viene illustrata la web part con un report di esempio relativo alle vendite e le opzioni di esportazione selezionabili dalla barra degli strumenti.  
  
 ![Web part di Visualizzatore report](media/rs-sharepointrvwebpart.gif "Web part di Visualizzatore report")  
  
## <a name="web-part-components"></a>Componenti della web part  
 Nell'area di visualizzazione viene visualizzato il report in formato HTML. A seconda della configurazione della web part, l'area di visualizzazione può essere ingrandita, in modo da visualizzare il report in modalità Pagina intera, oppure condividere lo spazio disponibile con due riquadri adiacenti e una barra degli strumenti.  
  
 La barra degli strumenti include caratteristiche per la navigazione tra le pagine, la ricerca, lo zoom e l'esportazione, per consentire all'utente di visualizzare i report in un altro formato di applicazione. Include inoltre una funzionalità di stampa facoltativa che consente di generare un output di stampa impaginato per i report HTML, oltre che di modificare il layout della pagina e le impostazioni dei margini. **Apri con Generatore report, Sottoscrivi**, **Esporta**e **stampa** sono disponibili nel menu **azioni** sulla barra degli strumenti. mentre i controlli per la navigazione tra le pagine e lo zoom sono disponibili direttamente sulla barra degli strumenti.  
  
> [!NOTE]  
>  La barra degli strumenti non può essere personalizzata a meno che non si scriva codice apposito, ma è possibile impostare alcune proprietà per nascondere tutti o parte dei controlli.  
  
### <a name="export-action-on-the-report-toolbar"></a>Azione Esporta sulla barra degli strumenti Report  
 **Esporta** nel menu **azioni** Visualizza i formati di applicazione associati alle estensioni per il rendering distribuite in un server di report. Per determinare la disponibilità di un formato specifico, è possibile aggiungere o rimuovere un'estensione per il rendering sul server di report oppure modificare le impostazioni di configurazione in modo da rimuovere un particolare formato di esportazione dall'elenco. Per controllare i formati disponibili, è inoltre possibile specificare impostazioni di configurazione sul server di report. È possibile modificare il comportamento predefinito di un formato specifico aggiungendo e modificando le impostazioni di configurazione per la corrispondente estensione per il rendering.  
  
### <a name="print-action-on-the-report-toolbar"></a>Azione Stampa sulla barra degli strumenti Report  
 **Stampa** nel menu **azioni** è una funzionalità di stampa personalizzata fornita tramite [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Quando si fa clic su **Stampa**, sul computer client viene scaricato un controllo ActiveX di stampa per il lato client. Nella maggior parte dei casi l'utente che fa clic su **Stampa** deve disporre di autorizzazioni di amministratore sul computer locale, poiché in genere il download dei controlli ActiveX viene consentito solo agli utenti con autorizzazioni di amministratore. È possibile utilizzare Amministrazione centrale SharePoint per abilitare o disabilitare il download del controllo di stampa lato client.  
  
### <a name="find-action-on-the-report-toolbar"></a>Azione Trova sulla barra degli strumenti del report  
 **Trova** nel menu **azioni** consente di spostarsi in una posizione di destinazione nel report. È possibile ricercare contenuto in un report digitando la parola o la frase che si desidera trovare. Il numero massimo di caratteri del termine di ricerca è 256. Quando viene trovato un valore corrispondente nel report, la visualizzazione del report viene spostata sulla sezione che lo contiene.  
  
 Il valore su cui si desidera basare la ricerca deve essere digitato esattamente come si prevede che sia presente nel report. Non immettere domande, ad esempio "qual è il profitto medio per questo mese?", a meno che non si supponga che tutte le parole della frase siano presenti nel report.  
  
 È possibile ricercare un solo termine o valore alla volta. Non è possibile utilizzare operatori di ricerca, ad esempio `AND` o `OR`, o simboli e caratteri jolly. Non è possibile eseguire ricerche incrociate su uno specifico insieme di dati, ad esempio la ricerca delle vendite nette di un particolare prodotto per un mese specifico. Per eseguire analisi di questo tipo, creare report click-through tramite Generatore report.  
  
 Le impostazioni di sicurezza del modello e del database che limitano l'accesso ai dati del report vengono applicate anche alle operazioni di ricerca. Se si ricerca un valore in un report click-through che utilizza un modello come origine dei dati, ma non si ha accesso a parte del modello, i dati corrispondenti a tale parte del modello verranno esclusi dalla ricerca.  
  
### <a name="panes-for-specifying-credentials-and-parameters"></a>Riquadri per specificare credenziali e parametri  
 Le **credenziali** e i **parametri** sono riquadri visualizzati accanto all'area di visualizzazione. Le **credenziali** vengono visualizzate quando la connessione all'origine dati per il report è configurata in modo da richiedere all'utente un account e una password con diritti di accesso all'origine dati. **Parameters** viene visualizzato quando il report accetta l'input dell'utente per i parametri definiti nel report.  
  
### <a name="setting-properties-on-the-report-viewer-web-part"></a>Impostazione delle proprietà nella web part Visualizzatore report  
 Le proprietà della web part includono proprietà personalizzate specifiche e proprietà generali valide per qualsiasi web part. Per altre informazioni, vedere [Personalizzare la web part Visualizzatore report](../../2014/reporting-services/customize-the-report-viewer-web-part.md).  
  
 Per impostazione predefinita, i report vengono aperti in modalità Pagina intera. In tale modalità viene visualizzata la barra degli strumenti, che fornisce i controlli per navigazione tra le pagine, la ricerca e altre funzionalità. È possibile personalizzare la web part per modificarne l'aspetto o il comportamento predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Aggiungere la web part Visualizzatore report a una pagina Web &#40;Reporting Services in modalità integrata SharePoint&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
