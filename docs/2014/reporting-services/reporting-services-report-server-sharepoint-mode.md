---
title: Server di report di Reporting Services (modalità SharePoint) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: c89596d916f9a8ec2fea91cdea8f72b1958c5b6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102831"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Server di report di Reporting Services (modalità SharePoint)

Un server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] configurato per la **modalità SharePoint** può essere eseguito all'interno di una distribuzione di un prodotto SharePoint. Tramite un server di report in modalità SharePoint è possibile utilizzare le funzionalità di collaborazione e gestione di SharePoint per report e altri tipi di contenuto di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . La modalità SharePoint richiede l'installazione della versione appropriata del componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per prodotti SharePoint nei front-end Web di SharePoint.  
  
Per ulteriori informazioni sull'installazione e sulla configurazione, vedere quanto riportato di seguito:  
  
- [Installare Reporting Services SharePoint Mode for SharePoint 2013](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
- [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
- [Aggiungere un ulteriore Server di Report a una Farm di &#40;scalabilità orizzontale SSRS&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
 Per informazioni sulle novità in questa versione, vedere la sezione "SharePoint" nella [What ' s New &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md).  
  
 **Contenuto dell'argomento:**  
  
-   [Riepilogo delle funzionalità](#bkmk_featuresum)  
  
-   [Modalità con connessione e modalità locale](#bkmk_connectedandlocal)  
  
-   [Funzionalità di SharePoint non supportate](#bkmk_unsupportedsharepoint)  
  
-   [Combinazioni supportate del componente aggiuntivo di SharePoint e del server di report](#bkmk_supportedcombinations)  
  
-   [Componenti utilizzati per l'integrazione](#bkmk_components)  
  
-   [Considerazioni sul linguaggio](#bkmk_language)  
  
-   [Attività correlate](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> Riepilogo delle funzionalità

 Quando si configura un server di report per l'esecuzione in modalità integrata SharePoint vengono aggiunte le funzionalità seguenti, che sono disponibili solo quando si distribuisce un server di report in tale modalità:  
  
-   Funzionalità di gestione dei documenti e collaborazione di SharePoint, inclusi avvisi. Un sito di SharePoint costituisce un portale unificato per l'accesso e la gestione di tutti gli elementi del report da un'unica posizione.  
  
-   Provider di autenticazione e autorizzazioni di SharePoint, per controllare l'accesso a report, modelli e altri elementi.  
  
-   Topologie di distribuzione di SharePoint per la distribuzione di report fuori dal firewall tramite una connessione Internet. Il server di report fornisce i servizi di report ed elaborazione dati nel contesto di una distribuzione di SharePoint più ampia, configurata per l'accesso a Internet.  
  
-   Gestione di report, modelli, origini dei dati, pianificazioni e cronologia dei report in pagine di applicazione personalizzate in un sito di SharePoint. È possibile impostare proprietà, definire pianificazioni e sottoscrizioni, nonché creare e gestire cronologie di report in un sito di SharePoint esattamente come avviene con gli altri strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Pubblicazione o caricamento di report, modelli di report, risorse e file di origini dati condivise in una raccolta di SharePoint, incluso il Centro report in Office SharePoint Server.  
  
     Utilizzo di Progettazione report, Progettazione modelli e Generatore report per creare report e origini dati da pubblicare direttamente in una raccolta di SharePoint. È inoltre possibile utilizzare l'azione Carica in un sito di SharePoint per aggiungere qualsiasi definizione di report e modello di report a una raccolta di SharePoint.  
  
     Poiché il server di report elabora le definizioni dei report sempre allo stesso modo, indipendentemente dalla modalità del server utilizzata, il layout e i dati del report sono indipendenti dalla modalità del server. Tutti i report eseguibili in un server di report in modalità nativa possono essere eseguiti anche in un server di report configurato per la modalità integrata SharePoint.  
  
-   Sottoscrizione e recapito di report a una raccolta di SharePoint tramite una nuova estensione per il recapito di SharePoint. I report possono essere recapitati anche per posta elettronica o a una cartella condivisa. Per recapitare i report vengono utilizzate le estensioni per il recapito del server di report. È possibile creare sottoscrizioni guidate dai dati per una distribuzione di report su vasta scala utilizzando i dati del sottoscrittore sottoposti a query in fase di esecuzione.  
  
-   Web part di Visualizzatore report che è possibile aggiungere alle pagine di SharePoint per visualizzare un report nell'applicazione Web di SharePoint. La web part include funzionalità per la navigazione tra le pagine, la ricerca, la stampa e l'esportazione.  
  
-   Utilizzo di un nuovo endpoint SOAP per la realizzazione di applicazioni personalizzate da integrare con un sito di SharePoint. È inoltre possibile utilizzare il provider WMI (Windows Management Instrumentation, Strumentazione gestione Windows) aggiornato per configurare a livello di programmazione un'istanza del server di report eseguita in modalità integrata SharePoint.  
  
-   Creazione di report di servizi Microsoft Access in modalità connessa.  
  
-   Aree AAM, distribuzioni che si interfacciano a Internet e token utenti di SharePoint per elenchi SharePoint.  
  
##  <a name="bkmk_connectedandlocal"></a> Modalità con connessione e modalità locale

 Con la versione SQL Server 2008 R2 viene introdotta una nuova *modalità locale* per la visualizzazione di report da un server SharePoint 2010 in cui è installato il componente aggiuntivo Reporting Services di Microsoft SQL Server 2008 R2 o versione successiva per prodotti SharePoint 2010.  
  
-   *Modalità locale*: la modalità locale consente l'esecuzione del rendering locale dei report dalla raccolta documenti di SharePoint, senza l'integrazione con un server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . A differenza del server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per i prodotti SharePoint è obbligatorio. Il componente aggiuntivo può essere installato in diversi modi, tra cui l'Utilità preparazione prodotti Microsoft SharePoint 2010. Per altre informazioni sulla modalità locale, vedere [Report in modalità locale e Report nel Visualizzatore di Report in modalità locale &#40;Reporting Services in modalità SharePoint&#41; ](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) e [dove trovare il componente aggiuntivo di Reporting Services per prodotti SharePoint](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modalità con connessione*: Modalità con connessione è supportata tramite l'integrazione un [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] server di report nella farm di SharePoint usando Amministrazione centrale SharePoint. L'integrazione con un server di report consente la creazione report completa end-to-end, fornendo le funzionalità di collaborazione di SharePoint 2010 e le funzionalità basate su server di un server di report tra cui: Sottoscrizioni, snapshot ed elaborazione basata su server.  
  
##  <a name="bkmk_unsupportedsharepoint"></a> Funzionalità di SharePoint non supportate

 Non tutte le funzionalità di SharePoint sono disponibili per le operazioni in modalità integrata. Di seguito è riportato un elenco delle funzionalità di SharePoint non direttamente integrate in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :  
  
-   Servizio di archiviazione sicura.  
  
-   In una raccolta documenti non è possibile utilizzare l'integrazione con il calendario di Outlook in SharePoint o la funzionalità di pianificazione di SharePoint per i file di Reporting Services.  
  
-   Catalogo dati business di SharePoint.  
  
-   La personalizzazione di SharePoint non è supportata neanche nelle pagine di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . L'integrazione del server di report non è supportata se l'applicazione Web di SharePoint è abilitata per l'accesso anonimo.  
  
-   SQL Server Reporting Services **non** supporta il controllo della versione della raccolta documenti di SharePoint. Se si salvano gli elementi del report in una raccolta documenti configurata con la cronologia delle versioni dei documenti abilitata, le funzionalità di Reporting Services non funzioneranno correttamente e verranno generati errori nel log ULS. Di seguito è riportato un esempio di errore nel log ULS:  
  
    -   "Un'origine dati associata al report è stata disabilitata"  
  
     La cronologia delle versioni della raccolta documenti viene configurata nella pagina "Impostazioni controllo versioni" di "Impostazioni raccolta".  
  
##  <a name="bkmk_supportedcombinations"></a> Combinazioni supportate del componente aggiuntivo di SharePoint e del server di report

 Non tutte le funzionalità sono supportate in tutte le combinazioni di server di report, componente aggiuntivo di Reporting Services per SharePoint e prodotti SharePoint. Per altre informazioni, vedere [combinazioni supportate di SharePoint e Server Reporting Services e componente aggiuntivo &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  La versione corretta del componente aggiuntivo di Reporting Services deve essere utilizzata con la versione corrispondente dei prodotti SharePoint.  
  
##  <a name="bkmk_components"></a> Componenti utilizzati per l'integrazione

 Per combinare i server in un'unica distribuzione, integrare un'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] con un'istanza dei prodotti SharePoint.  
  
 L'integrazione viene realizzata tramite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per prodotti SharePoint. Il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è un componente distribuito gratuitamente, che può essere scaricato e quindi installato in un server in cui viene eseguita la versione appropriata di SharePoint.  
  
> [!TIP]  
>  Non tutte le funzionalità sono supportate in tutte le combinazioni di server di report, componente aggiuntivo di Reporting Services per SharePoint e prodotti SharePoint. Per altre informazioni, vedere [combinazioni supportate di SharePoint e Server Reporting Services e componente aggiuntivo &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   In SharePoint il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornisce l'endpoint proxy ReportServer, una web part di visualizzatore di report e pagine dell'applicazione che consentono di visualizzare, archiviare e gestire il contenuto del server di report in un sito o una farm di SharePoint.  
  
-   In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono disponibili file di programma aggiornati, un endpoint SOAP ed estensioni di sicurezza e per il recapito personalizzate. È necessario configurare il server di report affinché venga eseguito in modalità integrata SharePoint e sia dedicato esclusivamente al supporto del recapito e dell'accesso ai report tramite il sito di SharePoint.  
  
 Dopo l'installazione del componente aggiuntivo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in SharePoint e la configurazione dei due server per l'integrazione, è possibile caricare o pubblicare i tipi di contenuto del server di report in una raccolta di SharePoint e quindi visualizzare e gestire tali documenti da un sito di SharePoint. Il caricamento o la pubblicazione iniziale del contenuto del server di report è molto importante. La web part e le pagine diventano disponibili quando l'utente seleziona definizioni di report (con estensione rdl), modelli di report (con estensione smdl) e origini dei dati condivise (con estensione rsds) in un sito di SharePoint.  
  
##  <a name="bkmk_language"></a> Considerazioni sul linguaggio

 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../includes/sps2010-md.md)] sono disponibili in molte più lingue rispetto a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 Quando si configura un server di report per l'esecuzione in una distribuzione di un prodotto SharePoint, è possibile che i vari elementi vengano visualizzati in lingue diverse. L'interfaccia utente, la documentazione e i messaggi verranno visualizzati nelle lingue seguenti:  
  
-   Tutti gli strumenti, le pagine di applicazione, gli errori, gli avvisi e i messaggi generati da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] verranno visualizzati nella lingua utilizzata dall'istanza di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , ovvero in una delle lingue di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Le pagine dell'applicazione aperte in un sito di SharePoint, la web part di Visualizzatore report e Generatore report saranno visualizzati in una delle lingue supportate per il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Per visualizzare l'elenco di lingue supportate, visitare la pagina di [download di SQL Server](https://msdn.microsoft.com/sql/downloads/) e cercare la pagina di download per il componente aggiuntivo [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
-   I siti di SharePoint, Amministrazione centrale SharePoint, la Guida online e i messaggi sono disponibili nelle lingue supportate dai prodotti Office Server.  
  
 Se la lingua del prodotto o della tecnologia SharePoint in uso è diversa da quella del server di report, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tenterà di utilizzare la lingua più simile disponibile nella stessa famiglia linguistica. Se non è disponibile un sostituto sufficientemente simile, per il server di report verrà utilizzata la lingua inglese.  
  
##  <a name="bkmk_relatedtasks"></a> Attività correlate

 Nella tabella seguente sono riepilogate le attività correlate a un server di report in modalità SharePoint per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :  
  
|**Attività**|**Collegamento**|  
|--------------|--------------|  
|Passaggi dettagliati per l'installazione e la configurazione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in modalità SharePoint.|[Installare Reporting Services in modalità SharePoint per SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) e [aggiungere un ulteriore Server di Report a una Farm di &#40;scalabilità orizzontale SSRS&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Scalabilità orizzontale della distribuzione di SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] aggiungendo server di report aggiuntivi.|[Aggiungere un ulteriore Server di Report a una Farm di &#40;scalabilità orizzontale SSRS&#41; ](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [topologie di distribuzione per le funzionalità SQL Server BI in SharePoint](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md) .|  
|Aggiunta di front-end Web SharePoint aggiuntivi con componenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] installati per la visualizzazione e gli elementi del report.|[Aggiungere un ulteriore front-end Web di Reporting Services a una farm](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configurazione della posta elettronica per le funzionalità di sottoscrizione e avvisi dati di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|[Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|Informazioni recenti per questa versione, disponibili nel sito Wiki TechNet.|[Suggerimenti e risoluzione dei problemi per SQL Server 2012 Reporting Services](https://go.microsoft.com/fwlink/?LinkId=221297).|  
  
## <a name="see-also"></a>Vedere anche  
 [Installare o disinstallare il Reporting aggiuntivo Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41; ](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md) [requisiti Hardware e Software per Reporting Services in modalità SharePoint](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md) [Web Part Visualizzatore di report in un sito di SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)