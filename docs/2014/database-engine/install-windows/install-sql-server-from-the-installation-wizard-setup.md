---
title: Installare SQL Server 2014 dall'installazione guidata (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e0af29d348ff55b415d22d44bc8e8e48a35d290
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775751"
---
# <a name="install-sql-server-2014-from-the-installation-wizard-setup"></a>Installare SQL Server 2014 dall'Installazione guidata (programma di installazione)
  In questo argomento vengono fornite istruzioni dettagliate per installare una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Poiché nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile un unico albero delle funzionalità per l'installazione di tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non è necessario installarli singolarmente. Per ulteriori informazioni sui vari componenti che possono essere installati, vedere [installazione per SQL Server 2014](installation-for-sql-server.md).  Per ulteriori informazioni su come installare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componenti singolarmente, vedere [Install SQL Server 2014](install-sql-server.md).  
  
 In questi argomenti aggiuntivi vengono illustrati altri modi per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Installare SQL Server 2014 dal prompt dei comandi](install-sql-server-from-the-command-prompt.md).  
  
-   [Installare SQL Server 2014 tramite un file di configurazione](install-sql-server-using-a-configuration-file.md)  
  
-   [Installare SQL Server 2014 con SysPrep](install-sql-server-using-sysprep.md)  
  
-   [Creare un nuovo cluster di failover di SQL Server &#40;&#41;di installazione ](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md).  
  
-   [Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata &#40;&#41;di installazione ](upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Prima di installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], rivedere gli argomenti in [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.  
  
### <a name="to-install-sscurrent"></a>Per installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserire il supporto di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nella cartella radice fare doppio clic sul file Setup.exe. Per eseguire l'installazione da una condivisione di rete, individuare la cartella radice nella condivisione, quindi fare doppio clic sul file Setup.exe.  
  
2.  L'Installazione guidata esegue Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per creare una nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic su **Installazione** a sinistra dell'area di navigazione, quindi fare clic su **Nuova installazione autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aggiunta di funzionalità a un'installazione esistente**.  
  
3.  Nella pagina relativa al codice Product Key selezionare un'opzione per indicare se si intende installare una versione gratuita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una versione di produzione del prodotto con una chiave PID. Per ulteriori informazioni, vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
     Per continuare, fare clic su **Avanti**.  
  
4.  Nella pagina Condizioni di licenza leggere il contratto di licenza e, per accettare, selezionare la casella di controllo **Accetto le condizioni di licenza** , quindi fare clic su **Avanti**. Per migliorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Nella finestra Regole globali, con la procedura di installazione si passerà automaticamente alla finestra Aggiornamenti prodotti se non vi sono errori di regole.  
  
6.  La pagina di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update verrà visualizzata successivamente se la casella di controllo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update non è selezionata in Pannello di controllo\Tutti gli elementi del Pannello di controllo\Windows Update\Modifica impostazioni. Se si seleziona la pagina [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, le impostazioni del computer vengono modificate per includere gli aggiornamenti quando si effettua l'analisi di Windows Update.  
  
7.  Nella pagina Aggiornamenti prodotto vengono visualizzati gli aggiornamenti più recenti sul prodotto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non viene individuato alcun aggiornamento del prodotto, durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa pagina non viene visualizzata e viene aperta automaticamente la pagina **Installazione dei file di installazione** .  
  
8.  Nella pagina Installa i file di installazione viene mostrato lo stato di avanzamento del download, dell'estrazione e dell'installazione dei file di installazione. Se viene individuato un aggiornamento per il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ne viene specificata l'inclusione, verrà installato anche questo aggiornamento.  
  
9. Nella pagina Impostazione ruolo selezionare ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione funzionalità**, quindi fare clic su **Avanti** per passare alla pagina Selezione funzionalità.  
  
10. Nella pagina Selezione funzionalità selezionare i componenti per l'installazione. Una volta selezionato il nome della funzionalità desiderata, nel riquadro **Descrizione funzionalità** viene visualizzata una descrizione per ogni gruppo di componenti. È possibile selezionare qualsiasi combinazione di caselle di controllo. Per ulteriori informazioni, vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro **Prerequisiti per le funzionalità selezionate** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno installati i prerequisiti che non sono stati ancora installati durante la procedura di installazione descritta più avanti in questo argomento.  
  
     È inoltre possibile specificare una directory personalizzata per i componenti condivisi utilizzando il campo posto nella pagina Selezione funzionalità. Per modificare il percorso di installazione per i componenti condivisi, aggiornare il percorso nel campo visualizzato nella parte inferiore della finestra di dialogo oppure fare clic su **Sfoglia** per passare a una directory di installazione. Il percorso di installazione predefinito è [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     Il percorso specificato per i componenti condivisi deve essere un percorso assoluto. La cartella non deve essere compressa o crittografata. Le unità di cui è stato eseguito il mapping non sono supportate.  
  
     Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene installato in un sistema operativo a 64 bit, saranno visualizzate le opzioni seguenti:  
  
    1.  Directory funzionalità condivise  
  
    2.  Directory funzionalità condivise (x86)  
  
     Il percorso specificato per ogni opzione descritta in precedenza deve essere diverso.  
  
11. Se tutte le regole vengono soddisfatte si procede automaticamente dalla finestra Regole funzionalità.  
  
12. Nella pagina Configurazione dell'istanza specificare se si desidera installare un'istanza predefinita o un'istanza denominata. Per ulteriori informazioni, vedere [Instance Configuration](../../sql-server/install/instance-configuration.md).  
  
     **ID istanza** : per impostazione predefinita, il nome dell'istanza viene usato come ID istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per usare un ID istanza non predefinito, specificare un valore differente nella casella di testo **ID istanza** .  
  
    > [!NOTE]  
    >  Le normali istanze autonome di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], sia che si tratti di istanze predefinite o denominate, usano un valore predefinito per l' **ID istanza**.  
  
     Tutti i Service Pack e gli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno applicati a ogni componente di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Istanze installate** : nella griglia vengono visualizzate le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer in cui viene eseguito il programma di installazione. Se nel computer è già installata un'istanza predefinita, è necessario installare un'istanza denominata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
     Il flusso di lavoro relativo alla parte rimanente dell'installazione dipende dalle funzionalità specificate per l'installazione. Le pagine visualizzate dipendono dalle selezioni effettuate.  
  
13. Usare la pagina Configurazione server - Account di servizio per specificare gli account di accesso per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I servizi effettivamente configurati in questa pagina dipendono dalle funzionalità selezionate per l'installazione.  
  
     È possibile assegnare lo stesso account di accesso a tutti i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure configurare singolarmente l'account di ogni servizio. È inoltre possibile specificare se i servizi verranno avviati automaticamente, manualmente o se sono disabilitati. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di configurare gli account del servizio singolarmente per assegnare i privilegi minimi a ogni servizio, in modo che ai servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengano concesse le autorizzazioni minime necessarie per completare le attività. Per altre informazioni, vedere [Configurazione Server - Account di servizio](../../sql-server/install/server-configuration-service-accounts.md) e [Configurare account di servizio e autorizzazioni di Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Per specificare lo stesso account di accesso per tutti gli account del servizio in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere le credenziali nei campi visualizzati nella parte inferiore della pagina.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     Usare la pagina Configurazione server - Regole di confronto per specificare regole di confronto non predefinite per il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Configurazione del server - Regole di confronto](../../sql-server/install/server-configuration-collation.md).  
  
14. Utilizzare la pagina Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Configurazione server per specificare gli elementi seguenti:  
  
    -   Modalità di sicurezza: selezionare l'autenticazione di Windows o l'autenticazione mista per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona l'autenticazione Modalità mista, è necessario specificare una password complessa per l'account amministratore di sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito.  
  
         Quando viene stabilita la connessione tra un dispositivo e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il meccanismo di sicurezza è lo stesso sia in modalità mista che di autenticazione di Windows. Per ulteriori informazioni, vedere [motore di database configurazione-provisioning dell'account](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Amministratori: è necessario specificare almeno un amministratore di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiungere l'account usato per eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Aggiungi utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Utilizzare la pagina Configurazione [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Directory dati per specificare directory di installazione non predefinite. Per eseguire l'installazione in directory predefinite, fare clic su **Avanti**.  
  
    > [!IMPORTANT]  
    >  Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Inoltre, l'installazione di SQL Server con le directory dei dati nella cartella radice dell'unità o in un punto di montaggio non riuscirà. Per ulteriori informazioni, consultare [SQL Server supporto per i volumi montati.](https://support.microsoft.com/kb/819546/en-us)  
  
     Per altre informazioni, vedere [Configurazione del motore di database - Directory dati](../../sql-server/install/database-engine-configuration-data-directories.md).  
  
     Utilizzare la pagina Configurazione [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM per abilitare la funzione FILESTREAM per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Configurazione del Motore di database - Filestream](../../sql-server/install/database-engine-configuration-filestream.md).  
  
15. Usare la pagina Configurazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Provisioning account per specificare la modalità server e gli utenti o gli account che disporranno delle autorizzazioni di amministratore per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La modalità server determina quali sottosistemi di memoria e archiviazione vengono utilizzati nel server. Tipi di soluzione diversi eseguiti nelle modalità server diverse. Se si intende eseguire database di cubi multidimensionali nel server, scegliere l'opzione predefinita, vale a dire quella relativa alla modalità server multidimensionale e di data mining. Relativamente alle autorizzazioni di amministratore, è necessario specificare almeno un amministratore di sistema per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per aggiungere l'account usato per eseguire il programma di installazione di SQL Server, fare clic su **Aggiungi utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer che disporranno di privilegi di amministratore per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulle autorizzazioni della modalità server e amministratore, vedere [Configurazione di Analysis Services - Provisioning account](../../sql-server/install/analysis-services-configuration-account-provisioning.md).  
  
     Dopo aver modificato l'elenco, fare clic su **OK**. Verificare l'elenco di amministratori nella finestra di dialogo di configurazione. Quando l'elenco è completo, fare clic su **Avanti**.  
  
     Utilizzare la pagina Configurazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Directory dati per specificare directory di installazione non predefinite. Per eseguire l'installazione in directory predefinite, fare clic su **Avanti**.  
  
    > [!IMPORTANT]  
    >  Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Inoltre, l'installazione di SQL Server con le directory dei dati nella cartella radice dell'unità o in un punto di montaggio non riuscirà. Per ulteriori informazioni, consultare [SQL Server supporto per i volumi montati.](https://support.microsoft.com/kb/819546/en-us)  
  
     Per altre informazioni, vedere [Configurazione di Analysis Services - Directory dati](../../sql-server/install/analysis-services-configuration-data-directories.md).  
  
16. Utilizzare la pagina Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per specificare il tipo di installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da creare. Per altre informazioni sulle modalità di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e le opzioni disponibili, vedere [Opzioni di configurazione di Reporting Services &#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md).  
  
     Dopo avere scelto un'opzione, fare clic su **Avanti** per continuare.  
  
17. Utilizzare la pagina di configurazione del controller di Riesecuzione distribuita per specificare gli utenti a cui si desidera concedere autorizzazioni amministrative per il servizio controller di Riesecuzione distribuita. Gli utenti che dispongono di autorizzazioni amministrative disporranno di accesso illimitato al servizio controller di Riesecuzione distribuita.  
  
     Fare clic su **Aggiungi utente corrente** per aggiungere gli utenti a cui concedere le autorizzazioni di accesso per il servizio controller di Riesecuzione distribuita. Fare clic sul pulsante **Aggiungi** per aggiungere autorizzazioni di accesso per il servizio controller di Riesecuzione distribuita. Fare clic sul pulsante **Rimuovi** per rimuovere le autorizzazioni di accesso dal servizio controller di Riesecuzione distribuita.  
  
     Per continuare, fare clic su **Avanti**.  
  
18. Utilizzare la pagina di configurazione del client Riesecuzione distribuita per specificare gli utenti a cui si desidera concedere autorizzazioni amministrative per il servizio client Riesecuzione distribuita. Gli utenti che dispongono di autorizzazioni amministrative disporranno di accesso illimitato al servizio client Riesecuzione distribuita.  
  
     **Nome controller** è un parametro facoltativo e il valore predefinito è \<*blank*>. Immettere il nome del controller che il computer client comunicherà con per il servizio client Riesecuzione distribuita. Tenere presente quanto segue:  
  
    -   Se è già stato configurato un controller, immettere il nome del controller durante la configurazione di ciascuno client.  
  
    -   In caso contrario, è possibile lasciare vuoto il nome del controller. Tuttavia, è necessario immettere manualmente il nome del controller nel file **configurazione client** .  
  
     Specificare la **directory di lavoro** per il servizio client riesecuzione distribuita. La directory di lavoro predefinita \<corrisponde alla *lettera di unità*>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:\\\Program Files \DReplayClient\WorkingDir.  
  
     Specificare la **directory dei risultati** per il servizio client riesecuzione distribuita. La directory dei risultati predefinita \< *è lettera di unità*>:\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Program\\files \DReplayClient\ResultDir.  
  
     Per continuare, fare clic su **Avanti**.  
  
19. Nella pagina Inizio installazione è disponibile una visualizzazione albero delle opzioni specificate durante l'installazione. In questa pagina, tramite il programma di installazione vengono indicati l'eventuale abilitazione o disabilitazione della funzionalità di aggiornamento del prodotto e la versione dell'aggiornamento finale.  
  
     Per continuare, fare clic su **Installa**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno innanzitutto installati i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
20. Durante l'installazione, nella pagina Stato dell'installazione è possibile monitorare lo stato di avanzamento del processo.  
  
21. Al termine dell'installazione nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo del processo di installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
22. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Passaggi successivi  
 Configurare la nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per ridurre la superficie di attacco di un sistema, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati e abilitati in modo selettivo i servizi e le funzionalità principali. Per ulteriori informazioni, vedere [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Convalidare un'installazione di SQL Server](validate-a-sql-server-installation.md)   
 [Eliminare un'installazione di SQL Server 2014](repair-a-failed-sql-server-installation.md)   
 [Visualizzare e leggere i file di log del programma di installazione SQL Server](view-and-read-sql-server-setup-log-files.md)   
 [Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata &#40;&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installazione di SQL Server 2014 dal prompt dei comandi](install-sql-server-from-the-command-prompt.md)  
  
  
