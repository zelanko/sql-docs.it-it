---
title: Server di report di Reporting Services (modalità SharePoint) | Microsoft Docs
ms.date: 09/26/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: af25232f5a1603f25814309270813188c05a89fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68262347"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Server di report di Reporting Services (modalità SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Un server di report di Reporting Services configurato per la **modalità SharePoint** può essere eseguito all'interno di una distribuzione di un prodotto SharePoint. Tramite un server di report in modalità SharePoint è possibile utilizzare le funzionalità di collaborazione e gestione di SharePoint per report e altri tipi di contenuto di [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] . La modalità SharePoint richiede l'installazione della versione appropriata del componente aggiuntivo Reporting Services per prodotti SharePoint nei front-end Web di SharePoint.  
  
> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

 Per ulteriori informazioni sull'installazione e sulla configurazione, vedere quanto riportato di seguito:  
  
-   [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Aggiungere un ulteriore server di report a una farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
## <a name="feature-summary"></a>Riepilogo delle funzionalità

 Quando si configura un server di report per l'esecuzione in modalità integrata SharePoint vengono aggiunte le funzionalità seguenti, che sono disponibili solo quando si distribuisce un server di report in tale modalità:  
  
-   Funzionalità di gestione dei documenti e collaborazione di SharePoint, inclusi avvisi. Un sito di SharePoint costituisce un portale unificato per l'accesso e la gestione di tutti gli elementi del report da un'unica posizione.  
  
-   Provider di autenticazione e autorizzazioni di SharePoint, per controllare l'accesso a report, modelli e altri elementi.  
  
-   Topologie di distribuzione di SharePoint per la distribuzione di report fuori dal firewall tramite una connessione Internet. Il server di report fornisce i servizi di report ed elaborazione dati nel contesto di una distribuzione di SharePoint più ampia, configurata per l'accesso a Internet.  
  
-   Gestione di report, modelli, origini dei dati, pianificazioni e cronologia dei report in pagine di applicazione personalizzate in un sito di SharePoint. È possibile impostare proprietà, definire pianificazioni e sottoscrizioni, nonché creare e gestire cronologie di report in un sito di SharePoint esattamente come avviene con gli altri strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Pubblicazione o caricamento di report, modelli di report, risorse e file di origini dati condivise in una raccolta di SharePoint, incluso il Centro report in Office SharePoint Server.  
  
     Utilizzo di Progettazione report, Progettazione modelli e Generatore report per creare report e origini dati da pubblicare direttamente in una raccolta di SharePoint. È inoltre possibile utilizzare l'azione Carica in un sito di SharePoint per aggiungere qualsiasi definizione di report e modello di report a una raccolta di SharePoint.  
  
     Poiché il server di report elabora le definizioni dei report sempre allo stesso modo, indipendentemente dalla modalità del server utilizzata, il layout e i dati del report sono indipendenti dalla modalità del server. Tutti i report eseguibili in un server di report in modalità nativa possono essere eseguiti anche in un server di report configurato per la modalità integrata SharePoint.  
  
-   Sottoscrizione e recapito di report a una raccolta di SharePoint tramite una nuova estensione per il recapito di SharePoint. I report possono essere recapitati anche per posta elettronica o a una cartella condivisa. Per recapitare i report vengono utilizzate le estensioni per il recapito del server di report. È possibile creare sottoscrizioni guidate dai dati per una distribuzione di report su vasta scala utilizzando i dati del sottoscrittore sottoposti a query in fase di esecuzione.  
  
-   Web part Visualizzatore di report che è possibile aggiungere alle pagine di SharePoint per visualizzare un report nell'applicazione Web di SharePoint. La web part include funzionalità per la navigazione tra le pagine, la ricerca, la stampa e l'esportazione.  
  
-   Utilizzo di un nuovo endpoint SOAP per la realizzazione di applicazioni personalizzate da integrare con un sito di SharePoint. È inoltre possibile utilizzare il provider WMI (Windows Management Instrumentation, Strumentazione gestione Windows) aggiornato per configurare a livello di programmazione un'istanza del server di report eseguita in modalità integrata SharePoint.  
  
-   Creazione di report di servizi Microsoft Access in modalità connessa.  
  
-   Aree AAM, distribuzioni che si interfacciano a Internet e token utenti di SharePoint per elenchi SharePoint.  
  
## <a name="connected-mode-and-local-mode"></a>Modalità con connessione e modalità locale

 Con la versione SQL Server 2008 R2 viene introdotta una nuova *modalità locale* per la visualizzazione di report da un server SharePoint 2010 in cui è installato il componente aggiuntivo Reporting Services di Microsoft SQL Server 2008 R2 o versione successiva per prodotti SharePoint 2010.  
  
-   *Modalità locale*: la modalità locale consente l'esecuzione del rendering locale dei report dalla raccolta documenti di SharePoint, senza l'integrazione con un server di report di Reporting Services. A differenza del server di report di Reporting Services, il componente aggiuntivo di Reporting Services per i prodotti SharePoint è obbligatorio. Il componente aggiuntivo può essere installato in diversi modi, tra cui l'Utilità preparazione prodotti Microsoft SharePoint 2010. Per altre informazioni sulla modalità locale, vedere [Report in modalità locale e con connessione nel Visualizzatore di report](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) e [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modalità con connessione*: la modalità con connessione è supportata tramite l'integrazione di un server di report di Reporting Services nella farm di SharePoint usando Amministrazione centrale SharePoint. L'integrazione con un server di report consente la creazione completa di report, fornendo le funzionalità di collaborazione di SharePoint 2010 e le funzionalità basate su server di un server di report, tra cui sottoscrizioni, snapshot ed elaborazione basata su server.  
  
## <a name="unsupported-sharepoint-features"></a>Funzionalità di SharePoint non supportate

 Non tutte le funzionalità di SharePoint sono disponibili per le operazioni in modalità integrata. Di seguito è riportato un elenco di funzionalità di SharePoint non direttamente integrate in Reporting Services:  
  
-   Servizio di archiviazione sicura.  
  
-   In una raccolta documenti non è possibile utilizzare l'integrazione con il calendario di Outlook in SharePoint o la funzionalità di pianificazione di SharePoint per i file di Reporting Services.  
  
-   Catalogo dati business di SharePoint.  
  
-   La personalizzazione di SharePoint non è supportata neanche nelle pagine di Reporting Services. L'integrazione del server di report non è supportata se l'applicazione Web di SharePoint è abilitata per l'accesso anonimo.  
  
-   SQL Server Reporting Services **non** supporta il controllo della versione della raccolta documenti di SharePoint. Se si salvano gli elementi del report in una raccolta documenti configurata con la cronologia delle versioni dei documenti abilitata, le funzionalità di Reporting Services non funzioneranno correttamente e verranno generati errori nel log ULS. Di seguito è riportato un esempio di errore nel log ULS:  
  
    -   "Un'origine dati associata al report è stata disabilitata"  
  
     La cronologia delle versioni della raccolta documenti viene configurata nella pagina "Impostazioni controllo versioni" di "Impostazioni raccolta".  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>Combinazioni supportate del componente aggiuntivo di SharePoint e del server di report

 Non tutte le funzionalità sono supportate in tutte le combinazioni di server di report, componente aggiuntivo di Reporting Services per SharePoint e prodotti SharePoint. Per altre informazioni, vedere [Combinazioni supportate di server di SharePoint e Reporting Services](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  La versione corretta del componente aggiuntivo di Reporting Services deve essere utilizzata con la versione corrispondente dei prodotti SharePoint.  
  
## <a name="components-that-provide-integration"></a>Componenti usati per l'integrazione

 Per combinare i server in un'unica distribuzione, integrare un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services con un'istanza dei prodotti SharePoint  
  
 L'integrazione viene realizzata tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il componente aggiuntivo Reporting Services per prodotti SharePoint. Il componente aggiuntivo Reporting Services è un componente distribuito gratuitamente, che può essere scaricato e quindi installato in un server in cui viene eseguita la versione appropriata di SharePoint.  
  
> [!TIP]  
>  Non tutte le funzionalità sono supportate in tutte le combinazioni di server di report, componente aggiuntivo di Reporting Services per SharePoint e prodotti SharePoint. Per altre informazioni, vedere [Combinazioni supportate di server di SharePoint e Reporting Services](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   In SharePoint il componente aggiuntivo Reporting Services offre l'endpoint proxy ReportServer, una web part Visualizzatore di report e pagine dell'applicazione che consentono di visualizzare, archiviare e gestire il contenuto del server di report in un sito o una farm di SharePoint.  
  
-   In Reporting Services sono disponibili file di programma aggiornati, un endpoint SOAP ed estensioni di sicurezza e per il recapito personalizzate. È necessario configurare il server di report affinché venga eseguito in modalità integrata SharePoint e sia dedicato esclusivamente al supporto del recapito e dell'accesso ai report tramite il sito di SharePoint.  
  
 Dopo l'installazione del componente aggiuntivo Reporting Services in SharePoint e la configurazione dei due server per l'integrazione, è possibile caricare o pubblicare i tipi di contenuto del server di report in una raccolta di SharePoint e quindi visualizzare e gestire tali documenti da un sito di SharePoint. Il caricamento o la pubblicazione iniziale del contenuto del server di report è molto importante. La web part e le pagine diventano disponibili quando l'utente seleziona definizioni di report (con estensione rdl), modelli di report (con estensione smdl) e origini dei dati condivise (con estensione rsds) in un sito di SharePoint.  
  
##  <a name="language-considerations"></a>Considerazioni sul linguaggio

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] sono disponibili in molte più lingue rispetto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Quando si configura un server di report per l'esecuzione in una distribuzione di un prodotto SharePoint, è possibile che i vari elementi vengano visualizzati in lingue diverse. L'interfaccia utente, la documentazione e i messaggi verranno visualizzati nelle lingue seguenti:  
  
- Tutti gli strumenti, le pagine di applicazione, gli errori, gli avvisi e i messaggi generati da Reporting Services verranno visualizzati nella lingua usata dall'istanza di Reporting Services, ovvero in una delle lingue di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Le pagine dell'applicazione aperte in un sito di SharePoint, la web part Visualizzatore di report e Generatore report verranno visualizzati in una delle lingue supportate per il componente aggiuntivo Reporting Services. Per visualizzare l'elenco di lingue supportate, visitare la pagina dei [download di SQL Server](https://msdn.microsoft.com/sql/downloads/) e cercare la pagina di download del componente aggiuntivo Reporting Services di SQL Server 2016.  
  
- I siti di SharePoint, Amministrazione centrale SharePoint, la Guida online e i messaggi sono disponibili nelle lingue supportate dai prodotti Office Server.  
  
 Se la lingua del prodotto o della tecnologia SharePoint in uso è diversa da quella del server di report, Reporting Services tenterà di usare la lingua più simile disponibile nella stessa famiglia linguistica. Se non è disponibile un sostituto sufficientemente simile, per il server di report verrà utilizzata la lingua inglese.  
  
## <a name="related-tasks"></a>Attività correlate

 Nella tabella seguente sono riepilogate le attività correlate a un server di report in modalità SharePoint per Reporting Services:  
  
|**Attività**|**Collegamento**|  
|--------------|--------------|  
|Passaggi dettagliati per l'installazione e la configurazione di Reporting Services in modalità SharePoint.|[Installare la modalità SharePoint di Reporting Services per SharePoint 2010](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c) e [Aggiungere un ulteriore server di report a una farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Scalabilità orizzontale della distribuzione di SharePoint di Reporting Services aggiungendo server di report aggiuntivi.|[Aggiungere un ulteriore server di report a una farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [Topologie di distribuzione per funzionalità di Business Intelligence di SQL Server in SharePoint](https://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).|  
|Aggiunta di front-end Web SharePoint aggiuntivi con componenti di Reporting Services installati per la visualizzazione e gli elementi del report.|[Aggiungere un ulteriore front-end Web di Reporting Services a una farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configurazione della posta elettronica per il server di report all'interno di SharePoint.|[Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|Informazioni recenti per questa versione, disponibili nel sito Wiki TechNet.|[Suggerimenti e risoluzione dei problemi per SQL Server 2012 Reporting Services](https://go.microsoft.com/fwlink/?LinkId=221297).|  

## <a name="next-steps"></a>Passaggi successivi

[Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)
[Web part Visualizzatore di report in un sito di SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
