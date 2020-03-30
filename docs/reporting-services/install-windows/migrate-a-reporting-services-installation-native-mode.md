---
title: Eseguire la migrazione di un'installazione di Reporting Services (modalità nativa) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 11/06/2018
ms.openlocfilehash: 5db33f22ffd5143d88c5654c753f1b08811c0c8a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68262897"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Eseguire la migrazione di un'installazione di Reporting Services (modalità nativa)

Questo argomento fornisce istruzioni dettagliate per la migrazione di una delle versioni supportate seguenti di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa a una nuova istanza di SQL Server Reporting Services:  
  
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

Per informazioni sulla migrazione di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  

::: moniker-end
  
 Per migrazione si intende lo spostamento di file di dati di un'applicazione a una nuova istanza di SQL Server. Di seguito sono elencati i motivi comuni per cui eseguire la migrazione dell'installazione:  
  
* Si dispone di una distribuzione su vasta scala o i requisiti di attività sono elevati.  
  
* Si intende modificare l'hardware o la topologia dell'installazione.  
  
* Si verifica un problema che blocca l'aggiornamento.

## <a name="native-mode-migration-overview"></a><a name="bkmk_nativemode_migration_overview"></a> Panoramica sulla migrazione della modalità nativa

 Il processo di migrazione per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include passaggi manuali e automatici. Le attività seguenti fanno parte della migrazione del server di report:  
  
* Eseguire il backup dei file di database, di applicazione e di configurazione.  
  
* Eseguire il backup della chiave di crittografia.  
  
* Installazione di una nuova istanza di SQL Server. Se si usa lo stesso hardware, è possibile installare SQL Server side-by-side con l'installazione esistente se è una delle versioni supportate.  
  
    > [!TIP]  
    >  Un'installazione side-by-side potrebbe richiedere l'installazione di SQL Server come istanza denominata.
  
* Spostare il database del server di report e gli altri file dell'applicazione dall'installazione esistente alla nuova installazione di SQL Server.  
  
* Spostare tutti i file dell'applicazione personalizzata nella nuova installazione.  
  
* Configurare il server di report.  
  
* Modificare **RSReportServer.config** per includere tutte le impostazioni personalizzate dall'installazione precedente.  
  
* Facoltativamente, configurare elenchi di controllo di accesso (ACL) personalizzati per il nuovo gruppo di servizi Windows per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
* Rimuovere le applicazioni e gli strumenti inutilizzati dopo avere verificato che la nuova istanza è completamente operativa.  
  
 Sono presenti restrizioni sulle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospitano il database del server di report. Rivedere l'argomento seguente se si riutilizza un database del server di report creato in un'installazione precedente.  
  
* [Creare un database del server di report](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
## <a name="fixed-database-name"></a><a name="bkmk_fixed_database_name"></a> Nome fisso del database

 Non è possibile rinominare il database del server di report poiché l'identità del database viene registrata nelle stored procedure del server di report al momento della creazione del database stesso. La ridenominazione dei database primari o temporanei del server di report causa errori durante l'esecuzione delle stored procedure, invalidando l'installazione del server di report.  
  
 Se il nome del database dell'installazione esistente non è appropriato per la nuova installazione, è consigliabile creare un nuovo database con il nome desiderato, quindi caricare i dati dell'applicazione esistenti utilizzando le tecniche seguenti:  
  
* Scrivere uno script [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] che chiama metodi SOAP del servizio Web ReportServer per copiare dati tra database. Lo script può essere eseguito mediante l'utilità RS.exe. Per altre informazioni su questo approccio, vedere [Script e PowerShell con Reporting Services](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
* Scrivere codice che chiama il provider WMI per copiare dati tra database. Per altre informazioni su questo approccio, vedere [Accedere al provider WMI per Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
* Se il numero di elementi non è elevato, è possibile ripubblicare report e origini dati condivise da Progettazione report, Progettazione modelli e Generatore report nel nuovo server di report. Ricreare assegnazioni di ruolo, sottoscrizioni, pianificazioni condivise, pianificazioni dello snapshot del report, proprietà personalizzate impostate nei report o in altri elementi, sicurezza degli elementi dei modelli e proprietà impostate nel server di report. È necessario sapere che la cronologia del report e i dati del log di esecuzione del report andranno persi se si eseguono queste azioni.
  
## <a name="before-you-start"></a><a name="bkmk_before_you_start"></a> Prima di iniziare

 Anche nei casi in cui si esegue la migrazione anziché l'aggiornamento dell'installazione, l'esecuzione di Preparazione aggiornamento nell'installazione esistente consente di identificare qualsiasi problema che potrebbe interessare la migrazione. Questo passaggio è particolarmente utile se si esegue la migrazione di un server di report che non è stato installato o configurato personalmente. L'esecuzione di Preparazione aggiornamento consente di individuare le impostazioni personalizzate che potrebbero non essere supportate in una nuova installazione di SQL Server.  
  
 È anche necessario considerare diverse importanti modifiche introdotte in SQL Server Reporting Services, che influiscono sulla migrazione dell'installazione:

* Il nuovo [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] ha sostituito Gestione report.
  
* A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], IIS non costituisce più un prerequisito. Se si esegue la migrazione di un'installazione del server di report a un nuovo computer, non è necessario aggiungere il ruolo del server Web. I passaggi per la configurazione degli URL e dell'autenticazione, inoltre, differiscono dalla versione precedente, come le tecniche e gli strumenti per la diagnosi e la risoluzione dei problemi.  
  
* Il servizio Web ReportServer, [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]e il servizio Windows ReportServer vengono eseguiti nello stesso account. Tutte e tre le applicazioni leggono le impostazioni di configurazione dal file RSReportServer.config.
  
* [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] e SQL Server Management Studio sono stati progettati per rimuovere le funzionalità sovrapposte. Ogni strumento supporta un set di attività distinto.
  
* I filtri ISAPI non sono supportati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive. Se si utilizzano filtri ISAPI, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione.  
  
* Le restrizioni relative agli indirizzi IP non sono supportate in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive. Se si utilizzano le restrizioni degli indirizzi IP, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione o utilizzare una tecnologia quale un firewall, un router o la conversione degli indirizzi di rete (NAT, Network Address Translation) per configurare indirizzi che non possono accedere al server di report.  
  
* I certificati SSL (Secure Sockets Layer) client non sono supportati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive. Se si utilizzano certificati SSL client, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione.  
  
* Se si usa un tipo di autenticazione diverso dall'autenticazione integrata di Windows, è necessario aggiornare l'elemento `<AuthenticationTypes>` nel file **RSReportServer.config** con un tipo di autenticazione supportato. I tipi di autenticazione supportati sono NTLM, Kerberos, Negotiate e Basic. Le autenticazioni anonime, .NET Passport e Digest non sono supportate in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive.  
  
* Se si usano fogli di stile CSS personalizzati nell'ambiente di report, la migrazione non può essere eseguita e sarà necessario spostarli manualmente in seguito alla migrazione.
  
Per altre informazioni sulle modifiche apportate in SQL Server Reporting Services, vedere la documentazione relativa a Gestione spazio aggiornamenti e [Novità di Reporting Services](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).  

## <a name="backup-files-and-data"></a><a name="bkmk_backup"></a> Backup di file e dati

 Prima di installare una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], verificare di avere eseguito il backup di tutti i file nell'installazione corrente.  
  
1. Eseguire il backup della chiave di crittografia per il database del server di report. Questo passaggio rappresenta una fase critica per la corretta esecuzione della migrazione. In un passaggio successivo del processo di migrazione sarà necessario ripristinare la chiave di crittografia per il server di report per ottenere di nuovo l'accesso ai dati crittografati. Per eseguire il backup della chiave, utilizzare lo strumento Gestione configurazione di Reporting Services.  
  
2. Eseguire il backup del database del server di report utilizzando uno dei metodi supportati per il backup di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere le istruzioni su come eseguire il backup del database del server di report in [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3. Eseguire il backup dei file di configurazione del server di report. I file di cui eseguire il backup includono:  
  
    1. RSReportServer.config  
  
    2. Rswebapplication.config  
  
    3. Rssvrpolicy.config  
  
    4. Rsmgrpolicy.config  
  
    5. Reportingservicesservice.exe.config  
  
    6. Web.config per l'applicazione [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] del server di report.  
  
    7. Machine.config per [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] se è stato modificato per le operazioni del server di report.  

## <a name="install-sql-server-reporting-services"></a><a name="bkmk_install_ssrs"></a> Installare SQL Server Reporting Services

 Installare una nuova istanza del server di report in modalità "solo file" per poterla configurare per l'utilizzo di valori non predefiniti. Per l'installazione da riga di comando, usare l'argomento **FilesOnly**. Nell'Installazione guidata selezionare l'opzione **Installa senza configurare il server di report**.  
  
 Fare clic su uno dei collegamenti seguenti per visualizzare istruzioni sull'installazione di una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
* [Installare SQL Server dall'Installazione guidata &#40;Installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
* [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  

## <a name="move-the-report-server-database"></a><a name="bkmk_move_database"></a> Spostamento del database del server di report

 Il database del server di report contiene report pubblicati, modelli, origini dati condivise, pianificazioni, risorse, sottoscrizioni e cartelle, insieme a proprietà di sistema e di elementi e autorizzazioni per l'accesso al contenuto del server di report.  
  
 Se la migrazione include l'utilizzo di un'istanza diversa del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , è necessario spostare il database del server di report nella nuova istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se si usa la stessa istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] , passare alla sezione [Spostamento di estensioni o di assembly personalizzati](#bkmk_move_custom).  
  
 Per spostare il database del server di report, seguire questa procedura:
  
1. Scegliere l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] da utilizzare. SQL Server Reporting Services richiede l'uso di una delle versioni seguenti per ospitare il database del server di report:  
  
    ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  

    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end
  
2. Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3. Creare **RSExecRole** nei database di sistema se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non ha mai ospitato un database del server di report. Per altre informazioni, vedere [Creare RSExecRole](../../reporting-services/security/create-the-rsexecrole.md).  
  
4. Seguire le istruzioni disponibili in [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Tenere presente che il database del server di report e il database temporaneo sono interdipendenti e devono essere spostati insieme. Non copiare i database. Se li si copia non si trasferiscono tutte le impostazioni di sicurezza nella nuova installazione. Non spostare processi di SQL Server Agent per operazioni pianificate del server di report. Tali processi vengono ricreati automaticamente dal server di report.  

## <a name="move-custom-assemblies-or-extensions"></a><a name="bkmk_move_custom"></a> Spostamento di estensioni o di assembly personalizzati

 Se l'installazione include elementi dei report, estensioni o assembly personalizzati, è necessario ridistribuire i componenti personalizzati. Se non si usano componenti personalizzati, passare alla sezione [Configurazione del server di report](#bkmk_configure_reportserver).  
  
 Per ridistribuire i componenti personalizzati, seguire questa procedura:  
  
1. Determinare se gli assembly sono supportati o devono essere ricompilati.

    * Le estensioni di sicurezza personalizzate devono essere riscritte usando l'interfaccia [IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx).
  
    * Le estensioni per il rendering personalizzate per [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devono essere riscritte usando il modello di oggetti per il rendering.  
  
    * I renderer HTML 3.2 e HTML OWC non sono supportati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive.  
  
    * Gli altri assembly personalizzati non richiedono la ricompilazione.  
  
2. Spostare gli assembly nel nuovo server di report e nella cartella \bin. In SQL Server i file binari del server di report si trovano nel percorso seguente per l'istanza del server di report predefinita:  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3. Modificare i file di configurazione per aggiungere voci per il componente personalizzato. Le voci possono variare a seconda del tipo di assembly usato. Per istruzioni sulla posizione dei file e delle voci di configurazione da aggiungere, vedere gli argomenti seguenti:  
  
    1. [Distribuzione di un assembly personalizzato](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2. [Procedura: Distribuzione di un elemento del report personalizzato](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3. [Distribuzione di un'estensione per l'elaborazione dati](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4. [Distribuzione di un'estensione per il recapito](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5. [Distribuzione di un'estensione per il rendering](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6. [Implementazione di un'estensione di sicurezza](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="configure-the-report-server"></a><a name="bkmk_configure_reportserver"></a> Configurazione del server di report

 Configurare gli URL per il servizio Web ReportServer e per il portale Web, quindi configurare la connessione al database del server di report.  
  
 Se si esegue la migrazione di una distribuzione con scalabilità orizzontale, portare tutti i nodi del server di report in modalità offline e migrare ciascuno server singolarmente. Dopo aver migrato il primo server di report e averlo connesso al database del server di report, la versione di tale database viene aggiornata automaticamente alla versione del database di SQL Server.  
  
> [!IMPORTANT]
>  Se uno dei server di report nella distribuzione con scalabilità orizzontale è online e non è stata eseguita la migrazione, si potrebbe verificare l'eccezione *rsInvalidReportServerDatabase* perché il server usa uno schema obsoleto quando è connesso al database aggiornato.  

Se il server di report di cui è stata eseguita la migrazione è configurato come database condiviso per una distribuzione con scalabilità orizzontale, è necessario eliminare tutte le chiavi di crittografia precedenti dalla tabella **Keys** nel database **ReportServer** rima di configurare il servizio del server di report. Se le chiavi non vengono rimosse, il server di report di cui è stata eseguita la migrazione tenterà l'inizializzazione in modalità di distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) e [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  

Non è possibile eliminare le chiavi di scalabilità orizzontale tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È necessario eliminare le chiavi precedenti dalla tabella **Keys** nel database **ReportServer** tramite SQL Server Management Studio. Eliminare tutte le righe nella tabella Keys. In questo modo vengono cancellati i dati dalla tabella e la tabella viene preparata per il solo ripristino della chiave simmetrica, come illustrato nei passaggi seguenti.  

Prima di eliminare le chiavi, è consigliabile eseguire innanzitutto il backup della chiave di crittografia simmetrica. Per eseguire questa operazione, è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Aprire Gestione configurazione, fare clic sulla scheda Chiavi di crittografia, quindi sul pulsante **Backup**. È inoltre possibile generare script dei comandi WMI per il backup della chiave di crittografia. Per altre informazioni su WMI, vedere [Metodo BackupEncryptionKey &#40;MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1. Avviare lo strumento Gestione configurazione Reporting Services e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] appena installata. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2. Configurare gli URL per il server di report e per il portale Web. Per altre informazioni, vedere [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3. Configurare il database del server di report, selezionando il database esistente dell'installazione precedente. Al termine della configurazione, i servizi del server di report vengono riavviati e, dopo aver stabilito una connessione al database del server di report, il database viene aggiornato automaticamente a SQL Server Reporting Services. Per altre informazioni su come eseguire la procedura guidata Cambia database, usata per creare o selezionare un database del server di report, vedere [Creare un database del server di report in modalità nativa](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4. Ripristinare le chiavi di crittografia. Questo passaggio è necessario per l'abilitazione di crittografia reversibile in stringhe di connessione preesistenti e credenziali già presenti nel database del server di report. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5. Se il server di report è stato installato in un nuovo computer e si utilizza Windows Firewall, assicurarsi che la porta TCP sulla quale è in attesa il server di report sia aperta. Per impostazione predefinita, tale porta è la numero 80. Per altre informazioni, vedere [Configurare un firewall per l'accesso al server di report](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6. Se si desidera amministrare il server di report in modalità nativa in locale, è necessario configurare il sistema operativo per consentire l'amministrazione locale con il portale Web. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  

## <a name="copy-custom-configuration-settings-to-rsreportserverconfig-file"></a><a name="bkmk_copy_custom_config"></a> Copia delle impostazioni di configurazione personalizzate nel file RSReportServer.config

Se nell'installazione precedente è stato modificato il file RSReportServer.config o RSWebApplication.config, è consigliabile apportare le stesse modifiche nel nuovo file RSReportServer.config. Nell'elenco seguente viene fornito un riepilogo di alcuni dei motivi per cui potrebbe essere stato necessario modificare il file di configurazione precedente e sono inclusi collegamenti ad altre informazioni su come configurare le stesse impostazioni in SQL Server 2016.  
  
|Personalizzazione|Informazioni|  
|-------------------|-----------------|  
|Recapito tramite posta elettronica del server di report con impostazioni personalizzate|[Impostazioni posta * elettronica (modalità nativa di Reporting Services)](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Impostazioni relative alle informazioni sul dispositivo|[Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="windows-service-group-and-security-acls"></a><a name="bkmk_windowsservice_group"></a> Gruppo di servizi Windows ed elenchi di controllo di accesso di sicurezza

 In [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], è disponibile un gruppo di servizi, ovvero il gruppo di servizi Windows per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , usato per creare elenchi di controllo di accesso di sicurezza per tutte le chiavi del Registro di sistema, i file e le cartelle installate con SQL Server Reporting Services. Il nome di questo gruppo Windows viene visualizzato nel formato SQLServerReportServerUser$\<*nome_computer*>$\<*nome_istanza*>.  

## <a name="verify-your-deployment"></a><a name="bkmk_verify"></a> Verifica della distribuzione

1. Testare le directory virtuali del server di report e di [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] aprendo un browser e digitando l'indirizzo URL. Per altre informazioni, vedere [Verificare un'installazione di Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
2. Testare i report e verificare che contengano i dati previsti. Rivedere le informazioni di origine dei dati per verificare se le informazioni sulla connessione all'origine dei dati sono ancora specificate. Il server di report usa il modello a oggetti dei report per l'elaborazione e il rendering dei report, ma non sostituisce i costrutti di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con i nuovi elementi RDL (Report Definition Language). Per altre informazioni sulla modalità di esecuzione dei report esistenti in una nuova versione del server di report, vedere [Aggiornare i report](../../reporting-services/install-windows/upgrade-reports.md).  

## <a name="remove-unused-programs-and-files"></a><a name="bkmk_remove_unused"></a> Rimozione di programmi e file inutilizzati

Dopo avere eseguito la migrazione del server di report a una nuova istanza, potrebbe essere necessario seguire questa procedura per rimuovere programmi e file che non sono più necessari.  
  
1. Disinstallare la versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se non è più necessaria. Questo passaggio non comporta l'eliminazione degli elementi riportati di seguito, che tuttavia possono essere rimossi manualmente se ritenuti inutili:  
  
    * Database del server di report precedente  
  
    * Ruolo RsExec  
  
    * Account del servizio del server di report  
  
    * Pool di applicazioni per il servizio Web ReportServer  
  
    * Directory virtuali per Gestione report e il server di report  
  
    * File di log del server di report  
  
2. Rimuovere IIS se non è più necessario nel computer.

## <a name="next-steps"></a>Passaggi successivi

* [Eseguire la migrazione di un'installazione di Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
* [Database del server di report](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
* [Eseguire l'aggiornamento e la migrazione di Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
* [Compatibilità con le versioni precedenti di Reporting Services](../../reporting-services/reporting-services-backward-compatibility.md)   
* [Gestione configurazione Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
