---
title: Installare Reporting Services Server di Report in modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f0c52d22f9592d149f25f6ae8a6de2813dfcba1d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043292"
---
# <a name="install-reporting-services-native-mode-report-server"></a>Installare un server di report in modalità nativa di Reporting Services
  Un server di report in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] può essere installato dall'installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dalla riga di comando. Nell'Installazione guidata è possibile scegliere di installare i file e di configurare il server con le impostazioni predefinite oppure di installare solo i file e di non configurare il server. In questo argomento viene esaminata la *configurazione predefinita per la modalità nativa* in cui tramite il programma di installazione viene sia installata e configurata un'istanza del server di report. Al termine dell'installazione, il server di report è in esecuzione e pronto per essere utilizzato. Un server di report in modalità nativa viene eseguito come server applicazioni autonomo. La modalità nativa è la modalità predefinita del server.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
##  <a name="bkmk_top"></a> Contenuto dell'argomento  
  
-   [Che cos'è la configurazione predefinita?](#bkmk_whatisdefaultconfiguration)  
  
-   [Casi in cui installare la configurazione predefinita per la modalità nativa](#bkmk_whentoinstalldefaultconfig)  
  
-   [Requisiti](#bkmk_requirements)  
  
-   [Prenotazioni URL predefinite](#bkmk_defaultURLreservations)  
  
-   [Installare la modalità nativa con l'installazione guidata SQL Server](#bkmk_installwithwizard)  
  
-   [Installare la modalità nativa con la riga di comando](#bkmk_commandline)  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> Che cos'è la configurazione predefinita?  
 Tramite l'installazione vengono installate le seguenti funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] quando si seleziona l'opzione di configurazione predefinita per la modalità nativa:  
  
-   Il servizio del server di report (che include il servizio Web ReportServer, l'applicazione di elaborazione in background e Gestione report)  
  
-   Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Le utilità della riga di comando di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe e rs.exe)  
  
 Tale opzione non si applica alle funzionalità condivise, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], che, se installate, devono essere specificate come elementi distinti.  
  
 Per un'installazione del server di report in modalità nativa, il programma di installazione configura gli elementi seguenti:  
  
-   Account del servizio del server di report.  
  
-   URL del servizio Web ReportServer.  
  
-   URL di Gestione report.  
  
-   Database del server di report.  
  
-   Accesso dell'account del servizio ai database del server di report.  
  
-   Connessione DNS per i database del server di report.  
  
 Tramite il programma di installazione non viene configurato l'account di esecuzione automatica, la posta elettronica del server di report, il backup delle chiavi di crittografia o una distribuzione con scalabilità orizzontale. Per configurare queste proprietà, è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Casi in cui installare la configurazione predefinita per la modalità nativa  
 Una configurazione predefinita comporta l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un stato operativo, che consente di utilizzare immediatamente il server di report al termine dell'installazione. Specificare questa modalità se si desidera ridurre il numero di passaggi, eliminando tutte le attività di configurazione altrimenti necessarie nello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 L'installazione della configurazione predefinita non garantisce il corretto funzionamento del server di report al termine dell'installazione. All'avvio del servizio, potrebbe non essere possibile registrare gli URL predefiniti. Eseguire sempre il test dell'installazione per verificare che il servizio venga avviato ed eseguito nel modo previsto.  
  
##  <a name="bkmk_requirements"></a> Requisiti  
 L'opzione di configurazione predefinita consente di utilizzare i valori predefiniti per configurare le impostazioni principali necessarie per rendere operativo un server di report. Di seguito vengono indicati i requisiti per questa opzione di installazione:  
  
-   È consigliabile soddisfare i requisiti hardware e software minimi per l'esecuzione di Microsoft SQL Server. Per ulteriori informazioni, vedere [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] devono essere installati insieme nella stessa istanza. Nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene ospitato il database del server di report creato e configurato dal programma di installazione.  
  
-   L'account utente utilizzato per eseguire il programma di installazione deve appartenere al gruppo Administrators locale e deve disporre dell'autorizzazione per accedere e creare i database nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita i database del server di report.  
  
-   Il programma di installazione deve essere in grado di utilizzare i valori predefiniti per riservare gli URL necessari per accedere al server di report e a Gestione report. Questi valori sono la porta 80, un carattere jolly complesso e i nomi delle directory virtuali nel formato **ReportServer_\<***nome_istanza***>** e **Reports_\<***nome_istanza***>**.  
  
-   È necessario poter utilizzare i valori predefiniti con il programma di installazione per creare i database del server di report. Tali valori sono **ReportServer** e **ReportServerTempDB**. Se sono presenti database esistenti da un'installazione precedente, il programma di installazione si blocca perché non è in grado di configurare il server di report nella configurazione predefinita per la modalità nativa. Per sbloccare il programma di installazione, è necessario rinominare, spostare o eliminare i database.  
  
 Se il computer non soddisfa tutti i requisiti per un'installazione predefinita, è necessario installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità "solo file", quindi utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurarlo al termine dell'installazione.  
  
 Non tentare di riconfigurare il computer solo per consentire il proseguimento di un'installazione predefinita. Tale scelta richiederebbe diverse ore di lavoro, vanificando i vantaggi correlati al risparmio di tempo offerti in genere da questa opzione di installazione. La soluzione migliore consiste nell'installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità "solo file" e quindi configurare il server di report per l'utilizzo di valori specifici.  
  
##  <a name="bkmk_defaultURLreservations"></a> Prenotazioni URL predefinite  
 Le prenotazioni URL sono composte da un prefisso, un nome host, una porta e una directory virtuale:  
  
|Parte|Descrizione|  
|----------|-----------------|  
|Prefisso|Il prefisso predefinito è HTTP. Se in precedenza è stato installato un certificato SSL (Secure Sockets Layer), il programma di installazione tenterà di creare prenotazioni URL che utilizzano il prefisso HTTPS.|  
|Nome host|Il nome host predefinito è un carattere jolly complesso (+). Specifica che il server di report accetterà qualsiasi richiesta HTTP sulla porta designata per qualsiasi nome host risolto nel computer, tra cui http://\<nomecomputer > / reportserver, http://localhost/reportserver, o http://\<IPAddress > / ReportServer.|  
|Port|La porta predefinita è 80. Si noti che se si utilizza un numero di porta diverso da 80, sarà necessario aggiungerlo in modo esplicito all'URL quando si apre un'applicazione Web di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una finestra del browser.|  
|Directory virtuale|Per impostazione predefinita, le directory virtuali vengono create nel formato reportserver_\<*nome_istanza*> per il servizio Web ReportServer e Reports_\<*nome_istanza*> per gestione Report. Per il servizio Web ReportServer, la directory virtuale predefinita è **reportserver**. Per Gestione report, la directory virtuale predefinita è **reports**.|  
  
 Di seguito viene fornito un esempio di stringa dell'URL completa:  
  
-   http://+:80/reportserver consente l'accesso al server di report.  
  
-   http://+:80/reports, fornisce l'accesso a gestione Report.  
  
##  <a name="bkmk_installwithwizard"></a> Installare la modalità nativa con l'installazione guidata SQL Server  
 Nell'elenco seguente sono illustrati i passaggi e le opzioni specifici di  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] selezionati nell'Installazione guidata di SQL Server. Nell'elenco non vengono descritte tutte le pagine che verranno visualizzate nell'installazione guidata, bensì solo le pagine correlate a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che fanno parte di un'installazione in modalità nativa.  
  
1.  Nella pagina **Impostazione ruolo** selezionare **Installazione funzionalità SQL Server**.  
  
     ![Installazione di funzionalità di SQL Server per impostazione ruolo](../../../2014/sql-server/install/media/rs-setuprole.gif "Installazione di funzionalità di SQL Server per impostazione ruolo")  
  
2.  Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:  
  
    -   **Servizi motore di database**, a meno che non sia già installata un'istanza del motore di database.  
  
    -   **Reporting Services-nativo**.  
  
    -   **Strumenti di gestione - base**. Gli strumenti di gestione non sono obbligatori ma consigliati, a meno che non si disponga di un'altra installazione di strumenti di gestione. L'opzione di configurazione predefinito causerà un server di report funzionante, ma è possibile modificare le opzioni di configurazione in un secondo momento. Alcune opzioni, ad esempio "Report personali" vengono gestite tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
     ![Selezionare la modalità nativa di SSRS nella selezione funzionalità](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "Selezionare la modalità nativa di SSRS nella selezione funzionalità")  
  
3.  Se si intende utilizzare la funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , nella pagina **Configurazione server** è possibile verificare se SQL Server Agent è configurato per il tipo di avvio **Automatico** .  
  
4.  Nella pagina **Configurazione di Reporting Services** selezionare **Installazione e configurazione**.  
  
     ![Configurazione della modalità di SSRS](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "Configurazione della modalità nativa di SSRS")  
  
5.  Al completamento dell'installazione guidata di SQL Server, verificare l'installazione della modalità nativa predefinita tramite i passaggi di base riportati di seguito.  
  
    -   Aprire Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e verificare che sia possibile connettersi al server di report.  
  
    -   Aprire il browser con i privilegi di amministratore e connettersi a Gestione report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , ad esempio `http://loclahost/Reports`.  
  
    -   Aprire il browser con i privilegi di amministratore e connettersi alla pagina del server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Ad esempio,  `http://loclahost/ReportServer`  
  
 Per ulteriori informazioni, vedere la sezione relativa alla modalità nativa dei due argomenti seguenti:  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Risoluzione dei problemi di installazione di Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
##  <a name="bkmk_commandline"></a> Installare la modalità nativa con la riga di comando  
 Nell'esempio seguente è incluso il servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] , in quanto è necessario per una configurazione predefinita.  
  
```  
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS"   
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK   
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
 Per altre informazioni ed esempi, vedere [prompt dei comandi di installazione di Reporting Services SharePoint Mode e modalità nativa](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md) e [installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di installazione di Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Installazione di tipo "solo file" &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurare connessioni SSL in un server di report in modalità nativa](../security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Guida introduttiva all'installazione di SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
