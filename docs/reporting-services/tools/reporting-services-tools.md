---
title: Strumenti di Reporting Services | Microsoft Docs
description: Informazioni sugli strumenti di sviluppo, configurazione, amministrazione e visualizzazione di report contenuti in SQL Server Reporting Services.
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b19b5aed9dcd3f40bb603606eeb0ae4df43beb0b
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892301"
---
# <a name="reporting-services-tools"></a>Strumenti di Reporting Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contiene un set di strumenti grafici e di scripting che supportano lo sviluppo e l'uso di report completi in un ambiente gestito. Il set include strumenti di sviluppo, strumenti di configurazione e amministrazione e strumenti per la visualizzazione di report. Questo articolo include una breve panoramica di ogni strumento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e di come è possibile accedervi.  
  
 Per trovare subito uno strumento, vedere [Esercitazione: Come individuare e avviare gli strumenti di Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md).  
  
## <a name="tools-for-report-authoring"></a>Strumenti per la creazione di report  
 La tabella seguente elenca gli strumenti disponibili per la creazione di report in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Strumento|Descrizione|Modalità di accesso|  
|----------|-----------------|-------------------|  
|[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]|Con [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] è possibile creare report per dispositivi mobili che adattano dinamicamente il contenuto alle dimensioni dello schermo o alla finestra del browser e che possono essere usati con schermi di qualsiasi dimensione.<br /><br /> Consente di creare report per dispositivi mobili in un'area di progettazione con righe e colonne della griglia regolabili ed elementi flessibili del report per dispositivi mobili.<br /><br /> Per altre informazioni, vedere [Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).|Scaricare [SQL Server Mobile Report Publisher](https://go.microsoft.com/fwlink/?LinkId=733527)|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|Un'esperienza interattiva di esplorazione e presentazione visiva dei dati progettata per consentire la creazione e l'interazione con i report basati sui modelli tabulari di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. Browser con Silverlight.|  
|Progettazione report|Questo strumento viene usato per progettare report e include le funzionalità seguenti:<br /><br /> Distribuzione in un server di report in modalità nativa o in modalità SharePoint.<br /><br /> Ospitato in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> Riquadro dei dati del report per organizzare i dati utilizzati nel report<br /><br /> Visualizzazioni a schede per la progettazione e l'anteprima per una progettazione dei report interattiva<br /><br /> Finestre di progettazione query che consentono di specificare i dati da recuperare dalle origini dati associati ai tipi di origini dati nel [file di configurazione RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)<br /><br /> Editor espressioni con supporto IntelliSense per compilare le espressioni di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] che consentono di personalizzare il contenuto e l'aspetto del report.<br /><br /> Supporta gli elementi del report personalizzati e le finestre Progettazione query personalizzate<br /><br /> <br /><br /> Per altre informazioni, vedere [Reporting Services in SQL Server Data Tools &#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|Generatore report|Questo strumento viene usato per progettare report e include le funzionalità seguenti:<br /><br /> Distribuzione in un server di report in modalità nativa o in modalità SharePoint.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] Ambiente di creazione simile a Office[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]<br /><br /> Possibilità di salvare elementi del report come parti di report<br /><br /> Una procedura guidata per la creazione di mappe<br /><br /> Aggregazioni di aggregazioni<br /><br /> Supporto migliorato per le espressioni<br /><br /> Finestre Progettazione query che consentono di specificare i dati da recuperare da una selezione di tipi di origini dati predefiniti<br /><br /> Per altre informazioni, vedere [Generatore report in SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md).|Scaricare la [versione autonoma di Generatore report](https://go.microsoft.com/fwlink/?LinkID=219138)<br /><br /> Oppure aprire dal portale Web o da SharePoint|  
  
## <a name="tools-for-report-server-administration"></a>Strumenti per l'amministrazione del server di report  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un set di strumenti grafici e di scripting per l'amministrazione del server di report. Gli strumenti utilizzati dipendono dalla modalità di distribuzione del server di report.  
  
### <a name="native-mode"></a>Modalità nativa  
 Nella tabella seguente vengono elencati gli strumenti disponibili per l'amministrazione del server di report distribuito in modalità nativa.  
  
|Strumento|Descrizione|Modalità di accesso|  
|----------|-----------------|-------------------|  
|Gestione configurazione server di report|Utilizzare questo strumento per configurare un'installazione di Reporting Services. Le attività disponibili includono:<br /><br />  Configurazione dell'account del servizio del server di report.<br /><br /> Creazione e configurazione di uno o più URL del servizio Web.<br /><br /> Configurazione dell'URL del portale Web<br /><br /> Creazione e configurazione del database del server di report.<br /><br /> Configurazione di una distribuzione con scalabilità orizzontale.<br /><br /> Backup, ripristino o sostituzione della chiave simmetrica utilizzata per crittografare stringhe di connessione e credenziali archiviate.<br /><br /> Configurazione dell'account di esecuzione automatica.<br /><br /> Configurazione delle impostazioni di sottoscrizione.<br /><br /> Configurazione di un server SMTP per il recapito tramite posta elettronica.<br /><br /> Configurazione del servizio Power BI (cloud).<br /><br /> Nota: Gestione configurazione del server di report consente di gestire il contenuto del server di report, abilitare funzionalità aggiuntive o concedere l'accesso al server.<br /><br /> Per altre informazioni, vedere [Gestione configurazione del server di report &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).|Menu Start|  
|SQL Server Management Studio|Utilizzare questo strumento per gestire una o più istanze del server di report in un unico ambiente, incluse le seguenti attività:.<br /><br /> Gestione sia delle istanze locali che remote del server di report<br /><br /> Impostazione delle proprietà del server di report<br /><br /> Modifica di definizioni di ruolo<br /><br /> Disabilitazione delle caratteristiche del server di report non utilizzate<br /><br /> Gestione di processi<br /><br /> Gestione di pianificazioni condivise|Menu Start|   
|Utilità rsconfig|Utilizzare questo strumento per configurare e gestire una connessione del server di report al database del server di report. È inoltre possibile utilizzarla per specificare un account utente per l'elaborazione automatica dei report.<br /><br /> Per altre informazioni, vedere [Utilità della riga di comando del server di report &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt dei comandi|  
|Utilità rskeymgmt|Utilizzare questo strumento per eseguire le operazioni seguenti:<br /><br /> Estrarre, ripristinare, creare ed eliminare la chiave simmetrica utilizzata per crittografare i dati del server di report.<br /><br /> Creare un join delle istanze del server di report in una distribuzione con scalabilità orizzontale.<br /><br /> <br /><br /> Per altre informazioni, vedere [Utilità della riga di comando del server di report &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt dei comandi|  
|Classi di Strumentazione gestione Windows (WMI)|Usare queste classi per automatizzare le attività di configurazione in Gestione configurazione del server di report senza che sia necessario usare l'interfaccia utente grafica.<br /><br /> Per altre informazioni, vedere [Accesso al provider WMI a livello di programmazione](../../reporting-services/accessing-the-wmi-provider-programmatically.md).|Visual Basic Script|  
  
### <a name="sharepoint-integrated-mode"></a>Modalità integrata SharePoint  
 In modalità SharePoint, Reporting Services è un'applicazione di servizio nell'architettura di SharePoint e viene amministrata direttamente tramite SharePoint  
  
|Strumento|Descrizione|Modalità di accesso|  
|----------|-----------------|-------------------|  
|Amministrazione centrale SharePoint|Usare Amministrazione centrale SharePoint per creare, eseguire una query e gestire le applicazioni di servizio condivise per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Per altre informazioni, vedere [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).|Browser per l'URL di Amministrazione centrale del sito di SharePoint|  
|Cmdlet di PowerShell|Utilizzare i cmdlet di PowerShell per creare, eseguire una query e gestire le applicazioni di servizio condivise per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Per altre informazioni, vedere [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)(Cmdlet di PowerShell per la modalità SharePoint di Reporting Services).|Shell di gestione SharePoint 2010|  
  
## <a name="tools-for-report-content-management"></a>Strumenti per la gestione del contenuto dei report  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile un set di strumenti grafici e di scripting per la gestione del contenuto. Gli strumenti utilizzati dipendono dalla modalità di distribuzione del server di report.  
  
|Strumento|Descrizione|Modalità di accesso|  
|----------|-----------------|-------------------|  
|URL del servizio Web ReportServer|Utilizzare questo strumento per cercare il contenuto nel catalogo del report in una pagina di navigazione degli elementi generica.<br /><br /> Per ulteriori informazioni, vedere [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md).|Browser|  
|portale Web|**(Solo in modalità nativa)** Usare questo strumento per amministrare una sola istanza del server di report da un percorso remoto su una connessione HTTP. È possibile eseguire le operazioni seguenti:<br /><br /> Visualizzare, ricercare, stampare e sottoscrivere report.<br /><br /> Creare, proteggere e gestire la gerarchia di cartelle per organizzare gli elementi presenti nel server.<br /><br /> Configurare la sicurezza basata sui ruoli dalla quale dipende l'accesso a elementi e operazioni.<br /><br /> Configurare le proprietà di esecuzione del report, la cronologia del report e i parametri del report.<br /><br /> Creare modelli di report che si connettono e recuperano dati da un'origine dati di Microsoft SQL Server Analysis Services o da un'origine dati relazionale di SQL Server.<br /><br /> Impostare la sicurezza degli elementi di un modello per consentire l'accesso a entità specifiche del modello o per eseguire il mapping delle entità a report click-through predefiniti creati in precedenza.<br /><br /> Creare pianificazioni condivise e origini dei dati condivise per migliorare la gestione delle pianificazioni e delle connessioni alle origini dei dati.<br /><br /> Creare sottoscrizioni guidate dai dati che consentono di implementare i report in un elenco di destinatari di grandi dimensioni.<br /><br /> Creare report collegati per riutilizzare e ridefinire gli scopi di un report esistente in modi diversi.<br /><br /> Avviare Generatore report per creare report da salvare ed eseguire nel server di report. Per altre informazioni, vedere [Portale Web di un server di report (modalità nativa SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).| Browser  
|Utilità rs|Questo strumento è un host di script che è possibile utilizzare per l'esecuzione di operazioni inserite nello script. Questo strumento consente di eseguire script di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] per la copia di dati tra database del server di report, la pubblicazione di report, la creazione di elementi in un database del server di report e altro ancora. Per altre informazioni, vedere [Utilità della riga di comando del server di report &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Prompt dei comandi|  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Report Server](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Concetti relativi a Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Che cos'è SQL Server Reporting Services (SSRS)](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  