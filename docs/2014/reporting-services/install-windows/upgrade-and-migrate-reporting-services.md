---
title: Eseguire l'aggiornamento e la migrazione di Reporting Services | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSRS, upgrading
- Reporting Services, upgrades
- SQL Server Reporting Services, upgrading
- upgrading Reporting Services
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 42cdcb1245e5280d25a94a81617da92f755ea048
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176941"
---
# <a name="upgrade-and-migrate-reporting-services"></a>Upgrade and Migrate Reporting Services

Questo argomento offre una panoramica delle opzioni di aggiornamento e migrazione per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sono disponibili due approcci generali per l'aggiornamento di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

-   **Aggiornamento:** Si aggiornano [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i componenti di nei server e nelle istanze in cui sono attualmente installati. Si tratta dell'aggiornamento comunemente definito "sul posto". L'aggiornamento sul posto non è supportato da una modalità all'altra del server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Non è possibile ad esempio eseguire l'aggiornamento da un server di report in modalità nativa a un server di report in modalità SharePoint. È possibile eseguire la migrazione degli elementi del report da una modalità all'altra. Per ulteriori informazioni, vedere la sezione "migrazione da nativa a SharePoint" più avanti in questo documento e l'argomento correlato [esempio Reporting Services script RS. exe per eseguire la migrazione del contenuto tra server di report](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).

-   **Migrate**: viene installato e configurato un nuovo ambiente SharePoint, vengono copiati gli elementi del report e le risorse nel nuovo ambiente e viene configurato il nuovo ambiente per l'utilizzo del contenuto esistente. Un tipo di migrazione di livello inferiore consiste nel copiare i database di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , i file di configurazione e, se si utilizza la modalità SharePoint, i database di contenuto di SharePoint.

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità SharePoint|

##  <a name="bkmk_top"></a>Contenuto dell'argomento:

-   [Problemi di aggiornamento noti e procedure consigliate](#bkmk_known_issues)

-   [Installazioni side-by-side](#bkmk_side_by_side)

-   [Aggiornamento sul posto](#bkmk_inplace_upgrade)

-   [Elenco di controllo pre-aggiornamento](#bkmk_upgrade_checklist)

-   [Scenari di aggiornamento e migrazione della modalità nativa](#bkmk_native_scenarios)

-   [Aggiornare una distribuzione con scalabilità orizzontale di Reporting Services in modalità nativa](#bkmk_native_scaleout)

-   [Scenari di aggiornamento e migrazione della modalità SharePoint](#bkmk_sharePoint_scenarios)

-   [Considerazioni per una migrazione](#bkmk_migration_considerations)

-   [Risorse aggiuntive](#bkmk_additional_resources)

##  <a name="bkmk_known_issues"></a>Problemi di aggiornamento noti e procedure consigliate
 Per un elenco dettagliato delle edizioni e delle versioni supportate che è possibile aggiornare, vedere [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).

> [!TIP]
>  Per le informazioni più recenti relative a problemi riguardanti [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere gli argomenti seguenti:
> 
>  -   [Note sulla versione di SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).
> -   [SQL Server Reporting Services 2014 suggerimenti, trucchi e risoluzione dei problemi](https://go.microsoft.com/fwlink/?LinkID=391254).
> -   Usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor. Per ulteriori informazioni, vedere [Reporting Services problemi di aggiornamento &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md) e [procedura: installare Preparazione aggiornamento](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_side_by_side"></a>Installazioni side-by-side
 È possibile eseguire l'installazione side-by-side della modalità nativa di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] e di una distribuzione in modalità nativa di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

 Le distribuzioni side-by-side della modalità SharePoint di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] e di qualsiasi versione precedente dei componenti della modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non sono supportate.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_inplace_upgrade"></a>Aggiornamento sul posto
 L'aggiornamento viene completato tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per aggiornare uno o tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluso [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Durante l'installazione vengono rilevate le istanze esistenti e viene richiesto di eseguire l'aggiornamento. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il programma di installazione offre diverse opzioni di aggiornamento che è possibile specificare come argomento della riga di comando o nell'Installazione guidata.

 Quando si esegue il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile selezionare l'opzione che consente di eseguire l'aggiornamento da una delle versioni seguenti oppure installare una nuova istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] che viene eseguita in modalità side-by-side insieme alle installazioni esistenti:

-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]

-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]

 Per ulteriori informazioni su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere quanto segue:

||
|-|
|[Eseguire l'aggiornamento a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)|
|[Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata &#40;&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|
|[Installare SQL Server 2014 dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)|

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_upgrade_checklist"></a>Elenco di controllo pre-aggiornamento
 Prima di effettuare l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere gli argomenti seguenti:

-   Rivedere i requisiti per determinare se l'hardware e il software in uso supportano [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Per ulteriori informazioni, vedere [Hardware and Software Requirements for Installing SQL Server 2014](../../../2014/sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

-   Utilizzare Controllo configurazione sistema (SCC) per analizzare il computer del server di report per individuare eventuali condizioni che potrebbero compromettere l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).

-   Rivedere le procedure consigliate per la sicurezza e le indicazioni di guida per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [considerazioni sulla sicurezza per un'installazione di SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md).

-   Eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor sul computer del server di report per individuare eventuali problemi che potrebbero impedire l'aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).

-   Eseguire il backup della chiave simmetrica. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).

-   Eseguire il backup dei database e dei file di configurazione del server di report. Per altre informazioni, vedere [Backup and Restore Operations for Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md).

-   Eseguire il backup di eventuali personalizzazioni nelle directory virtuali di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] esistenti in IIS.

-   Rimuovere certificati SSL non validi.  In questa operazione sono inclusi i certificati scaduti e quelli che non si intende aggiornare prima dell'aggiornamento di Reporting Services.  I certificati non validi causano l'esito negativo dell'aggiornamento e un messaggio di errore simile al seguente verrà scritto nel file di registro di Reporting Services: **Microsoft.ReportingServices.WmiProvider.WMIProviderException: Nel sito Web non è configurato un certificato SSL (Secure Sockets Layer)**.

 Prima di aggiornare un ambiente di produzione, eseguire sempre un aggiornamento di prova in un ambiente di pre-produzione che abbia la stessa configurazione dell'ambiente di produzione.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

## <a name="overview-of-migration-scenarios"></a>Panoramica degli scenari di migrazione
 Se si esegue l'aggiornamento da una versione supportata di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è in genere possibile eseguire l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per aggiornare i file di programma del server di report, il database e tutti i dati dell'applicazione.

 È tuttavia necessario eseguire manualmente la **migrazione** di un'installazione del server di report se si verifica una delle condizioni seguenti:

-   Tramite Upgrade Advisor sono stati rilevati uno o più blocchi di aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).

-   Si desidera modificare il tipo di server di report usato nella distribuzione. Non è possibile, ad esempio, eseguire l'aggiornamento o la conversione da un server di report in modalità nativa a un server di report in modalità SharePoint. Per altre informazioni, vedere [Migrazione dalla modalità nativa alla modalità SharePoint &#40;SSRS&#41;](../../reporting-services/install-windows/native-to-sharepoint-migration-ssrs.md).

-   Si desidera ridurre la quantità di tempo in cui il server di report viene portato offline durante il processo di aggiornamento. L'installazione corrente rimane online durante la copia dei dati di contenuto in una nuova istanza del server di report e il test dell'installazione senza la modifica dello stato di installazione del server di report esistente.

-   Si desidera eseguire la migrazione di una distribuzione di SharePoint 2010 di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a SharePoint 2013. SharePoint 2013 non supporta l'aggiornamento sul posto da SharePoint 2010. Per altre informazioni, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_native_scenarios"></a>Scenari di aggiornamento e migrazione della modalità nativa
 **Aggiornamento:** L'aggiornamento sul posto per la modalità nativa è lo stesso processo per ognuna delle versioni supportate elencate in precedenza in questo argomento. Eseguire l'Installazione guidata di SQL Server o l'installazione da riga di comando. Al termine dell'installazione il database del server di report verrà aggiornato automaticamente al nuovo schema del database del server di report. Per ulteriori informazioni, vedere la sezione relativa all' [aggiornamento sul posto](#bkmk_inplace_upgrade) in questo argomento.

 Il processo di aggiornamento viene avviato quando si seleziona un'istanza del server di report esistente da aggiornare.

1.  Se il database del server di report è installato in un computer remoto e non si dispone dell'autorizzazione necessaria per aggiornarlo, verrà richiesto di specificare le credenziali per l'aggiornamento a un database del server di report remoto. Assicurarsi di fornire credenziali che dispongono di autorizzazioni `sysadmin` o per l'aggiornamento del database.

2.  Il programma di installazione verifica la presenza di eventuali condizioni o impostazioni che impediscono l'aggiornamento e legge le impostazioni di configurazione. Alcuni esempi sono le estensioni personalizzate distribuite nel server di report. Se l'aggiornamento viene bloccato, è necessario modificare l'installazione per evitare il blocco oppure eseguire la migrazione a una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Per altre informazioni, vedere la documentazione di Preparazione aggiornamento.

3.  Se è possibile procedere, viene richiesto di continuare con il processo di aggiornamento.

4.  Tramite il programma di installazione vengono create nuove cartelle per i file di programma di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Le cartelle di programma per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] un'installazione includono MSRS12. \< *nome istanza*>.

5.  Vengono inoltre aggiunti i file di programma del server di report, gli strumenti di configurazione e le utilità della riga di comando di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che fanno parte della funzionalità del server di report.

    1.  I file di programma della versione precedente vengono rimossi.

    2.  Tra gli strumenti e le utilità di configurazione del server di report aggiornati alla nuova versione sono inclusi lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa, le utilità della riga di comando, ad esempio RS.exe, e Generatore report.

    3.  Altri strumenti client, ad esempio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , e la documentazione online non vengono aggiornati. Per ottenere le nuove versioni degli strumenti, è possibile aggiungerle quando si esegue il programma di installazione. Le versioni precedenti coesisteranno insieme alle versioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Eventuali esempi installati vengono mantenuti nella versione precedente, in quanto l'installazione non supporta l'aggiornamento degli esempi di SQL Server.

    4.  
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è un download separato. Per altre informazioni, vedere [Microsoft SQL Server 2014 Data Tools - Business Intelligence per Microsoft Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).

6.  Il programma di installazione riutilizza la voce di servizio in Gestione controllo servizi per il servizio del server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Tale voce di servizio include l'account del servizio Windows del server di report.

7.  Nuovi URL vengono riservati in base alle impostazioni delle directory virtuali esistenti in IIS. Poiché le directory virtuali di IIS potrebbero non essere rimosse dal programma di installazione, assicurarsi di rimuoverle manualmente al termine dell'aggiornamento.

8.  I database del server di report vengono aggiornati al nuovo schema e `RSExecRole` viene modificato aggiungendo le autorizzazioni del proprietario di database al ruolo. Questo passaggio si verifica solo quando si esegue l' [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiornamento da precedente a SP1.

9. Il programma di installazione unisce le impostazioni nei file di configurazione. Usando come base i file di configurazione dell'installazione corrente, vengono aggiunte nuove voci. Le voci obsolete non vengono rimosse, ma non verranno più lette dal server di report al termine dell'aggiornamento. L'aggiornamento non comporta l'eliminazione dei file di log precedenti, del file RSWebApplication.config obsoleto o delle impostazioni delle directory virtuali in IIS. L'aggiornamento non comporta inoltre la rimozione di Progettazione report SQL Server 2005, di Management Studio o degli altri strumenti client. Se non sono più necessari, accertarsi di rimuovere i file e gli strumenti al termine dell'aggiornamento.

 **Migrazione:** La migrazione di una versione precedente di un'installazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] modalità nativa a prevede gli stessi passaggi per tutte le versioni supportate elencate in precedenza in questo argomento. Per altre informazioni, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_native_scaleout"></a>Aggiornare una distribuzione con scalabilità orizzontale di Reporting Services in modalità nativa
 Di seguito viene illustrato come aggiornare una distribuzione in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con scalabilità orizzontale a più di un server di report. Questo processo implica tempi di inattività della distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :

1.  Eseguire il backup dei database e delle chiavi di crittografia del server di report. Per altre informazioni, vedere [Operazioni di backup e ripristino per Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md) e [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).

2.  Utilizzare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e rimuovere tutti i server di report dalla distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).

3.  Aggiornare uno dei server di report a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

4.  Utilizzare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per aggiungere di nuovo i server di report nella distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).

     Per ogni server, ripetere i passaggi di aggiornamento e scalabilità orizzontale.

##  <a name="bkmk_sharePoint_scenarios"></a>Scenari di aggiornamento e migrazione della modalità SharePoint
 Nelle sezioni seguenti vengono descritti i problemi e i passaggi di base necessari per eseguire l'aggiornamento o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la migrazione da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] versioni specificate della modalità SharePoint di alla modalità SharePoint di.

 Esistono due componenti di installazione per aggiornare una distribuzione della modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Servizio SharePoint Shared.

    > [!TIP]
    >  Utilizzare il cmdlet di SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di `Get-SPRSServiceApplicationServers` per determinare i server nella farm SharePoint che attualmente eseguono il servizio SharePoint Shared di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e, pertanto, richiedono un aggiornamento.

-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Componente aggiuntivo per prodotti SharePoint. Per ulteriori informazioni, vedere [installare o disinstallare il componente aggiuntivo Reporting Services per sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).

 Per informazioni dettagliate sulla migrazione di un'installazione in modalità SharePoint, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).

> [!IMPORTANT]
>  Alcuni degli scenari seguenti richiedono l'inattività dell'ambiente SharePoint a causa delle diverse tecnologie che devono essere aggiornate. Se non è possibile rendere inattivo l'ambiente, sarà necessario completare una migrazione anziché un aggiornamento sul posto.

### <a name="sssql11-to-sssql14"></a>[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]A[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente iniziale:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]., SharePoint 2010.

 **Ambiente finale:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010 o SharePoint 2013.

-   **SharePoint 2010:** L'aggiornamento sul posto di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è supportato, ma lo scenario di aggiornamento richiede tempo di inattività dell'ambiente SharePoint.

     Se si desidera eseguire SharePoint 2013 nell'ambiente finale, è necessario completare un aggiornamento del collegamento di database da SharePoint 2010 a SharePoint 2013.

-   **SharePoint 2013:** SharePoint 2013 non supporta l'aggiornamento sul posto da SharePoint 2010. Tuttavia, la procedura di **aggiornamento del collegamento di un database**  è supportata. Il comportamento è diverso dall'aggiornamento a SharePoint 2010, in cui un cliente può scegliere tra i due approcci di aggiornamento di base: l'aggiornamento sul posto e l'aggiornamento del collegamento di un database.

     Se si dispone di un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] integrata con SharePoint 2010, non è possibile eseguire l'aggiornamento sul posto del server SharePoint. È tuttavia possibile eseguire la migrazione dei database del contenuto e di quelli dell'applicazione di servizio dalla farm di SharePoint 2010 a una di SharePoint 2013.

### <a name="sskilimanjaro-to-sssql14"></a>[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]A[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente iniziale:** SQL Server 2008 R2, SharePoint 2010.

 **Ambiente finale:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   L'aggiornamento sul posto è supportato e non sono previsti tempi di inattività per l'ambiente SharePoint.

-   Installare la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint in ciascun front-end Web della farm. È possibile installare il componente aggiuntivo mediante l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oppure è possibile scaricarlo.

-   Eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] l'installazione di per aggiornare la modalità SharePoint per ogni "server di report". L'installazione guidata di SQL Server installerà [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] il servizio e creerà una nuova applicazione di servizio.

     Se si desidera eseguire SharePoint 2013 nell'ambiente finale, è necessario completare un aggiornamento del collegamento di database da SharePoint 2010 a SharePoint 2013.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

### <a name="sskatmai-sp2-to-sssql14"></a>Da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente iniziale:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2, SharePoint 2007.

 **Ambiente finale:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   Questo scenario dell'aggiornamento sul posto richiede l'inattività dell'ambiente SharePoint poiché entrambe le tecnologie di SharePoint e SQL Server devono essere aggiornate. È possibile scegliere di completare una migrazione anziché un aggiornamento sul posto.

-   Eseguire innanzitutto l'aggiornamento di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a Service Pack 2 (SP2), se non è già stato completato.

-   Eseguire l'aggiornamento a SharePoint 2010. Quando si esegue il programma di installazione dei prerequisiti di SharePoint 2010, verrà eseguito l'aggiornamento del componente aggiuntivo Reporting Services per i prodotti SharePoint 2010.

-   Installare la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint in tutti i front-end Web SharePoint. Con il programma di installazione dei prerequisiti di SharePoint viene installata la versione SQL Server 2008 R2 del componente aggiuntivo, ma è necessaria la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per usare il server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .

-   > [!WARNING]
    >  Al termine dell'aggiornamento di SharePoint, l'ambiente di Reporting Services si troverà in uno stato non funzionante finché non viene completato l'aggiornamento di SQL Server.

-   Eseguire l'aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando si esegue l'installazione guidata di SQL Server, viene visualizzata una finestra di dialogo relativa alla finestra di dialogo "**autenticazione in modalità SharePoint di SQL Server Reporting Services**". Verrà installato il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e le credenziali della pagina di autenticazione verranno usate per la creazione di un nuovo pool di applicazioni di SharePoint.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

### <a name="sql-server-2005-sp2-to-sssql14"></a>SQL Server 2005 SP2 a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]
 **Ambiente iniziale:** SQL Server 2005 SP2, SharePoint 2007.

 **Ambiente finale:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], SharePoint 2010.

-   Questo scenario dell'aggiornamento sul posto richiede l'inattività dell'ambiente SharePoint poiché entrambe le tecnologie di SharePoint e SQL Server devono essere aggiornate. È possibile scegliere di completare una migrazione anziché un aggiornamento sul posto.

-   Eseguire innanzitutto l'aggiornamento di SQL Server 2005 a Service Pack 2 (SP2), se non è già stato completato.

-   Eseguire l'aggiornamento a SharePoint 2010. Quando si esegue il programma di installazione dei prerequisiti di SharePoint 2010, verrà eseguito l'aggiornamento del componente aggiuntivo Reporting Services per i prodotti SharePoint 2010.

-   > [!WARNING]
    >  Al termine dell'aggiornamento di SharePoint, l'ambiente di Reporting Services si troverà in uno stato non funzionante finché non viene completato l'aggiornamento di SQL Server.

-   Installare la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint in tutti i front-end Web SharePoint. Con il programma di installazione dei prerequisiti di SharePoint viene installata la versione SQL Server 2008 R2 del componente aggiuntivo, ma è necessaria la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per usare il server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .

-   Eseguire l'aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando si esegue l'Installazione guidata di SQL Server, viene visualizzata la finestra di dialogo Autenticazione della modalità SharePoint di SQL Server Reporting Services. Verrà installato il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e le credenziali della pagina di autenticazione verranno usate per la creazione di un nuovo pool di applicazioni di SharePoint.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_migration_considerations"></a>Considerazioni per una migrazione
 Quando si spostano dati dell'applicazione, è necessario tenere presente i problemi e le restrizioni seguenti:

-   La sicurezza della chiave di crittografia include un valore hash in cui è incorporata l'identità del computer.

-   I nomi del database del server di report sono fissi e non possono essere modificati nel nuovo computer.

### <a name="encryption-key-considerations"></a>Considerazioni sulla chiave di crittografia
 Eseguire sempre il backup delle chiavi di crittografia prima di spostare un database del server di report in un nuovo computer.

 In seguito allo spostamento di un'installazione del server di report in un altro computer, il valore hash che protegge le chiavi di crittografia usate per proteggere dati sensibili archiviati nel database del server di report non sarà più valido. Ogni istanza del server di report che usa il database dispone della propria copia della chiave di crittografia, crittografata con l'identità dell'account del servizio come definito nel computer corrente. Se si cambia computer, il servizio non sarà più in grado di accedere alla propria chiave, anche se si usa lo stesso nome dell'account nel nuovo computer.

 Per ristabilire la crittografia reversibile nel nuovo computer del server di report, è necessario ripristinare la chiave di cui in precedenza è stato eseguito il backup. Il set di chiavi completo archiviato nel database del server di report è costituito da un valore della chiave simmetrica più le informazioni sull'identità del servizio usate per limitare l'accesso alla chiave in modo che possa essere usata solo dall'istanza del server di report in cui è archiviata. Durante il ripristino della chiave, nel server di report le copie esistenti della chiave vengono sostituite con nuove versioni che includono i valori relativi all'identità del computer e del servizio definiti nel computer corrente. Per altre informazioni, vedere gli argomenti seguenti:

-   Modalità SharePoint: vedere la sezione "Gestione chiavi" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)

-   Modalità nativa: vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

### <a name="fixed-database-name"></a>Nome fisso del database
 Non è possibile rinominare il database del server di report poiché l'identità del database viene registrata nelle stored procedure del server di report al momento della creazione del database stesso. La ridenominazione dei database primari o temporanei del server di report provocherà errori durante l'esecuzione delle procedure, rendendo non valida l'installazione del server di report.

 Se il nome del database dell'installazione esistente non è appropriato per la nuova installazione, è consigliabile creare un nuovo database con il nome desiderato, quindi caricare i dati dell'applicazione esistenti usando le tecniche seguenti:

-   Scrivere uno script [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] che chiama metodi SOAP del servizio Web ReportServer per copiare dati tra database. Lo script può essere eseguito mediante l'utilità RS.exe. Per altre informazioni su questo approccio, vedere [Script e PowerShell con Reporting Services](../tools/scripting-and-powershell-with-reporting-services.md).

-   Scrivere codice che chiama il provider WMI per copiare dati tra database. Per altre informazioni su questo approccio, vedere [Accedere al provider WMI per Reporting Services](../tools/access-the-reporting-services-wmi-provider.md).

-   Se il numero di elementi non è elevato, è possibile ripubblicare report, modelli di report e origini dati condivise da Progettazione report, Progettazione modelli e Generatore report nel nuovo server di report. È necessario ricreare assegnazioni di ruolo, sottoscrizioni, pianificazioni condivise, pianificazioni dello snapshot del report, proprietà personalizzate impostate nei report o in altri elementi, sicurezza degli elementi dei modelli e proprietà impostate nel server di report. La cronologia del report e i dati del log di esecuzione dei report saranno persi.

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

##  <a name="bkmk_additional_resources"></a>Risorse aggiuntive

> [!NOTE]
>  Per altre informazioni sull'aggiornamento del collegamento di un database di SharePoint, vedere gli argomenti seguenti:

-   [Panoramica del processo di aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688) (https://go.microsoft.com/fwlink/p/?LinkId=256688).

-   [Pulire le preparazioni prima di un aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689) (https://go.microsoft.com/fwlink/p/?LinkId=256689).

-   [Aggiornare i database da sharepoint 2010 a sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690) (https://go.microsoft.com/fwlink/p/?LinkId=256690).

 ![Icona freccia usata con il collegamento Torna all'inizio](../../2014-toc/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [in questo argomento:](#bkmk_top)

## <a name="see-also"></a>Vedere anche
 [Aggiornare i report](../../reporting-services/install-windows/upgrade-reports.md) [aggiornare a SQL Server 2014 usando l'installazione guidata &#40;installazione&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)


