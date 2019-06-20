---
title: Confronto tra i server di report di Reporting Services in SharePoint e nativa | Microsoft Docs
ms.date: 06/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f7a75f578c025386966fc4fc7a15c41e7e44e0a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "67038021"
---
# <a name="comparing-native-and-sharepoint-reporting-services-report-servers"></a>Confronto tra i server di report di Reporting Services in SharePoint e nativa

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Questo articolo offre informazioni sull'elemento centrale di un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services, costituito da un motore di elaborazione insieme a estensioni per l'aggiunta di funzionalità.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

Un server di report di Reporting Services viene eseguito in una delle due modalità di distribuzione: nativa o SharePoint. Vedere la sezione [Confronto tra le funzionalità delle modalità SharePoint e nativa](#feature-comparison-of-sharepoint-and-native-mode) per un confronto delle funzionalità.  
  
 **Installazione:** per informazioni sull'installazione di Reporting Services, vedere [Installare Reporting Services](../install-windows/install-reporting-services.md).

## <a name="overview-of-report-server-modes"></a>Panoramica delle modalità del server di report

 I motori di elaborazione (processori) sono l'elemento fondamentale del server di report. Supportano l'integrità del sistema di reporting e non possono essere modificati né estesi. Anche le estensioni sono processori, ma eseguono funzioni molto specifiche. Reporting Services include una o più estensioni predefinite per ogni tipo di estensione supportata. È possibile aggiungere estensioni personalizzate a un server di report. In questo modo è possibile estendere un server di report per supportare funzionalità non disponibili per impostazione predefinita, ad esempio il supporto per tecnologie Single Sign-On, l'output dei report in formati di applicazione che non sono già gestiti dalle estensioni per il rendering predefinite e il recapito dei report a una stampante o applicazione.  
  
 Una singola istanza del server di report viene definita dalla raccolta completa di componenti di elaborazione ed estensioni che forniscono l'elaborazione end-to-end, dalla gestione della richiesta iniziale alla presentazione di un report finito. Tramite i suoi sottocomponenti, il server di report elabora le richieste di report e rende disponibili i report per l'accesso su richiesta o la distribuzione pianificata.  
  
 Funzionalmente, un server di report abilita la creazione di report, il rendering di report e il recapito di report per una varietà di origini dati e schemi di autenticazione e autorizzazione estensibili. Inoltre in un server di report sono contenuti i relativi database in cui vengono archiviati i report pubblicati, le origini dati condivise, i set di dati condivisi, le parti del report, le sottoscrizioni e le pianificazioni condivise, i file di origine della definizione di report, le definizioni dei modelli, i report compilati, gli snapshot, i parametri e altre risorse. Un server di report abilita anche l'amministrazione per la configurazione del server di report per elaborare le richieste del report, gestire le cronologie degli snapshot e gestire le autorizzazioni per report, origini dati, set di dati e sottoscrizioni.  
  
 Un server di report di Reporting Services supporta due modalità per la distribuzione delle istanze di server di report:  
  
-   **Modalità nativa**: compresa la modalità nativa con web part di SharePoint, in cui un server di report viene eseguito come server applicazioni che offre tutte le funzionalità di elaborazione e gestione esclusivamente tramite i componenti di Reporting Services. Un server di report in modalità nativa può essere configurato con Gestione configurazione di Reporting Services e SQL Server Management Studio.  
  
-   **Modalità SharePoint**, in cui un server di report viene installato come parte di una server farm di SharePoint.  Distribuire e configurare la modalità SharePoint usando i comandi PowerShell o le pagine di gestione del contenuto di SharePoint.  
  
 In SQL Server Reporting Services non è possibile passare un server di report da una modalità all'altra. Se si desidera modificare il tipo di server di report usato dall'ambiente, è necessario installare la modalità desiderata del server di report e copiare o spostare gli elementi del report o il database del server di report dal server di report precedente in quello nuovo. Questo processo viene in genere chiamato 'migrazione'. I passaggi necessari per eseguire la migrazione dipendono dalla modalità con cui si esegue questa operazione e dalla versione dalla quale si esegue la migrazione. Per altre informazioni, vedere [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
## <a name="feature-comparison-of-sharepoint-and-native-mode"></a>Confronto tra le funzionalità delle modalità SharePoint e nativa
  
|Funzionalità o componente|Modalità nativa|Modalità SharePoint|  
|--------------------------|-----------------|---------------------|  
|**Indirizzamento tramite URL**|Sì|L'indirizzamento tramite URL è diverso nella modalità integrata SharePoint. Per fare riferimento a report, modelli di report, origini dati condivise e risorse vengono usati gli URL di SharePoint. La gerarchia di cartelle del server di report non viene usata. Se si dispone di applicazioni personalizzate che si basano sull'accesso all'URL supportato in un server di report in modalità nativa, questa funzionalità non sarà più disponibile quando il server di report è configurato per l'integrazione con SharePoint.<br /><br /> Per altre informazioni sull'accesso all'URL, vedere [Riferimento ai parametri di accesso con URL](../../reporting-services/url-access-parameter-reference.md)|  
|**Estensioni di sicurezza personalizzate**|Sì|Le estensioni di sicurezza personalizzate di Reporting Services non possono essere distribuite o usate nel server di report. Il server di report include una speciale estensione di sicurezza, che viene usata quando si configura un server di report per l'esecuzione in modalità di integrazione con SharePoint. Tale estensione di sicurezza è un componente interno ed è necessaria per le operazioni in modalità integrata.|  
|**Gestione configurazione**|Sì|**\*\* Importante \*\*** Non è possibile usare Gestione configurazione per gestire un server di report in modalità SharePoint. Usare invece Amministrazione centrale SharePoint.|  
|**Portale Web**|Sì|Non è possibile gestire in modalità SharePoint nel portale web. Usare le pagine dell'applicazione SharePoint. Per altre informazioni, vedere [Servizio SharePoint di Reporting Services e applicazioni di servizio](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).|  
|**Report collegati**|Sì|No.|  
|**Report personali**|Sì|no|  
|**Sottoscrizioni personali** e metodi di invio in batch|Sì|no|  
|**Avvisi dati**|no|Sì|  
|**Power View**|no|Sì<br /><br /> È necessario disporre di Silverlight nel browser del client. Per altre informazioni sui requisiti del browser, vedere [Supporto browser per Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)|  
|**Report RDL**|Sì|Sì<br /><br /> I report RDL possono essere eseguiti nei server di report di Reporting Services in modalità nativa o SharePoint.|  
|**Report RDLX**|no|Sì<br /><br /> I report RDLX di Power View possono essere eseguiti solo nei server di report di Reporting Services in modalità SharePoint.|  
|**Credenziali del token utente di SharePoint per l'estensione dell'elenco SharePoint**|no|Sì|  
|**Aree AAM per distribuzioni che si interfacciano a Internet**|no|Sì|  
|**Backup e recupero di SharePoint**|no|Sì|  
|**Supporto del log ULS**|no|Sì|  
  
## <a name="native-mode"></a>Modalità nativa

 In modalità nativa un server di report è un server applicazioni autonomo che fornisce tutte le funzionalità necessarie per la visualizzazione, la gestione, l'elaborazione e il recapito di report e modelli di report. Questa è la modalità predefinita per le istanze del server di report. È possibile installare un server di report in modalità nativa configurato durante l'installazione oppure configurarlo per le operazioni in modalità nativa al termine dell'installazione.  
  
 Nel diagramma riportato di seguito è illustrata l'architettura a tre livelli di una distribuzione in modalità nativa di Reporting Services. Vengono mostrati il database del server di report e le origini dati nel livello dati, i componenti del server di report nel livello intermedio e le applicazioni client e gli strumenti predefiniti o personalizzati nel livello di presentazione. Viene inoltre illustrato il flusso delle richieste e dei dati tra i componenti server, indicando quali componenti gestiscono l'invio e il recupero di contenuto da un archivio dati.  
  
 ![Architettura di Reporting Services](../../reporting-services/report-server-sharepoint/media/reporting-serv-arch.gif "Architettura di Reporting Services")  
  
 Il server di report viene implementato come un servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] di Windows, denominato "servizio del server di report", che ospita un servizio Web, l'elaborazione in background e altre operazioni. Nell'applicazione console Servizi, il servizio è elencato come SQL Server Reporting Services (MSSQLSERVER).  
  
 Sviluppatori di terze parti possono creare estensioni aggiuntive per sostituire o estendere la capacità di elaborazione del server di report. Per altre informazioni sulle interfacce programmatiche disponibili per gli sviluppatori di applicazioni, vedere il [Riferimento tecnico](../../reporting-services/technical-reference-ssrs.md).  
  
### <a name="native-mode-with-sharepoint-web-parts"></a>Modalità nativa con web part di SharePoint

 Reporting Services offre due web part che è possibile installare e registrare in un'istanza di [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 o versioni successive o di SharePoint Portal Server 2003 o versioni successive. Da un sito di SharePoint è possibile usare le web part per trovare e visualizzare report archiviati ed elaborati in un server di report eseguito in modalità nativa. Le web part sono state introdotte nelle versioni precedenti di Reporting Services.  
  
## <a name="sharepoint-mode"></a>Modalità SharePoint

 In modalità SharePoint è necessario che un server di report venga eseguito all'interno di una server farm di SharePoint. Le funzionalità di elaborazione, rendering e gestione del server di report sono rappresentate da un server applicazioni SharePoint in cui vengono eseguiti il servizio condiviso SharePoint di Reporting Services e una o più applicazioni di servizio di Reporting Services. Un sito di SharePoint fornisce l'accesso front-end al contenuto e alle operazioni del server di report.  
  
 La modalità SharePoint richiede quanto indicato di seguito:  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   Versione appropriata del componente aggiuntivo Reporting Services per i prodotti SharePoint 2010.  
  
-   Un server applicazioni SharePoint in cui sia installato il servizio condiviso Reporting Services e sia disponibile almeno un'applicazione di servizio di Reporting Services.  
  
 La figura seguente illustra un ambiente Reporting Services in modalità SharePoint:  
  
 ![Architettura funzionale di SharePoint SSRS](../../reporting-services/report-server-sharepoint/media/rs-sharepoint-architecture.gif "Architettura funzionale di SharePoint SSRS")  
  
||Descrizione|  
|-|-----------------|  
|**(1)**|Server Web o front-end Web (WFE). Il componente aggiuntivo Reporting Services deve essere installato in ogni server Web da cui si vuole usare le funzionalità di applicazione Web, ad esempio la visualizzazione di report o le pagine di gestione di Reporting Services per attività quali la gestione delle origini dati o delle sottoscrizioni.|  
|**(2)**|Con il componente aggiuntivo vengono installati endpoint URL e SOAP per consentire la comunicazione tra i client e i server applicazioni tramite il proxy del servizio di Reporting Services.|  
|**(3)**|Server applicazioni in cui è in esecuzione il servizio condiviso di Reporting Services. La distribuzione con scalabilità orizzontale dell'elaborazione del report viene gestita come parte della farm SharePoint e aggiungendo il servizio Reporting Services a ulteriori server applicazioni.|  
|**(4)**|È possibile creare più applicazioni di servizio di Reporting Services con configurazioni diverse, inclusi autorizzazioni, messaggi di posta elettronica, proxy e sottoscrizioni.|  
|**(5)**|Report, origini dati e altri elementi vengono archiviati nei database del contenuto di SharePoint.|  
|**(6)**|Le applicazioni di servizio di Reporting Services creano tre database per le funzionalità di server di report, temporanee e di avvisi dati. Le impostazioni di configurazione che si applicano a tutte le applicazioni di servizio SSRS vengono archiviate nel file **RSReportserver.config** .|  
  
## <a name="report-process-and-schedule-and-delivery-process"></a>Elaborazione di report e processo di pianificazione e recapito

 Nel server di report sono disponibili due motori di elaborazione tramite cui vengono eseguite l'elaborazione preliminare e intermedia dei report e le operazioni pianificate e di recapito. Il componente Elaborazione report gestisce il recupero della definizione o del modello del report e l'integrazione delle informazioni sul layout con i dati provenienti dall'estensione per l'elaborazione dati e ne esegue il rendering nel formato richiesto. Con il componente Elaborazione pianificazione e recapito è possibile elaborare i report generati da una pianificazione e recapitarli alle destinazioni.  
  
## <a name="report-server-database"></a>Database del server di report

 Il server di report è un server senza stato che archivia tutte le proprietà, gli oggetti e i metadati in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nei dati archiviati sono inclusi i report pubblicati e compilati, i modelli di report e la gerarchia di cartelle in cui è disponibile l'indirizzamento per tutti gli elementi gestiti dal server di report. Un database del server di report può offrire lo spazio di archiviazione interno per una singola installazione di Reporting Services o per più server di report che fanno parte di una distribuzione con scalabilità orizzontale. Se un server di report viene configurato per l'esecuzione in una distribuzione più ampia di un prodotto o una tecnologia SharePoint, vengono usati i database SharePoint in aggiunta al database del server di report. Per altre informazioni sugli archivi dati utilizzati nell'installazione di Reporting Services, vedere [Report Server Database &#40;SSRS Native Mode&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md).  
  
## <a name="authentication-rendering-data-and-delivery-extensions"></a>Estensioni per le operazioni di autenticazione, rendering, elaborazione dati e recapito

 Il server di report supporta le estensioni per l'autenticazione, l'elaborazione dati, l'elaborazione di report, il rendering e il recapito. Un server di report richiede almeno un'estensione di autenticazione, un'estensione per l'elaborazione dati e un'estensione per il rendering. Le estensioni personalizzate di elaborazione dei report e di recapito sono facoltative. Sono tuttavia necessarie se si desidera supportare la distribuzione dei report o controlli personalizzati.  
  
 In Reporting Services sono disponibili estensioni predefinite che consentono di utilizzare tutte le funzionalità del server senza la necessità di sviluppare componenti personalizzati. Nella tabella seguente sono descritte le estensioni predefinite che concorrono a formare un'istanza del server di report completa con funzionalità immediatamente disponibili per l'utilizzo:  
  
|Tipo|Default|  
|----------|-------------|  
|Autenticazione|Un'istanza del server di report predefinita supporta l'autenticazione di Windows, incluse le funzionalità di rappresentazione e delega, se abilitate nel dominio.|  
|Elaborazione dati|In un'istanza del server di report predefinita sono incluse le estensioni per l'elaborazione dati per origini dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion Essbase, SAPBW, OLE DB, Parallel Data Warehouse e ODBC.|  
|Rendering|In un'istanza del server di report predefinita sono incluse le estensioni per il rendering di file HTML, Excel, CSV, XML, immagine, Word, elenco SharePoint e PDF.|  
|Recapito|Un'istanza del server di report predefinita include un'estensione per il recapito tramite posta elettronica e un'estensione per il recapito tramite condivisione di file. Se il server di report è configurato per l'integrazione con SharePoint, è possibile utilizzare un'estensione per il recapito tramite cui è possibile salvare report in una raccolta di SharePoint.|  
  
> [!NOTE]  
>  In Reporting Services è incluso un set completo di strumenti e applicazioni che è possibile usare per amministrare il server, creare contenuto e renderlo disponibile per gli utenti dell'organizzazione.  
  
## <a name="related-tasks"></a>Attività correlate

 Negli articoli seguenti vengono fornite altre informazioni relative a installazione, uso e gestione di un server di report:  
  
|Attività|Collegamento|  
|----------|----------|  
|Verificare i requisiti hardware e software.|[Hardware and Software Requirements for Reporting Services in SharePoint Mode](https://msdn.microsoft.com/library/ed91877d-4f74-4266-a932-b824b4810c99).|  
|Installare la modalità SharePoint di Reporting Services.|[Installare la modalità SharePoint di Reporting Services per SharePoint 2010](https://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)|  
|Illustra come ottimizzare le impostazioni di memoria per il servizio Web ReportServer e il servizio Windows.|[Configurare la memoria disponibile per applicazioni del server di report](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)|  
|Vengono illustrati i passaggi consigliati per configurare il server di report per l'amministrazione remota.|[Configurare un server di report per l'amministrazione remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)|  
|Vengono fornite istruzioni per la configurazione della disponibilità della funzionalità **Report personali** in un'istanza del server di report nativa.|[Abilitare e disabilitare la funzionalità Report personali](../../reporting-services/report-server/enable-and-disable-my-reports.md)|  
|Vengono fornite istruzioni per la configurazione del controllo RSClientPrint tramite cui viene fornita la funzionalità di stampa nei browser supportati. Per altre informazioni sui requisiti del browser, vedere [Supporto browser per Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).|[Abilitare e disabilitare la stampa sul lato client per Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  

## <a name="next-steps"></a>Passaggi successivi

[Estensioni di Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
[Strumenti di Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
[Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
[Database del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Implementazione di un'estensione di sicurezza](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[Implementazione di un'estensione per l'elaborazione dati](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
[Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
