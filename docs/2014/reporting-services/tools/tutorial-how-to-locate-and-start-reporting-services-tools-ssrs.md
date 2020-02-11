---
title: 'Esercitazione: Individuazione e avvio degli strumenti di Reporting Services (SSRS) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4edd0b6e3928a2bc3a280403a87eda5bb797e620
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099476"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>Esercitazione: Individuazione e avvio degli strumenti di Reporting Services (SSRS)
  In questa esercitazione vengono descritti gli strumenti utilizzati per configurare un server di report, gestire le operazioni e il contenuto del server di report, nonché creare e pubblicare report. In questa esercitazione vengono descritte le procedure per individuare e aprire ogni strumento. Se si ha familiarità con gli strumenti, è possibile passare ad altre esercitazioni che consentono di acquisire capacità importanti per l'utilizzo di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Per ulteriori informazioni sulle altre esercitazioni, vedere [Reporting Services esercitazioni &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md).  
  
 In questo argomento  
  
-   [Gestione configurazione Reporting Services (modalità nativa)](#bkmk_configuration_manager)  
  
-   [Gestione report (modalità nativa)](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [SQL Server Data Tools con Progettazione report e creazione guidata report](#bkmk_ssdt)  
  
-   [Generatore report](#bkmk_report_builder)  
  
##  <a name="bkmk_configuration_manager"></a>Reporting Services Configuration Manager (modalità nativa)  
 Utilizzare Gestione configurazione in modalità nativa per completare le operazioni seguenti:, , , , , e.  
  
-   Specificare l'account del servizio.  
  
-   Creare o aggiornare il database del server di report.  
  
-   Modificare le proprietà di connessione.  
  
-   Specificare gli URL.  
  
-   Gestire le chiavi di crittografia.  
  
-   Configurare l'elaborazione automatica del report e il relativo recapito per posta elettronica.  
  
 **Installazione:** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Configuration Manager viene installato quando si installa [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] la modalità nativa. Per ulteriori informazioni, vedere [Install Reporting Services server di report in modalità nativa](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>Per avviare Gestione configurazione Reporting Services  
  
1.  Nella schermata Start di Windows digitare `reporting` e nei risultati di ricerca delle **app** fare clic su **Reporting Services Configuration Manager**.  
  
     ![Gestione configurazione Reporting Services all'avvio](../media/bi-ssrs-configmanager-win8-startscreen.gif "Gestione configurazione Reporting Services all'avvio")  
  
     **O**  
  
     Fare clic sul pulsante **Avvia**, selezionare **Programmi**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Strumenti di configurazione**, quindi scegliere **Gestione configurazione Reporting Services**.  
  
     Verrà visualizzata la finestra di dialogo **Selezione istanza Server report** in cui è possibile selezionare l'istanza del server di report che si desidera configurare.  
  
2.  In **Nome server**specificare il nome del computer in cui è installata l'istanza del server di report. Per impostazione predefinita è specificato il nome del computer locale, ma è anche possibile digitare il nome di un'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Se si specifica un computer remoto, fare clic su **Trova** per stabilire una connessione. È necessario configurare in anticipo il server di report per l'amministrazione remota. Per altre informazioni, vedere [Configurare un server di report per l'amministrazione remota](../report-server/configure-a-report-server-for-remote-administration.md).  
  
3.  In **Nome istanza**selezionare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] che si desidera configurare. Nell'elenco sono visualizzate solo le istanze del server di report basate su [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Non è possibile configurare versioni precedenti di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
4.  Fare clic su **Connetti**.  
  
5.  Per verificare di avere avviato lo strumento, confrontare i risultati ottenuti con la figura seguente:  
  
     ![Strumento di configurazione di Reporting Services](../media/rs-ui-reportserverconfigkatmai.gif "Strumento di configurazione di Reporting Services")  
  
 **Passaggi successivi:** [configurare e amministrare un Server di report &#40;modalità nativa SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md) e [Reporting Services Configuration Manager &#40;modalità nativa ](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)&#41;.  
  
##  <a name="bkmk_report_manager"></a>Gestione report (modalità nativa)  
 Utilizzare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md) per impostare autorizzazioni, gestire sottoscrizioni e pianificazioni e utilizzare i report. Con Gestione report è inoltre possibile visualizzare i report.  
  
 **Installazione:** Gestione report viene installato quando si installa [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] la modalità nativa di: [installare Reporting Services server di report in modalità nativa](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 Per aprire Gestione report è necessario disporre di autorizzazioni sufficienti (inizialmente, solo i membri del gruppo Administrators locale dispongono delle autorizzazioni per l'accesso alle funzionalità di Gestione report). Gestione report offre diverse pagine e opzioni a seconda delle assegnazioni di ruolo dell'utente corrente. Per gli utenti che non dispongono di autorizzazioni verrà visualizzata una pagina vuota. Per gli utenti con autorizzazioni per la visualizzazione di report verranno visualizzati collegamenti per aprire i report. Per sapere di più sulle autorizzazioni, vedere [Ruoli e autorizzazioni &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
#### <a name="to-start-report-manager"></a>Per avviare Gestione report  
  
1.  Aprire il browser. Per informazioni sui browser supportati e le versioni del browser, vedere [Planning for Reporting Services e Power View Browser Support &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
2.  Nella barra degli indirizzi del browser digitare l'URL di Gestione report. Per impostazione predefinita, l'URL **è\<http://nomeserver>/Reports**. È possibile verificare il nome e l'URL del server tramite lo strumento di configurazione di Reporting Services. Per altre informazioni sugli URL usati in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], vedere [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
3.  Gestione report verrà aperto nella finestra del browser. La pagina iniziale è la cartella Home. A seconda delle autorizzazioni di cui si dispone, verranno visualizzati ulteriori cartelle, collegamenti ipertestuali ai report e file di risorse all'interno della pagina iniziale. Potrebbero inoltre essere disponibili pulsanti e comandi aggiuntivi nella barra degli strumenti.  
  
4.  Se si esegue Gestione report nel server di report locale, vedere [configurare un server di report in modalità nativa per l'amministrazione locale &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 **Passaggi successivi:** [configurare Gestione report &#40;&#41;in modalità nativa ](../report-server/configure-web-portal.md).  
  
##  <a name="bkmk_managements_studio"></a>Management Studio  
 Gli amministratori del server di report possono utilizzare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per gestire un server di report insieme ad altri componenti server di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md).  
  
#### <a name="to-start-sql-server-management-studio"></a>Per avviare SQL Server Management Studio  
  
1.  Dalla schermata iniziale di Windows digitare `sql server` e nei risultati di ricerca delle **app** fare clic su **SQL Server Management Studio**.  
  
     ![Management Studio dalla schermata iniziale di Windows](../media/bi-ssms-win8-startscreen.gif "Management Studio dalla schermata iniziale di Windows")  
  
     **O**  
  
     Fare clic su **Start**, selezionare **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], quindi scegliere **SQL Server Management Studio**. Viene visualizzata la finestra di dialogo **Connetti al server** .  
  
2.  Se la finestra di dialogo **Connetti al server** non viene visualizzata, in **Esplora oggetti**fare clic su **Connetti** e quindi scegliere **Reporting Services**.  
  
3.  Nell'elenco **Tipo server** selezionare **Reporting Services**. Se [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] non è incluso nell'elenco, significa che non è installato.  
  
4.  Nell'elenco **Nome server** selezionare un'istanza del server di report. Nell'elenco sono visualizzate le istanze locali. È inoltre possibile specificare il nome di un'istanza remota di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
5.  Fare clic su **Connetti**. È possibile espandere il nodo radice per impostare proprietà server, modificare definizioni di ruolo o disabilitare funzionalità del server di report.  
  
##  <a name="bkmk_ssdt"></a>SQL Server Data Tools con Progettazione report e creazione guidata report  
 Progettazione report è disponibile in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Business Intelligence per Visual Studio 2012. Nell'area di progettazione dello strumento sono inclusi finestre a schede, procedure guidate e menu per l'accesso alle funzionalità per la creazione di report. Lo strumento di progettazione report è disponibile quando si sceglie un modello di progetto per il server di report o di procedura guidata di server di report. Per sapere di più, vedere [Reporting Services in SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md).  
  
#### <a name="to-start-report-designer"></a>Per avviare Progettazione report  
  
1.  Dalla schermata iniziale di Windows digitare **data** e nei risultati di ricerca per **Applicazioni** fare clic su **SQL Server Data Tools per Visual Studio 2012**.  
  
     **O**  
  
     Fare clic su **Start**, scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], quindi fare clic su **SQL Server Data Tools (SSDT)**.  
  
2.  Scegliere **Nuovo** dal menu **File**e quindi fare clic su **Progetto**.  
  
3.  Nell'elenco **Tipi progetto** fare clic su **Progetti Business Intelligence**.  
  
4.  Nell'elenco **Modelli** fare clic su **Progetto Server report**. Nella figura seguente vengono illustrati i modelli di progetto così come sono visualizzati nella finestra di dialogo:  
  
     ![Finestra di dialogo relativa al nuovo modello di progetto](../media/rs-ui-newrsproject.gif "Finestra di dialogo relativa al nuovo modello di progetto")  
  
5.  Digitare un nome e un percorso per il progetto oppure fare clic su **Sfoglia** e selezionare il percorso desiderato.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] si apre con [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] la pagina iniziale. In Esplora soluzioni sono disponibili le categorie per la creazione di report e origini dei dati. È possibile utilizzare queste categorie per creare nuovi report e origini dei dati. Le finestre a schede vengono visualizzate quando si crea una definizione di report. Queste finestre sono Dati, Layout e Anteprima.  
  
 Per iniziare il primo report, vedere [Creare un report tabella semplice &#40;Esercitazione su SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md). Per altre informazioni sulle finestre di progettazione query che è possibile usare in Progettazione report, vedere [strumenti di progettazione di query in Progettazione report SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md).  
  
##  <a name="bkmk_report_builder"></a>Generatore report  
 Usare [Generatore report &#40;&#41;SSRS](report-builder-authoring-environment-ssrs.md) per creare report in un [!INCLUDE[msCoName](../../includes/msconame-md.md)] ambiente di creazione simile a Office. È possibile personalizzare e aggiornare tutti i report esistenti, sia che siano stati creati in Progettazione report o nelle versioni precedenti di Generatore report. Per informazioni sul percorso del file ReportBuilder3.msi che si esegue per installare Generatore report nel computer locale, rivolgersi all'amministratore.  
  
 **Installazione:** La versione di Generatore report viene installata in modalità [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nativa o in modalità SharePoint. La versione autonoma di Generatore report è un download separato.  Vedere [installare la versione autonoma di Generatore report &#40;Generatore report&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>Per avviare la versione ClickOnce di Generatore report da Gestione report (modalità nativa)  
  
1.  Nel Web browser digitare l'URL di Gestione report per il server di report. L'URL predefinito è http://\<*nomeserver*>/reports. Verrà aperto Gestione report.  
  
2.  Fare clic su **Generatore report**.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>Per avviare Generatore report ClickOnce tramite un URL  
  
1.  Nella barra degli indirizzi del browser digitare l'URL seguente:  
  
     **http://\<nomeserver>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application**  
  
2.  Premere INVIO.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>Per avviare la versione ClickOnce di Generatore report nella modalità SharePoint di Reporting Services  
  
1.  Accedere al sito contenente la raccolta in cui si desidera creare un nuovo report.  
  
2.  Aprire la raccolta.  
  
3.  Scegliere **Report di Generatore report** dal menu **Nuovo**.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
#### <a name="to-start-report-builder-stand-alone"></a>Per avviare la versione autonoma di Generatore report  
  
1.  Dalla schermata iniziale di Windows digitare **generatore report** , quindi scegliere **Generatore report 3.0**.  
  
     **O**  
  
     Dal menu Start scegliere **Tutti i programmi**, quindi fare clic su **Generatore report di Microsoft SQL Server 2014**.  
  
2.  Fare clic su **Generatore report**.  
  
     Verrà visualizzato Generatore report e sarà possibile creare o aprire un report.  
  
3.  Fare clic su **Guida di Generatore report** per aprire la documentazione relativa a Generatore report.  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione, disinstallazione e Generatore report del supporto](../install-uninstall-and-report-builder-support.md)   
 [Reporting Services installazione in modalità SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services server di report](../reporting-services-report-server.md)   
 [Strumenti di progettazione query in Progettazione report SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
