---
title: Configurare Gestione Report (modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 81be4bb3802888a8471308135775723c9ba0fd9e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419862"
---
# <a name="configure-report-manager-native-mode"></a>Configurare Gestione report (modalità nativa)
  Gestione report è un'applicazione front-end Web utilizzata per visualizzare report, gestire il contenuto del server di report e concedere l'accesso utente a un server di report in modalità nativa. Gestione report viene installato con il servizio Web ReportServer all'interno della stessa istanza del server di report e facoltativamente configurato se si seleziona l'opzione **Installa la configurazione predefinita della modalità nativa** del programma di installazione. Può essere configurato anche come attività di post-installazione. In questo argomento vengono fornite informazioni sui seguenti scenari di configurazione di Gestione report:  
  
-   [Configurare Gestione report per l'utilizzo dell'URL predefinito](#ConfigureRMURL)  
  
     Gestione report è un'applicazione Web a cui si accede tramite un browser Web. È necessario almeno definire l'URL utilizzato per aprire l'applicazione in una finestra del browser. L'URL è costituito da un nome host, una porta e una directory virtuale. I valori predefiniti per questo URL includono i valori del nome host e della porta definiti per l'URL del servizio Web ReportServer, oltre al nome della directory virtuale **reports** . Se si dispone di un'istanza denominata, la directory virtuale è **istanza_report**, dove **istanza** è il nome dell'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Eseguire Gestione report da un computer remoto**. A seconda della configurazione della rete, potrebbe essere necessario abilitare la porta 80 nei computer per consentire le richieste con Gestione report.  
  
    > [!TIP]  
    >  Se si tenta di accedere a Gestione report in un computer remoto e si ricevono messaggi di errore di connessione nel browser, una causa comune è da individuare nelle impostazioni del firewall. Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](configure-a-firewall-for-report-server-access.md).  
  
     Se necessario, abilitare la porta 80 su entrambi i computer per consentire le richieste tramite tale porta. Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](configure-a-firewall-for-report-server-access.md).  
  
-   [Configurare Gestione report per l'utilizzo dell'URL di un server di report specifico](#ConfigureSpecificURL)  
  
     Per impostazione predefinita, Gestione report si connette al servizio Web ReportServer eseguito nello stesso servizio ReportServer e utilizza l'URL di questo servizio per eseguire la connessione. Se si definiscono più URL per il servizio Web ReportServer, viene utilizzato quello definito per ultimo. Per alcune distribuzioni, può tuttavia essere necessario connettere sempre Gestione report al servizio Web tramite un URL statico, ad esempio nei casi in cui il filtro dei pacchetti è stato configurato su una porta o un indirizzo IP specifico e si desidera che tutte le connessioni al server di report vengano sottoposte alle regole di filtro definite.  
  
-   [Impostare Gestione report per far sì che punti a un server di report remoto](#ConfigureRemoteRS)  
  
     Per impostazione predefinita, Gestione report fornisce l'accesso front-end al servizio Web ReportServer in esecuzione nella stessa istanza del server. È tuttavia possibile configurarlo per la connessione a un servizio Web ReportServer remoto se si desidera eseguire il servizio Web e Gestione report in processi distinti o se si configura l'accesso in modo diverso per ogni server, ad esempio se si distribuisce Gestione report agli utenti tramite una connessione Extranet o Internet e si desidera inserire un firewall tra il server di report e Gestione report.  
  
-   [Personalizzare stili e titolo dell'applicazione](#ModifyTitle)  
  
     Gestione report, il visualizzatore di report HTML e la barra degli strumenti dei report possono essere personalizzati in modo limitato modificando gli stili e il titolo dell'applicazione visualizzato in Gestione report.  
  
-   [Disattivare Gestione report](#DisableRM)  
  
     Quando si installa un'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che usa la modalità nativa, Gestione report è abilitato per impostazione predefinita. È tuttavia possibile disabilitarlo se si dispone di un'applicazione front-end personalizzata con una funzionalità equivalente, se si intende usare solo le interfacce SOAP o Accesso con URL per accedere al server di report o se si usa Gestione report da un'istanza del server di report diversa.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per utilizzare Gestione report, è necessario che vengano soddisfatti i prerequisiti seguenti:  
  
-   È necessario disporre di una configurazione minima del server di report. Per altre informazioni sulla configurazione minima di un server di report, vedere [Configurare un server di report &#40;modalità nativa di Reporting Services&#41;](configure-a-report-server-reporting-services-native-mode.md).  
  
-   Il server di report deve essere eseguito in modalità nativa. Non è possibile utilizzare Gestione report con un server di report configurato per la modalità integrata SharePoint. In SQL Server 2013 non è possibile passare un server di report da una modalità all'altra. Se si desidera modificare il tipo di server di report utilizzato dall'ambiente, è necessario installare la modalità desiderata del server di report desiderato e copiare o spostare gli elementi del report dal server di report precedente in quello nuovo. Questo processo viene in genere chiamato 'migrazione'. I passaggi necessari per eseguire la migrazione dipendono dalla modalità con cui si esegue questa operazione e dalla versione dalla quale si esegue la migrazione. Per ulteriori informazioni, vedere [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   È necessario disporre anche di Internet Explorer 7.0 o versione successiva con gli script abilitati. Per altre informazioni, vedere [Planning for Reporting Services e supporto Browser per Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
##  <a name="ConfigureRMURL"></a> Configurare Gestione report per l'utilizzo dell'URL predefinito  
 Per impostazione predefinita, l'URL di Gestione report è costituito da un nome di directory virtuale univoco, oltre che dalla porta e dal nome host definito per il servizio Web ReportServer eseguito nella stessa istanza. Nella maggior parte dei casi, il nome host corrisponde al nome di rete del computer del server di report, ma può anche essere un indirizzo IP o l'intestazione host che si risolve nel computer. Per configurare Gestione report per l'utilizzo dell'URL predefinito, usare la pagina **URL Gestione report** dello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>Per configurare l'URL di Gestione report predefinito e la directory virtuale  
  
1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi all'istanza del server di report.  
  
2.  Nello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , fare clic su **URL Gestione report** per aprire la pagina per la configurazione dell'URL.  
  
3.  Immettere un nome di directory virtuale univoco per Gestione report.  
  
4.  Fare clic su **Applica**.  
  
5.  Se si utilizza [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] o Windows Server 2008, potrebbe essere necessario completare altri passaggi per utilizzare Gestione report. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="ConfigureSpecificURL"></a> Configurare Gestione report per l'utilizzo dell'URL di un server di report specifico  
 Quando si configurano gli URL nello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , Gestione report rileva e utilizza automaticamente gli URL nuovi e aggiornati per il server di report eseguito nella stessa istanza del server. Se la distribuzione richiede l'utilizzo di un unico URL statico per tutte le richieste del server di report, è possibile specificare tale URL nel file RSReportServer.config.  
  
#### <a name="to-configure-a-static-report-server-url"></a>Per configurare un URL di un server di report statico  
  
1.  Aprire il file **RSReportServer.config** in un editor di testo. Per impostazione predefinita, il percorso di questo file è \Programmi\Microsoft SQL Server\MSRS12.\<*nomeistanza*>\Reporting Services\ReportServer.  
  
2.  Individuare `ReportServerURL`.  
  
3.  Sostituirlo con l'URL dell'istanza del server di report.  
  
4.  Salvare le modifiche, quindi chiudere il file.  
  
 Per altre informazioni sul file di configurazione, vedere [modificare un File di configurazione di Reporting Services &#40;RSReportServer. config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md) e [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).  
  
##  <a name="ConfigureRemoteRS"></a> Configurare Gestione report per l'utilizzo di un server di report remoto  
 Per le configurazioni di distribuzione in cui Gestione report e il server di report si trovano in computer diversi, è necessario disporre di due installazioni distinte di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Gestione report è incorporato nel servizio del server di report e non può essere installato separatamente. Se si desidera eseguire Gestione report in un computer diverso all'interno di un proprio processo, è necessario installare un secondo server di report. Entrambe le istanze del server devono essere server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>Per connettere Gestione report a un'istanza del server di report remoto  
  
1.  Installare due istanze del server di report.  
  
2.  Configurare la prima installazione che ospiterà il server di report:  
  
    1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Fare clic su **URL servizio Web** per configurare un nome host, una porta e una directory virtuale per il server di report.  
  
    3.  Fare clic su **Database** per configurare il database del server di report.  
  
3.  Configurare la seconda installazione che ospiterà Gestione report:  
  
    1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Fare clic su **URL Gestione report** per immettere un nome di directory virtuale per Gestione report.  
  
     Non configurare il database. Non testare gli URL.  
  
4.  Nel computer di Gestione report modificare le impostazioni di configurazione in RSReportServer.config in modo da puntare all'istanza del server di report remoto. All'avvio, Gestione report leggerà il file di configurazione per ottenere l'URL del server di report:  
  
    1.  Aprire RSReportServer.config in un editor di testo. Per impostazione predefinita, si trova in \Programmi\Microsoft SQL Server\MSRS11. \< *instancename*> Services\ReportServer.  
  
    2.  Individuare `ReportServerURL`.  
  
    3.  Sostituirlo con l'URL dell'istanza del server di report remoto.  
  
    4.  Salvare le modifiche, quindi chiudere il file.  
  
5.  > [!TIP]  
    >  Se necessario, abilitare la porta 80 su entrambi i computer per consentire le richieste tramite tale porta. Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](configure-a-firewall-for-report-server-access.md).  
  
6.  Riavviare il server di report.  
  
7.  Aprire Gestione report in una finestra del browser. Se già è aperto, aggiornare il browser per verificare che Gestione report sia connesso al server remoto. Verrà visualizzato il contenuto del server di destinazione.  
  
8.  Disabilitare le caratteristiche server non utilizzate:  
  
    -   Nel computer di Gestione report disabilitare `WebServiceAndHTTPAccessEnabled` e `ScheduleEventsAndReportDeliveryEnabled`.  
  
    -   Nel computer del server di report disabilitare `ReportManagerEnabled`.  
  
 Per altre informazioni sulla disabilitazione delle funzionalità, vedere [Abilitare o disabilitare le funzionalità di Reporting Services](turn-reporting-services-features-on-or-off.md).  
  
##  <a name="ModifyTitle"></a> Personalizzare gli stili o il titolo dell'applicazione  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] non supporta la personalizzazione dei fogli di stile di Gestione report non è supportata. È tuttavia possibile modificare gli stili se si è esperti di sviluppo Web, tenendo conto dei rischi che questa operazione comporta. Per altre informazioni sui file che contengono informazioni sullo stile, vedere [Personalizzare i fogli di stile per il visualizzatore HTML e Gestione report](../customize-style-sheets-for-html-viewer-and-report-manager.md).  
  
 A Gestione report è associato un titolo di applicazione visualizzato nella parte superiore della pagina. Il titolo predefinito è **SQL Server Reporting Services**, ma è possibile personalizzarlo. A tale scopo, utilizzare la pagina Impostazioni sito di Gestione report. Per modificare le impostazioni dell'applicazione in Gestione report, è necessario disporre del ruolo **Amministratore sistema** per impostare le proprietà nella pagina Impostazioni sito. Per visualizzare il titolo dell'applicazione, è necessario disporre del ruolo **Utente sistema** .  
  
#### <a name="to-modify-application-title"></a>Per modificare il titolo dell'applicazione  
  
1.  Accedere usando un account con autorizzazioni di **Amministratore sistema** sul server di report.  
  
2.  Aprire Internet Explorer.  
  
3.  Immettere l'URL di Gestione report. Per impostazione predefinita, l'URL è http://\<**nome-server**>/reports, ma se Reporting Services è stato installato come istanza denominata, l'URL predefinito sarà http://\<**nome-server**>/reports\<**_nomeistanza**>.  
  
4.  Fare clic su **Impostazioni sito**.  
  
5.  Nella scheda **Generale** sostituire **SQL Server Reporting Services**con un nome diverso in **Nome** .  
  
6.  Fare clic su **Applica**.  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 È possibile disattivare Gestione report se si dispone di un'applicazione personalizzata che offre funzionalità equivalenti oppure se si utilizza l'applicazione Gestione report di un'istanza di servizio diversa. Per disattivare Gestione report, è possibile modificare il file RSReportServer.config.  
  
#### <a name="to-turn-off-report-manager"></a>Per disattivare Gestione report  
  
1.  Aprire il file RSReportServer.config in un editor di testo. Per impostazione predefinita, si trova in \Programmi\Microsoft SQL Server\MSRS11. \< *instancename*> Services\ReportServer.  
  
2.  Individuare **IsReportManagerEnabled**.  
  
3.  Impostare il valore su **False**.  
  
4.  Salvare le modifiche, quindi chiudere il file.  
  
 Per altre informazioni come modificare il file di configurazione, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md). Per altre informazioni sulla disabilitazione delle funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Abilitare o disabilitare le funzionalità di Reporting Services](turn-reporting-services-features-on-or-off.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Pianificazione per Reporting Services e supporto Browser per Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Verificare un'installazione di Reporting Services](../install-windows/verify-a-reporting-services-installation.md)   
 [Personalizzare i fogli di stile per il visualizzatore HTML e Gestione report](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Abilitare o disabilitare le funzionalità di Reporting Services](turn-reporting-services-features-on-or-off.md)   
 [Gestione di un server di report in modalità nativa](manage-a-reporting-services-native-mode-report-server.md)   
 [File di configurazione RSReportServer](rsreportserver-config-configuration-file.md)   
 [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  
