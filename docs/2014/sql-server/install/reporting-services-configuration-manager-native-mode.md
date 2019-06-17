---
title: Gestione configurazione Reporting Services (modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bbd786485915405de36511f5710e3490bdfd8a3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092654"
---
# <a name="reporting-services-configuration-manager-native-mode"></a>Gestione configurazione Reporting Services (modalità nativa)
  Utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurare un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa. Se si è installato un server di report mediante l'opzione di installazione di tipo "solo file", è necessario utilizzare Gestione configurazione per configurare il server prima di poterlo utilizzare. Se si è installato un server di report mediante l'opzione di installazione della configurazione predefinita, è possibile utilizzare Gestione configurazione per verificare o modificare le impostazioni specificate durante l'installazione. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurare un'istanza remota o locale di un server di report.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  A partire dalla versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è progettato per gestire server di report in modalità SharePoint. La modalità SharePoint viene gestita e configurata tramite Amministrazione centrale SharePoint gli e script di PowerShell. Per informazioni, vedere [installazione in modalità SharePoint di Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
 **Contenuto della sezione:**  
  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
 Vengono fornite indicazioni e procedure su come modificare l'account e la password del servizio.  
  
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
 Viene descritto come configurare gli URL usati per accedere al servizio Web ReportServer e a Gestione report.  
  
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
 Descrive come creare un database del server di report necessario per l'archiviazione di oggetti e metadati del server.  
  
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
 Descrive come modificare la stringa di connessione usata dal server di report per la connessione al database.  
  
 [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
 Descrive come configurare un account utente per l'esecuzione automatica dei report.  
  
 [Configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Descrive come configurare un server di report in modo da supportare la distribuzione dei report tramite posta elettronica.  
  
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Vengono fornite informazioni sulla configurazione di più istanze del server di report per l'utilizzo di un database del server di report condiviso.  
  
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
 Viene illustrato come usare e gestire le chiavi di crittografia usate per l'archiviazione di dati sensibili.  
  
 [Gestire un server di report in modalità nativa di Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
 Include istruzioni dettagliate su alcune attività comuni.  
  
 [Gli argomenti della Guida F1 di Gestione configurazione di Reporting Services &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
 Sono inclusi gli argomenti della Guida relativi alle pagine dello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Contenuto dell'argomento:**  
  
-   [Scenari di utilizzo di Gestione configurazione Reporting Services](#bkmk_scenarios)  
  
-   [Requisiti](#bkmk_requirements)  
  
-   [Per avviare Gestione configurazione Reporting Services](#bkmk_start_configuration_manager)  
  
##  <a name="bkmk_scenarios"></a> Scenari di utilizzo di Gestione configurazione Reporting Services  
 Tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è possibile effettuare le attività seguenti:  
  
-   Configurare l'account del servizio del server di report. Questo account viene inizialmente configurato durante l'installazione, ma può essere modificato tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se la password viene aggiornata o si desidera utilizzare un account diverso.  
  
-   Creare e configurare URL. Il server di report e Gestione report sono applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] alle quali è possibile accedere tramite URL. L'URL del server di report fornisce l'accesso agli endpoint di SOAP del server di report. L'URL di Gestione report viene utilizzato per aprire Gestione report. È possibile configurare un solo URL o più URL per ogni applicazione.  
  
-   Creare e configurare il database del server di report. Il server di report è un server senza stato che richiede un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per lo spazio di archiviazione interno. Per creare il database del server di report e configurare una connessione al database del server di report, è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È anche possibile selezionare un database del server di report esistente in cui è già incluso il contenuto che si desidera utilizzare.  
  
-   Configurare una distribuzione con scalabilità orizzontale in modalità nativa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta una topologia di distribuzione che consente a più istanze del server di report di utilizzare un singolo database del server di report condiviso. Per distribuire un server di report con scalabilità orizzontale, utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per connettere ogni server di report al database del server di report condiviso.  
  
-   Eseguire il backup, il ripristino o la sostituzione della chiave simmetrica utilizzata per crittografare stringhe di connessione e credenziali archiviate. È necessario disporre di un backup della chiave simmetrica se si modifica l'account del servizio o si sposta un database del server di report in un altro computer.  
  
-   Configurazione dell'account di esecuzione automatica. Questo account viene utilizzato per le connessioni remote durante le operazioni pianificate o quando non sono disponibili credenziali utente.  
  
-   Consente di configurare la posta elettronica del server di report. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per il recapito tramite posta elettronica del server di report che usa SMTP (Simple Mail Transfer Protocol) per recapitare report o notifiche di elaborazione di report in una cassetta postale elettronica. È possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per specificare quale server o gateway SMTP nella rete dovrà essere utilizzato per il recapito tramite posta elettronica.  
  
 Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente di gestire il contenuto del server di report, abilitare funzionalità aggiuntive o concedere l'accesso al server. La distribuzione completa richiede anche l'utilizzo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per abilitare funzionalità aggiuntive o modificare valori predefiniti e di Gestione report per concedere l'accesso utente al server.  
  
##  <a name="bkmk_requirements"></a> Requisiti  
 Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è uno strumento specifico della versione. Non è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato con questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per configurare una versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se si eseguono versioni precedenti e più recenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità side-by-side nello stesso computer, sarà necessario utilizzare Gestione configurazione Reporting Services fornito con ogni versione per configurare ciascuna istanza.  
  
 Per utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario disporre di quanto segue:  
  
-   Autorizzazioni di amministratore di sistema locale nel computer in cui è ospitato il server di report da configurare. Se si sta configurando un computer remoto, è necessario disporre delle autorizzazioni di amministratore di sistema locale anche in questo computer.  
  
-   È necessario disporre dell'autorizzazione per la creazione di database nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database del server di report.  
  
-   Il servizio WMI (Windows Management Instrumentation) deve essere attivato e in esecuzione nel server di report che si sta configurando. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza il provider WMI del server di report per la connessione ai server di report locali e remoti. Se si sta configurando un server di report remoto, il computer deve consentire l'accesso remoto a WMI. Per altre informazioni, vedere [Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
-   Prima di poter connettersi a un'istanza remota del server di report e configurarla, è necessario abilitare il passaggio delle chiamate di Strumentazione gestione Windows (WMI) attraverso Windows Firewall. Per altre informazioni, vedere [Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato automaticamente durante l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
##  <a name="bkmk_start_configuration_manager"></a> Per avviare Gestione configurazione Reporting Services  
  
#### <a name="to-start-reporting-services-configuration"></a>Per avviare la configurazione di Reporting Services  
  
1.  Effettuare il passaggio riportato di seguito appropriato alla versione di Microsoft Windows in uso:  
  
    -   Nella schermata iniziale di Windows digitare **Reporting** e nei risultati di ricerca selezionare **Gestione configurazione Reporting Services** .  
  
    -   Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], quindi **Strumenti di configurazione**.  
  
         Se si desidera configurare un'istanza del server di report di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aprire la cartella del programma per la versione specifica. Selezionare, ad esempio, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] anziché [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] per aprire gli strumenti di configurazione per i componenti server di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
         Fare clic su **Gestione configurazione Reporting Services**.  
  
2.  Verrà visualizzata la finestra di dialogo **Connessione configurazione Reporting Services** in cui è possibile selezionare l'istanza del server di report che si desidera configurare. Fare clic su **Connetti**.  
  
3.  In **Nome server**specificare il nome del computer in cui è installata l'istanza del server di report. Per impostazione predefinita, viene visualizzato il nome del computer locale, ma è possibile digitare il nome di un'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se si desidera connettersi a un server di report installato in un computer remoto.  
  
4.  Se si specifica un computer remoto, fare clic su **Trova** per stabilire una connessione.  
  
5.  In **Istanza server di report**selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si desidera configurare. Nell'elenco sono visualizzate solo le istanze del server di report relative a questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Non è possibile configurare versioni precedenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
6.  Fare clic su **Connetti**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Strumenti di Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Configurare e amministrare un server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
