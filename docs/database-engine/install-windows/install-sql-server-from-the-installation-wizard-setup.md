---
title: Installare SQL Server 2016 dall'Installazione guidata (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
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
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 1c907d719e139cd2d6d0cda3623cbaf668d09461
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794944"
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>Installare SQL Server dall'Installazione guidata (programma di installazione)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
In questo articolo viene descritto come installare SQL Server con l'Installazione guidata. Si applica a [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] e a [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)].

Questo articolo fornisce istruzioni dettagliate per installare una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile un unico albero delle funzionalità per l'installazione di tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non è necessario installarli singolarmente. Per altre informazioni su come installare i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] singolarmente, vedere [Installare SQL Server](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components).  

 Questi articoli aggiuntivi illustrano altri modi per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  

-   [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
-   [Installare SQL Server tramite un file di configurazione](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
  
-   [Installare SQL Server tramite SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
  
-   [Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   [Eseguire l'aggiornamento a SQL Server usando l'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) 

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], rivedere gli articoli in [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
> Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Requisito di installazione patch 

Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  
  
## <a name="to-install-includessnoversionincludesssnoversion-mdmd"></a>Per installare [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]  
  
1.  Inserire il supporto di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nella cartella radice fare doppio clic sul file Setup.exe. Per eseguire l'installazione da una condivisione di rete, individuare la cartella radice nella condivisione, quindi fare doppio clic sul file Setup.exe.  
  
2.  L'Installazione guidata esegue il Centro installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per creare una nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic su **Installazione** a sinistra dell'area di navigazione, quindi fare clic su **Nuova installazione autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aggiunta di funzionalità a un'installazione esistente**.  

3.  Nella pagina relativa al codice Product Key selezionare un'opzione per indicare se si intende installare una versione gratuita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una versione di produzione del prodotto con una chiave PID. Per altre informazioni, vedere [Edizioni e funzionalità supportate di SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
     Scegliere **Avanti**per continuare.

<!--
The following item is for SQL Server 2019 or greater
-->
  
::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
4.  Nella pagina Condizioni di licenza leggere il contratto di licenza e, per accettare, selezionare la casella di controllo **Accetto le condizioni di licenza e [l'informativa sulla privacy](https://privacy.microsoft.com/privacystatement)** e quindi fare clic su **Avanti**.  

::: moniker-end

<!--
The following item is for SQL Server 2016-2017
-->

::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
4.  Nella pagina Condizioni di licenza leggere il contratto di licenza e, per accettare, selezionare la casella di controllo **Accetto le condizioni di licenza** , quindi fare clic su **Avanti**.  

::: moniker-end

  >[!NOTE]
  > SQL Server trasmette le informazioni sull'esperienza di installazione, nonché altri dati sull'utilizzo e le prestazioni per aiutare Microsoft a migliorare il prodotto. Per altre informazioni sull'elaborazione dei dati e i controlli sulla privacy di SQL Server, vedere l'[informativa sulla privacy](https://privacy.microsoft.com/privacystatement) e [Configurare SQL Server per inviare commenti e suggerimenti a Microsoft](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016).

5.  Nella finestra Regole globali, con la procedura di installazione si passerà automaticamente alla finestra Aggiornamenti prodotti se non vi sono errori di regole.  
  
6.  La pagina di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update verrà visualizzata successivamente se la casella di controllo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update non è selezionata in Pannello di controllo\Tutti gli elementi del Pannello di controllo\Windows Update\Modifica impostazioni. Se si seleziona la pagina [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, le impostazioni del computer vengono modificate per includere gli aggiornamenti quando si effettua l'analisi di Windows Update.  

7.  Nella pagina Aggiornamenti prodotto vengono visualizzati gli aggiornamenti più recenti sul prodotto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se non viene individuato alcun aggiornamento del prodotto, durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa pagina non viene visualizzata e viene aperta automaticamente la pagina **Installazione dei file di installazione** .  

8.  Nella pagina Installa i file di installazione viene mostrato lo stato di avanzamento del download, dell'estrazione e dell'installazione dei file di installazione. Se viene individuato un aggiornamento per il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ne viene specificata l'inclusione, verrà installato anche questo aggiornamento. Se non viene trovato alcun aggiornamento, il programma di installazione proseguirà automaticamente. 
  
9. In **Regole di installazione** il programma di installazione di SQL Server esegue un controllo per rilevare i problemi potenziali che potrebbero verificarsi durante l'esecuzione dell'installazione. Se si verificano errori, fare clic sulla colonna **Stato** per altre informazioni. In caso contrario, fare clic su **Avanti**. 

10. Se questa è la prima installazione di SQL Server nel computer, la pagina **Tipo di installazione** non viene visualizzata e si passa direttamente alla pagina **Selezione funzionalità**. Tuttavia, se SQL Server è già installato nel sistema, nella pagina **Tipo di installazione** scegliere di eseguire una nuova installazione o aggiungere funzionalità a un'installazione esistente. Scegliere **Avanti**. 
  
11. Nella pagina **Selezione funzionalità** selezionare i componenti per l'installazione. Per installare una nuova istanza del motore di database di SQL Server, ad esempio, selezionare **Servizi motore di database**.

    Una volta selezionato il nome della funzionalità desiderata, nel riquadro **Descrizione funzionalità** viene visualizzata una descrizione per ogni gruppo di componenti. È possibile selezionare qualsiasi combinazione di caselle di controllo. Per altre informazioni, vedere Edizioni e componenti di [SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) e [SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).
  
     I prerequisiti per le funzionalità selezionate vengono visualizzati nel riquadro **Prerequisiti per le funzionalità selezionate** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno installati i prerequisiti che non sono stati ancora installati durante la procedura di installazione descritta più avanti in questo argomento.  
  
     È inoltre possibile specificare una directory personalizzata per i componenti condivisi utilizzando il campo posto nella pagina Selezione funzionalità. Per modificare il percorso di installazione per i componenti condivisi, aggiornare il percorso nel campo visualizzato nella parte inferiore della finestra di dialogo oppure fare clic su **Sfoglia** per passare a una directory di installazione. Il percorso di installazione predefinito è [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     Il percorso specificato per i componenti condivisi deve essere un percorso assoluto. La cartella non deve essere compressa o crittografata. Le unità di cui è stato eseguito il mapping non sono supportate.  
  
     SQL Server usa due directory per le funzionalità condivise:
  
     * Directory funzionalità condivise  
  
     * Directory funzionalità condivise (x86)  
  
     Il percorso specificato per ogni opzione descritta in precedenza deve essere diverso.  
  
12. Se tutte le regole vengono soddisfatte si procede automaticamente dalla finestra Regole funzionalità.  
  
13. Nella pagina Configurazione dell'istanza specificare se si desidera installare un'istanza predefinita o un'istanza denominata. Per ulteriori informazioni, vedere [Instance Configuration](../../sql-server/install/instance-configuration.md#instance-configuration).  
  
     **ID istanza** : per impostazione predefinita, come ID istanza viene usato il nome dell'istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per usare un ID istanza non predefinito, specificare un valore differente nella casella di testo **ID istanza** .  
  
    > [!NOTE]  
    >  Le normali istanze autonome di [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], sia che si tratti di istanze predefinite o denominate, usano un valore predefinito per l' **ID istanza**.  
  
     Tutti i Service Pack e gli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno applicati a ogni componente di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Istanze installate** : nella griglia vengono visualizzate le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer in cui viene eseguito il programma di installazione. Se nel computer è già installata un'istanza predefinita, è necessario installare un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)].  
  
     Il flusso di lavoro della parte rimanente dell'installazione dipende dalle funzionalità specificate per l'installazione. Le pagine visualizzate dipendono dalle selezioni effettuate.  
  
14. Usare la pagina Configurazione server - Account di servizio per specificare gli account di accesso per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I servizi effettivamente configurati in questa pagina dipendono dalle funzionalità selezionate per l'installazione.  Per altre informazioni sulle impostazioni di configurazione, vedere [Guida dell'installazione guidata](../../sql-server/install/instance-configuration.md#serverconfig)
  
     È possibile assegnare lo stesso account di accesso a tutti i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure configurare singolarmente l'account di ogni servizio. È inoltre possibile specificare se i servizi verranno avviati automaticamente, manualmente o se sono disabilitati. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di configurare gli account del servizio singolarmente per assegnare i privilegi minimi a ogni servizio, in modo che ai servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengano concesse le autorizzazioni minime necessarie per completare le attività. Per altre informazioni, vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Per specificare lo stesso account di accesso per tutti gli account del servizio in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], immettere le credenziali nei campi visualizzati nella parte inferiore della pagina.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
    
    > [!NOTE]
    > Iniziare con [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e selezionare la casella di controllo *Concedi il privilegio Esecuzione attività di manutenzione volume al servizio del motore di database di SQL Server* per consentire all'account di servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] l'uso di [Inizializzazione immediata dei file di database](../../relational-databases/databases/database-instant-file-initialization.md).
  
     Usare la pagina Configurazione server - Regole di confronto per specificare regole di confronto non predefinite per il [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni, vedere [Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
15. Usare la scheda **Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Configurazione del server** per specificare gli elementi seguenti:  
  
    -   Modalità di sicurezza: selezionare l'autenticazione di Windows o l'autenticazione mista per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona l'autenticazione Modalità mista, è necessario specificare una password complessa per l'account amministratore di sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito.  
  
       Quando viene stabilita la connessione tra un dispositivo e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il meccanismo di sicurezza è lo stesso sia in modalità mista che di autenticazione di Windows. Per altre informazioni, vedere [Configurazione del motore di database - Configurazione del server](../../sql-server/install/instance-configuration.md#serverconfig)
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Amministratori: è necessario specificare almeno un amministratore di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiungere l'account usato per eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Aggiungi utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Usare la scheda **Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - Directory dati** per specificare directory di installazione non predefinite. Per eseguire l'installazione in directory predefinite, fare clic su **Avanti**.  
  
    > [!IMPORTANT]  
    > Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Per altre informazioni, vedere [Configurazione del motore di database - Directory dati](../../sql-server/install/instance-configuration.md#datadir). 

     Usare la pagina  **Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - TempDB** per configurare le dimensioni dei file, il numero di file, le directory di installazione non predefinite e le impostazioni di aumento delle dimensioni dei file per TempDB. Per altre informazioni, vedere [Configurazione del motore di database - TempDB](../../sql-server/install/instance-configuration.md#tempdb).  

     ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
     Usare la scheda  **Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - MaxDOP** per specificare l'opzione max degree of parallelism. Questa impostazione determina quanti processori possono essere usati da una singola istruzione durante l'installazione e il valore consigliato viene calcolato automaticamente nel corso dell'installazione. Per altre informazioni, vedere le [linee guida dell'opzione max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).
     ::: moniker-end

     Usare la scheda**Configurazione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] - FILESTREAM** per abilitare la funzione FILESTREAM per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Configurazione del Motore di database - Filestream](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream).  
  
  
16. Usare la pagina Configurazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Provisioning account per specificare la modalità server e gli utenti o gli account che disporranno delle autorizzazioni di amministratore per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La modalità server determina quali sottosistemi di memoria e archiviazione vengono utilizzati nel server. Tipi di soluzione diversi eseguiti nelle modalità server diverse. Se si intende eseguire database di cubi multidimensionali nel server, scegliere l'opzione predefinita, vale a dire quella relativa alla modalità server multidimensionale e di data mining. Relativamente alle autorizzazioni di amministratore, è necessario specificare almeno un amministratore di sistema per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per aggiungere l'account usato per eseguire il programma di installazione di SQL Server, fare clic su **Aggiungi utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer che disporranno di privilegi di amministratore per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulle autorizzazioni della modalità server e amministratore, vedere [Configurazione di Analysis Services - Provisioning account](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning).  

    Dopo aver modificato l'elenco, fare clic su **OK**. Verificare l'elenco di amministratori nella finestra di dialogo di configurazione. Quando l'elenco è completo, fare clic su **Avanti**.

    Utilizzare la pagina Configurazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] - Directory dati per specificare directory di installazione non predefinite. Per eseguire l'installazione in directory predefinite, fare clic su **Avanti**.  
   
    > [!IMPORTANT]  
    > Quando si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se si specifica lo stesso percorso di directory per INSTANCEDIR e SQLUSERDBDIR, SQL Server Agent e la ricerca full-text non vengono avviati perché mancano le autorizzazioni.  
    >  
    > Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
   
    Per altre informazioni, vedere [Configurazione di Analysis Services - Directory dati](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories).  
   
17. Utilizzare la pagina di configurazione del controller di Riesecuzione distribuita per specificare gli utenti a cui si desidera concedere autorizzazioni amministrative per il servizio controller di Riesecuzione distribuita. Gli utenti che dispongono di autorizzazioni amministrative disporranno di accesso illimitato al servizio controller di Riesecuzione distribuita.  
  
     Fare clic su **Aggiungi utente corrente** per aggiungere gli utenti a cui concedere le autorizzazioni di accesso per il servizio controller di Riesecuzione distribuita. Fare clic sul pulsante **Aggiungi** per aggiungere autorizzazioni di accesso per il servizio controller di Riesecuzione distribuita. Fare clic sul pulsante **Rimuovi** per rimuovere le autorizzazioni di accesso dal servizio controller di Riesecuzione distribuita.  
  
     Scegliere **Avanti**per continuare.  
  
18. Utilizzare la pagina di configurazione del client Riesecuzione distribuita per specificare gli utenti a cui si desidera concedere autorizzazioni amministrative per il servizio client Riesecuzione distribuita. Gli utenti che dispongono di autorizzazioni amministrative disporranno di accesso illimitato al servizio client Riesecuzione distribuita.  
  
     **Nome controller** è un parametro facoltativo e il valore predefinito è \<*blank*>. Immettere il nome del controller che il computer client comunicherà con per il servizio client Riesecuzione distribuita. Si noti quanto segue:  
  
    -   Se è già stato configurato un controller, immettere il nome del controller durante la configurazione di ciascuno client.  
  
    -   In caso contrario, è possibile lasciare vuoto il nome del controller. Tuttavia, è necessario immettere manualmente il nome del controller nel file **configurazione client** .  
  
     Specificare la **Directory di lavoro** per il servizio client Riesecuzione distribuita. La directory di lavoro predefinita è \<*lettera unità*>:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Specificare la **Directory dei risultati** per il servizio client Riesecuzione distribuita. La directory dei risultati predefinita è \<*lettera unità*>:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Scegliere **Avanti**per continuare.  
  
19. Nella pagina Inizio installazione è disponibile una visualizzazione albero delle opzioni specificate durante l'installazione. In questa pagina, tramite il programma di installazione vengono indicati l'eventuale abilitazione o disabilitazione della funzionalità di aggiornamento del prodotto e la versione dell'aggiornamento finale.  
  
     Per continuare, fare clic su **Installa**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il programma di installazione consentirà innanzitutto di installare i prerequisiti obbligatori per le funzionalità selezionate e, successivamente, le funzionalità stesse.  
  
20. Durante l'installazione, nella pagina Stato dell'installazione è possibile monitorare lo stato di avanzamento del processo.  
  
21. Al termine dell'installazione nella pagina Operazione completata viene visualizzato un collegamento al file di log di riepilogo del processo di installazione e ad altre note importanti. Per completare il processo di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic su **Chiudi**.  
  
22. Se viene richiesto, riavviare il computer. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Passaggi successivi  
 Configurare la nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per ridurre la superficie di attacco di un sistema, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati e abilitati in modo selettivo i servizi e le funzionalità principali. Per ulteriori informazioni, vedere [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Convalidare un'installazione di SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Ripristinare un'installazione non riuscita di SQL Server 2016](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Eseguire l'aggiornamento a SQL Server 2016 usando l'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installazione di SQL Server 2016 dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
