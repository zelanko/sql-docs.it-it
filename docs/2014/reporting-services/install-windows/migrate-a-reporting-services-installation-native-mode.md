---
title: Eseguire la migrazione di un'installazione di Reporting Services (modalità nativa) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.custom: ''
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.date: 08/10/2017
ms.openlocfilehash: c359f709b2c0a1ba779111a007843dd249b5d7b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63261294"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Eseguire la migrazione di un'installazione di Reporting Services (modalità nativa)

  In questo argomento vengono fornite istruzioni dettagliate per la migrazione di una delle versioni supportate seguenti di una [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] distribuzione in modalità nativa a una nuova [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] istanza di:  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)](Richiede più passaggi, vedere [non è possibile usare SQL Server 2005 per ospitare i database del server di Report 2014](https://support.microsoft.com/kb/2796721).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa.|  
  
 Per informazioni sulla migrazione di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
 Per migrazione si intende lo spostamento di file di dati di un'applicazione a una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Di seguito sono elencati i motivi comuni per cui eseguire la migrazione dell'installazione:  
  
-   Si dispone di una distribuzione su vasta scala o i requisiti di attività sono elevati.  
  
-   Si intende modificare l'hardware o la topologia dell'installazione.  
  
-   Si verifica un problema che blocca l'aggiornamento.  
  
##  <a name="bkmk_nativemode_migration_overview"></a>Panoramica della migrazione in modalità nativa  
 Il processo di migrazione per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include passaggi manuali e automatici. Le attività seguenti fanno parte della migrazione del server di report:  
  
-   Eseguire il backup dei file di database, di applicazione e di configurazione.  
  
-   Eseguire il backup della chiave di crittografia.  
  
-   Installare una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se si utilizza lo stesso hardware, è possibile installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] side-by-side con l'installazione esistente se è una delle versioni supportate.  
  
    > [!TIP]  
    >  Un'installazione side-by-side potrebbe richiedere l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] come istanza denominata.  
  
-   Spostare il database del server di report e gli altri file dell'applicazione dall'installazione esistente alla nuova installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
-   Spostare tutti i file dell'applicazione personalizzata nella nuova installazione.  
  
-   Configurare il server di report.  
  
-   Modificare **RSReportServer.config** per includere tutte le impostazioni personalizzate dall'installazione precedente.  
  
-   Facoltativamente, configurare elenchi di controllo di accesso (ACL) personalizzati per il nuovo gruppo di servizi Windows per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Rimuovere le applicazioni e gli strumenti inutilizzati dopo avere verificato che la nuova istanza è completamente operativa.  
  
 Sono presenti restrizioni sulle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospitano il database del server di report. Rivedere l'argomento seguente se si riutilizza un database del server di report creato in un'installazione precedente.  
  
-   [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
  
##  <a name="bkmk_fixed_database_name"></a>Nome del database predefinito  
 Non è possibile rinominare il database del server di report poiché l'identità del database viene registrata nelle stored procedure del server di report al momento della creazione del database stesso. La ridenominazione dei database primari o temporanei del server di report causa errori durante l'esecuzione delle stored procedure, invalidando l'installazione del server di report.  
  
 Se il nome del database dell'installazione esistente non è appropriato per la nuova installazione, è consigliabile creare un nuovo database con il nome desiderato, quindi caricare i dati dell'applicazione esistenti utilizzando le tecniche seguenti:  
  
-   Scrivere uno script [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] che chiama metodi SOAP del servizio Web ReportServer per copiare dati tra database. Lo script può essere eseguito mediante l'utilità RS.exe. Per altre informazioni su questo approccio, vedere [Script e PowerShell con Reporting Services](../tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Scrivere codice che chiama il provider WMI per copiare dati tra database. Per altre informazioni su questo approccio, vedere [Accedere al provider WMI per Reporting Services](../tools/access-the-reporting-services-wmi-provider.md).  
  
-   Se il numero di elementi non è elevato, è possibile ripubblicare report, modelli di report e origini dati condivise da Progettazione report, Progettazione modelli e Generatore report nel nuovo server di report. È necessario ricreare assegnazioni di ruolo, sottoscrizioni, pianificazioni condivise, pianificazioni dello snapshot del report, proprietà personalizzate impostate nei report o in altri elementi, sicurezza degli elementi dei modelli e proprietà impostate nel server di report. La cronologia del report e i dati del log di esecuzione dei report saranno persi.  
  
##  <a name="bkmk_before_you_start"></a>Prima di iniziare  
 Anche nei casi in cui si esegue la migrazione anziché l'aggiornamento dell'installazione, l'esecuzione di Preparazione aggiornamento nell'installazione esistente consente di identificare qualsiasi problema che potrebbe interessare la migrazione. Questo passaggio è particolarmente utile se si esegue la migrazione di un server di report che non è stato installato o configurato personalmente. L'esecuzione di Preparazione aggiornamento consente di individuare le impostazioni personalizzate che potrebbero non essere supportate in una nuova installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 È inoltre necessario considerare diverse importanti modifiche introdotte in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , che influiranno sulla migrazione dell'installazione:  
  
-   A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], IIS non costituisce più un prerequisito. Se si esegue la migrazione di un'installazione del server di report a un nuovo computer, non è necessario aggiungere il ruolo del server Web. I passaggi per la configurazione degli URL e dell'autenticazione, inoltre, differiscono dalla versione precedente, come le tecniche e gli strumenti per la diagnosi e la risoluzione dei problemi.  
  
-   Il servizio Web ReportServer, Gestione report e il servizio Windows ReportServer sono consolidati all'interno di un singolo servizio del server di report. Tutte e tre le applicazioni vengono eseguite utilizzando lo stesso account. Tutte e tre le applicazioni leggono le impostazioni di configurazione dal file RSReportServer.config, rendendo obsoleto il file RSWebApplication.config.  
  
-   Gestione report e SQL Server Management Studio sono stati riprogettati per rimuovere le funzionalità sovrapposte. Ogni strumento supporta un set di attività distinto e gli strumenti non sono più intercambiabili.  
  
-   I filtri ISAPI non sono supportati [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in e versioni successive. Se si utilizzano filtri ISAPI, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione.  
  
-   Le restrizioni degli indirizzi IP non sono [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supportate in e versioni successive. Se si utilizzano le restrizioni degli indirizzi IP, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione o utilizzare una tecnologia quale un firewall, un router o la conversione degli indirizzi di rete (NAT, Network Address Translation) per configurare indirizzi che non possono accedere al server di report.  
  
-   I certificati client Secure Sockets Layer (SSL) non sono supportati [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in e versioni successive. Se si utilizzano certificati SSL client, è necessario riprogettare la soluzione per la creazione di report prima di procedere alla migrazione.  
  
-   Se si usa un tipo di autenticazione diverso dall'autenticazione integrata di Windows, è necessario aggiornare l'elemento `<AuthenticationTypes>` nel file **RSReportServer.config** con un tipo di autenticazione supportato. I tipi di autenticazione supportati sono NTLM, Kerberos, Negotiate e Basic. L'autenticazione anonima, .NET Passport e digest non sono supportate [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in e versioni successive.  
  
-   Se si utilizzano fogli di stile CSS personalizzati nell'ambiente di report, tali fogli non saranno migrati e sarà necessario spostarli manualmente in seguito alla migrazione.  
  
 Per ulteriori informazioni sulle modifiche apportate in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere la documentazione di preparazione aggiornamento e [novità &#40;Reporting Services&#41;](../what-s-new-reporting-services.md).  
  
##  <a name="bkmk_backup"></a>Backup di file e dati  
 Prima di installare una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], verificare di avere eseguito il backup di tutti i file nell'installazione corrente.  
  
1.  Eseguire il backup della chiave di crittografia per il database del server di report. Questo passaggio rappresenta una fase critica per la corretta esecuzione della migrazione. In un passaggio successivo del processo di migrazione sarà necessario ripristinare la chiave di crittografia per il server di report per ottenere di nuovo l'accesso ai dati crittografati. Per eseguire il backup della chiave, utilizzare lo strumento Gestione configurazione di Reporting Services.  
  
2.  Eseguire il backup del database del server di report utilizzando uno dei metodi supportati per il backup di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere le istruzioni su come eseguire il backup del database del server di report in [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3.  Eseguire il backup dei file di configurazione del server di report. I file di cui eseguire il backup includono:  
  
    1.  RSReportServer.config  
  
    2.  Rswebapplication.config  
  
    3.  Rssvrpolicy.config  
  
    4.  Rsmgrpolicy.config  
  
    5.  Reportingservicesservice.exe.config  
  
    6.  Web.config per entrambe le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] del server di report e di Gestione report.  
  
    7.  Machine.config per [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] se è stato modificato per le operazioni del server di report.  
  
##  <a name="bkmk_install_ssrs"></a>Installa SQL Server Reporting Services  
 Installare una nuova istanza del server di report in modalità "solo file" per poterla configurare per l'utilizzo di valori non predefiniti. Per l'installazione da riga di comando, utilizzare l'argomento `FilesOnly`. Nell'Installazione guidata selezionare l'opzione **Installa senza configurare il server di report**.  
  
 Fare clic su uno dei collegamenti seguenti per visualizzare istruzioni sull'installazione di una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   [Installare SQL Server 2014 dall'installazione guidata &#40;&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [Installare SQL Server 2014 dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
##  <a name="bkmk_move_database"></a>Spostare il database del server di report  
 Il database del server di report contiene report pubblicati, modelli, origini dati condivise, pianificazioni, risorse, sottoscrizioni e cartelle, insieme a proprietà di sistema e di elementi e autorizzazioni per l'accesso al contenuto del server di report.  
  
 Se la migrazione include l'utilizzo di un'istanza diversa del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , è necessario spostare il database del server di report nella nuova istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se si usa la stessa istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] , passare alla sezione [Spostamento di estensioni o di assembly personalizzati](#bkmk_move_custom).  
  
 Per spostare il database del server di report, effettuare le operazioni seguenti:  
  
1.  Scegliere l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] da utilizzare. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede l'utilizzo di una delle versioni seguenti per ospitare il database del server di report:  
  
    -   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    -   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
2.  Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  Creare `RSExecRole` nei database di sistema se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non ha mai ospitato un database del server di report. Per altre informazioni, vedere [Creare RSExecRole](../security/create-the-rsexecrole.md).  
  
4.  Seguire le istruzioni disponibili in [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Tenere presente che il database del server di report e il database temporaneo sono interdipendenti e devono essere spostati insieme. Non copiare i database. Se li si copia non si trasferiscono tutte le impostazioni di sicurezza nella nuova installazione. Non spostare processi di SQL Server Agent per operazioni pianificate del server di report. Tali processi verranno ricreati automaticamente dal server di report.  
  
##  <a name="bkmk_move_custom"></a>Spostare estensioni o assembly personalizzati  
 Se l'installazione include elementi dei report, estensioni o assembly personalizzati, è necessario ridistribuire i componenti personalizzati. Se non si usano componenti personalizzati, passare alla sezione [Configurazione del server di report](#bkmk_configure_reportserver).  
  
 Per ridistribuire i componenti personalizzati, effettuare le operazioni seguenti:  
  
1.  Determinare se gli assembly sono supportati o devono essere ricompilati.  
  
    -   È necessario ricompilare le estensioni di autenticazione personalizzate create per la versione [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
    -   Le estensioni per il [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] rendering personalizzate per devono essere riscritte usando il modello a oggetti di rendering (ROM).  
  
    -   I renderer HTML 3,2 e HTML OWC non sono supportati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e versioni successive.  
  
    -   Gli altri assembly personalizzati non richiedono la ricompilazione.  
  
2.  Spostare gli assembly nel nuovo server di report e nelle cartelle \bin di Gestione report. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]i file binari del server di report si trovano nel percorso seguente per l' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] istanza predefinita:  
  
     `\Program files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3.  Modificare i file di configurazione per aggiungere voci per il componente personalizzato. Le voci possono variare a seconda del tipo di assembly utilizzato. Per istruzioni sulla posizione dei file e delle voci di configurazione da aggiungere, vedere gli argomenti seguenti:  
  
    1.  [Distribuzione di un assembly personalizzato](../custom-assemblies/deploying-a-custom-assembly.md)  
  
    2.  [Procedura: Distribuzione di un elemento del report personalizzato](../custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3.  [Distribuzione di un'estensione per l'elaborazione dati](../extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4.  [Distribuzione di un'estensione per il recapito](../extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5.  [Distribuzione di un'estensione per il rendering](../extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6.  [Implementazione di un'estensione di sicurezza](../extensions/security-extension/implementing-a-security-extension.md)  
  
##  <a name="bkmk_configure_reportserver"></a>Configurare il server di report  
 Configurare gli URL per il servizio Web ReportServer e per Gestione report, quindi configurare la connessione al database del server di report.  
  
 Se si esegue la migrazione di una distribuzione con scalabilità orizzontale, portare tutti i nodi del server di report in modalità offline e migrare ciascuno server singolarmente. Dopo aver migrato il primo server di report e averlo connesso al database del server di report, la versione di tale database viene aggiornata automaticamente alla versione del database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
> [!IMPORTANT]  
>  Se uno dei server di report nella distribuzione con scalabilità orizzontale è online e non è stato migrato, si potrebbe verificare l'eccezione rsInvalidReportServerDatabase perché il server utilizza uno schema obsoleto quando è connesso al database aggiornato.  
  
> [!NOTE]  
>  Se il server di report di cui è stata eseguita la migrazione è stato configurato come database condiviso per una distribuzione con scalabilità orizzontale, è necessario eliminare tutte le chiavi di crittografia precedenti dalla tabella **Keys** nel database **ReportServer** rima di configurare il servizio del server di report. Se le chiavi non vengono rimosse, il server di report di cui è stata eseguita la migrazione tenterà l'inizializzazione in modalità di distribuzione con scalabilità orizzontale. Per altre informazioni, vedere [Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale &#40;Gestione configurazione SSRS&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md) e [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md).  
>   
>  Non è possibile eliminare le chiavi di scalabilità orizzontale tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È necessario eliminare le chiavi precedenti dalla tabella **Keys** nel database **ReportServer** tramite SQL Server Management Studio. Eliminare tutte le righe nella tabella Keys. In questo modo verranno cancellati i dati dalla tabella e la tabella verrà preparata per il solo ripristino della chiave simmetrica, come illustrato nei passaggi seguenti.  
>   
>  Prima di eliminare le chiavi, è consigliabile eseguire innanzitutto il backup della chiave di crittografia simmetrica. Per eseguire questa operazione, è possibile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Aprire Gestione configurazione, fare clic sulla scheda **Chiavi di crittografia** , quindi sul pulsante **Backup** . È inoltre possibile generare script dei comandi WMI per il backup della chiave di crittografia. Per altre informazioni su WMI, vedere [Metodo BackupEncryptionKey &#40;MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1.  Avviare lo strumento Gestione configurazione di Reporting Services e connettersi all'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] appena installata. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Configurare gli URL per il server di report e per Gestione report. Per altre informazioni, vedere [Configurare un URL &#40;Gestione configurazione SSRS&#41;](configure-a-url-ssrs-configuration-manager.md).  
  
3.  Configurare il database del server di report, selezionando il database esistente dell'installazione precedente. Dopo aver completato la configurazione, i servizi del server di report verranno riavviati e, una volta stabilita una connessione al database del server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], il database verrà aggiornato automaticamente a. Per altre informazioni su come eseguire la procedura guidata Cambia database, usata per creare o selezionare un database del server di report, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Ripristinare le chiavi di crittografia. Questo passaggio è necessario per l'abilitazione di crittografia reversibile in stringhe di connessione preesistenti e credenziali già presenti nel database del server di report. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5.  Se il server di report è stato installato in un nuovo computer e si utilizza Windows Firewall, assicurarsi che la porta TCP sulla quale è in attesa il server di report sia aperta. Per impostazione predefinita, tale porta è la numero 80. Per ulteriori informazioni, vedere [configurazione di un firewall per l'accesso al server di report](../report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Se si desidera amministrare il server di report in modalità nativa in locale, è necessario configurare il sistema operativo per consentire l'amministrazione locale con Gestione report. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="bkmk_copy_custom_config"></a>Copiare le impostazioni di configurazione personalizzate nel file RSReportServer. config  
 Se nell'installazione precedente è stato modificato il file RSReportServer.config o RSWebApplication.config, è consigliabile apportare le stesse modifiche nel nuovo file RSReportServer.config. Nell'elenco seguente viene fornito un riepilogo di alcuni dei motivi per cui potrebbe essere stato necessario modificare il file di configurazione precedente e sono inclusi collegamenti a ulteriori informazioni su come configurare le stesse impostazioni in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Personalizzazione|Informazioni|  
|-------------------|-----------------|  
|Recapito tramite posta elettronica del server di report con impostazioni personalizzate|[Configurare un server di report per il recapito tramite posta elettronica &#40;ssrs Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [le impostazioni di posta elettronica-Configuration Manager &#40;modalità nativa SSRS&#41;](e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Impostazioni relative alle informazioni sul dispositivo|[Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](../customize-rendering-extension-parameters-in-rsreportserver-config.md)|  
|Gestione report in un'istanza remota|[Configurare Gestione report &#40;modalità nativa&#41;](../report-server/configure-web-portal.md)|  
  
##  <a name="bkmk_windowsservice_group"></a>ACL di sicurezza e gruppo di servizi Windows  
 In [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]è disponibile un gruppo di servizi, ovvero [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] il gruppo di servizi Windows, che consente di creare ACL di sicurezza per tutte le chiavi del registro di sistema, i file e [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]le cartelle installate con. Il nome del gruppo di Windows viene visualizzato nel formato\<SQLServerReportServerUser $*computer_name*>$\<*instance_name*>. Questo gruppo prende il posto dei due gruppi di servizi Windows in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se si dispone di ACL personalizzati associati a uno dei [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gruppi di Windows, sarà necessario applicare tali ACL al nuovo gruppo per la nuova istanza del server di report in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##  <a name="bkmk_verify"></a>Verificare la distribuzione  
  
1.  Testare le directory virtuali del server di report e di Gestione report aprendo un browser e digitando l'indirizzo URL. Per ulteriori informazioni, vedere [Verify a Reporting Services Installation](verify-a-reporting-services-installation.md).  
  
2.  Testare i report e verificare che contengano i dati previsti. Rivedere le informazioni di origine dei dati per verificare se le informazioni sulla connessione all'origine dei dati sono ancora specificate. Il server di report utilizza il modello a oggetti dei report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'elaborazione e il rendering dei report, ma non sostituisce i costrutti di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] con i nuovi elementi RDL (Report Definition Language). Per altre informazioni sulla modalità di esecuzione dei report esistenti in un server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , vedere [Aggiornare i report](upgrade-reports.md).  
  
##  <a name="bkmk_remove_unused"></a>Rimuovere programmi e file inutilizzati  
 Dopo aver eseguito la migrazione del server di report a un' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] istanza di, è possibile eseguire la procedura seguente per rimuovere programmi e file che non sono più necessari.  
  
1.  Disinstallare la versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se non è più necessaria. Questo passaggio non comporta l'eliminazione degli elementi riportati di seguito, che tuttavia possono essere rimossi manualmente se ritenuti inutili:  
  
    -   Database del server di report precedente  
  
    -   Ruolo RsExec  
  
    -   Account del servizio del server di report  
  
    -   Pool di applicazioni per il servizio Web ReportServer  
  
    -   Directory virtuali per Gestione report e il server di report  
  
    -   File di log del server di report  
  
2.  Rimuovere IIS se non è più necessario nel computer.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md)   
 [Database del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Aggiornare ed eseguire la migrazione Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Compatibilità con le versioni precedenti di Reporting Services](../reporting-services-backward-compatibility.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
