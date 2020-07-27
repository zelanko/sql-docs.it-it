---
title: Gestione dei pacchetti (servizio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7121efa290a8cea45804467243e11dbfd98f275
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921997"
---
# <a name="package-management-ssis-service"></a>Gestione dei pacchetti (servizio SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La gestione dei pacchetti include monitoraggio, gestione, importazione ed esportazione di pacchetti.  
 
 ## <a name="package-store"></a>Archivio pacchetti  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include due cartelle di livello principale per l'accesso ai pacchetti: 
 - **Pacchetti in esecuzione** 
 - **Pacchetti archiviati**

 La cartella **Pacchetti in esecuzione** include i pacchetti in esecuzione nel server. La cartella **Pacchetti archiviati** include i pacchetti che vengono salvati nell'archivio pacchetti. Questi sono gli unici pacchetti gestiti dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'archivio pacchetti può includere sia il database msdb sia le cartelle del file system elencate nel file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Il file di configurazione specifica le cartelle msdb e del file system da gestire. Possono inoltre essere presenti pacchetti archiviati in un'altra posizione nel file system non gestiti dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 I pacchetti salvati in msdb sono archiviati in una tabella denominata sysssispackages. Quando si salvano i pacchetti in msdb, è possibile raggrupparli in cartelle logiche. L'uso di cartelle logiche può essere utile per organizzare i pacchetti in base allo scopo o per filtrarli nella tabella sysssispackages. Creare nuove cartelle logiche in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per impostazione predefinita, le cartelle logiche aggiunte a msdb vengono incluse automaticamente nell'archivio pacchetti.  
  
 Le cartelle logiche create sono rappresentate da righe nella tabella sysssispackagefolders di msdb. Le colonne folderid e parentfolderid di sysssispackagefolders definiscono la gerarchia delle cartelle. Le cartelle logiche radice di msdb corrispondono alle righe di sysssispackagefolders con valori Null nella colonna parentfolderid. Per altre informazioni, vedere [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md) e [sysssispackagefolders (Transact-SQL&)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 Quando si apre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e ci si connette a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vengono visualizzate le cartelle di msdb gestite dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] elencate nella cartella Pacchetti archiviati. Se il file di configurazione specifica cartelle del file system radice, nella cartella Pacchetti archiviati sono elencati anche i pacchetti salvati nel file system in tali cartelle e in tutte le sottocartelle.  
  
 È possibile archiviare pacchetti in qualunque cartella del file system, ma non verranno elencati nelle sottocartelle della cartella **Pacchetti archiviati** a meno che non si aggiunga la cartella all'elenco di cartelle nel file di configurazione per l'archivio pacchetti. Per altre informazioni sul file di configurazione, vedere [Servizio Integration Services &#40;servizio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 La cartella **Pacchetti in esecuzione** non contiene alcuna sottocartella e non è estensibile.  
  
 Per impostazione predefinita, la cartella **Pacchetti archiviati** contiene due sottocartelle, ovvero **File System** e **MSDB**. La cartella **File System** include i pacchetti che vengono salvati nel file system. La posizione di tali file è specificata nel file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La cartella predefinita è Packages, inclusa in %Programmi%\Microsoft SQL Server\100\DTS. La cartella **MSDB** include i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che sono stati salvati nel database msdb di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel server. La tabella sysssispackages contiene i pacchetti salvati in msdb.  
  
 Per visualizzare un elenco dei pacchetti presenti nell'archivio pacchetti, è necessario aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="monitor-running-packages"></a>Monitorare l'esecuzione dei pacchetti  
 La cartella **Pacchetti in esecuzione** include i pacchetti attualmente in esecuzione. Per visualizzare informazioni sui pacchetti indicati nella pagina **Riepilogo** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], fare clic sulla cartella **Pacchetti in esecuzione** . Nella pagina **Riepilogo** verranno visualizzate informazioni come la durata di esecuzione dei pacchetti. Per visualizzare informazioni aggiornate, aggiornare la cartella.  
  
 Per visualizzare informazioni su un singolo pacchetto indicato nella pagina **Riepilogo** , fare clic sul pacchetto. Nella pagina **Riepilogo** vengono visualizzate informazioni come la versione e la descrizione del pacchetto.  
  
Per arrestare un pacchetto in esecuzione dalla cartella **Pacchetti in esecuzione**, fare clic con il pulsante destro del mouse sul pacchetto e quindi scegliere **Arresta**.  
  
## <a name="view-packages-in-ssms"></a>Visualizzare pacchetti in SSMS
    
 In questo argomento viene descritta la procedura per la connessione a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e la visualizzazione di un elenco dei pacchetti gestiti dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="to-connect-to-integration-services"></a>Per connettersi a Integration Services  
  
1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, quindi **SQL Server Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** selezionare **Integration Services** dall'elenco **Tipo server** , specificare il nome del server nella finestra di dialogo **Nome server** e quindi fare clic su **Connetti**.  
  
    > [!IMPORTANT]  
    >  Se non è possibile stabilire la connessione con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è probabile che il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non sia in esecuzione. Per informazioni sullo stato del servizio, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server**, **Strumenti di configurazione**, quindi fare clic su **Gestione configurazione SQL Server**. Nel riquadro di sinistra fare clic su **Servizi di SQL Server**. Nel riquadro di destra cercare il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se non è già in esecuzione, avviare il servizio.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] si apre. Per impostazione predefinita, la finestra Esplora oggetti viene aperta e posizionata nell'angolo inferiore sinistro del programma. Se Esplora oggetti non viene visualizzato, scegliere **Esplora oggetti** dal menu **Visualizza** .  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Per visualizzare i pacchetti gestiti da Integration Services  
  
1.  In Esplora oggetti espandere la cartella Pacchetti archiviati.  
  
2.  Espandere le sottocartelle di Pacchetti archiviati per visualizzare i pacchetti.  

## <a name="import-and-export-packages"></a>Importare ed esportare pacchetti
 
 I pacchetti possono essere salvati nella tabella sysssispackages del database msdb di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nel file system.  
  
 L'archivio pacchetti, ovvero l'archivio logico gestito e monitorato dal servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , può includere sia il database msdb che le cartelle del file system specificate nel file di configurazione per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 È possibile importare ed esportare pacchetti tra i tipi di archivio seguenti:  
  
-   Cartelle del file system in qualsiasi posizione del file system.  
  
-   Cartelle dell'archivio pacchetti SSIS. Le due cartelle predefinite sono File system e MSDB.  
  
-   Il database msdb di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consente di importare ed esportare pacchetti. Durante queste operazioni il formato e la posizione dei pacchetti vengono modificati. Tramite le caratteristiche di importazione ed esportazione è possibile aggiungere pacchetti al file system, all'archivio pacchetti o al database msdb e copiarli quindi con un formato di archiviazione diverso. I pacchetti salvati in msdb, ad esempio, possono essere copiati nel file system e viceversa.  
  
 È inoltre possibile copiare un pacchetto in un formato diverso tramite l'utilità del prompt dei comandi **dtutil** (dtutil.exe). Per altre informazioni, vedere [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
 È possibile importare o esportare un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da o nei percorsi seguenti:  
  
-   È possibile importare un pacchetto archiviato in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nel file system o nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Il pacchetto importato viene salvato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o in una cartella nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Un pacchetto archiviato nel file system, in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] può essere esportato in un percorso e un formato di archiviazione diverso.  
  
 Per l'importazione e l'esportazione di un pacchetto tra versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ci sono tuttavia alcune restrizioni:  
  
-   In un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]è possibile importare pacchetti da un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ma non è possibile esportare pacchetti in un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
-   In un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]non è possibile importare pacchetti da o esportare pacchetti in un'istanza di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Le procedure descritte di seguito descrivono come utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per importare o esportare un pacchetto.  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Per importare un pacchetto utilizzando SQL Server Management Studio  
  
1.  Fare clic sul pulsante **Start**, scegliere **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi fare clic su **SQL Server Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** impostare le opzioni seguenti:  
  
    -   Nella casella **Tipo server** selezionare **Integration Services**.  
  
    -   Nella casella **Nome server** specificare il nome di un server oppure fare clic su **\<Browse for more...>** e individuare il server da usare.  
  
3.  Se il riquadro Esplora oggetti non è visualizzato, scegliere **Esplora oggetti** dal menu **Visualizza**.  
  
4.  In Esplora oggetti espandere la cartella **Pacchetti archiviati** .  
  
5.  Espandere le sottocartelle per individuare la cartella in cui si desidera importare un pacchetto.  
  
6.  Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Importa pacchetto**, quindi effettuare una delle operazioni seguenti:  
  
    -   Per importare il pacchetto da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare l'opzione **SQL Server** , specificare il server e selezionare la modalità di autenticazione. Se si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
         Fare clic sul pulsante Sfoglia **(...)** , selezionare il pacchetto da importare e quindi fare clic su **OK**.  
  
    -   Per importare il pacchetto dal file system, selezionare l'opzione **File system** .  
  
         Fare clic sul pulsante Sfoglia **(...)** , selezionare il pacchetto da importare e quindi fare clic su **Apri**.  
  
    -   Per importare il pacchetto dall'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] , selezionare l'opzione **Archivio pacchetti SSIS** e specificare il server.  
  
         Fare clic sul pulsante Sfoglia **(...)** , selezionare il pacchetto da importare e quindi fare clic su **OK**.  
  
7.  Facoltativamente, aggiornare il nome del pacchetto.  
  
8.  Per aggiornare il livello di protezione del pacchetto, fare clic sul pulsante Sfoglia **(...)** e specificare un livello di protezione diverso usando la finestra di dialogo **Livello di protezione pacchetto**. Se l'opzione **Crittografa tutti i dati sensibili con una password** o **Crittografa tutti i dati con una password** è selezionata, digitare e confermare una password.  
  
9. Fare clic su **OK** per completare l'importazione.  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Per esportare un pacchetto utilizzando SQL Server Management Studio  
  
1.  Fare clic sul pulsante **Start**, scegliere **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi fare clic su **SQL Server Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** impostare le opzioni seguenti:  
  
    -   Nella casella **Tipo server** selezionare **Integration Services**.  
  
    -   Nella casella **Nome server** specificare il nome di un server oppure fare clic su **\<Browse for more...>** e individuare il server da usare.  
  
3.  Se il riquadro Esplora oggetti non è visualizzato, scegliere **Esplora oggetti** dal menu **Visualizza**.  
  
4.  In Esplora oggetti espandere la cartella **Pacchetti archiviati** .  
  
5.  Espandere le sottocartelle per individuare il pacchetto da esportare.  
  
6.  Fare clic sul pacchetto con il pulsante destro del mouse, scegliere **Esporta**e quindi eseguire una delle operazioni seguenti:  
  
    -   Per esportare il pacchetto in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare l'opzione **SQL Server** , specificare il server e selezionare la modalità di autenticazione. Se si seleziona l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
         Fare clic sul pulsante Sfoglia **(...)** ed espandere la cartella **Pacchetti SSIS** per individuare la cartella in cui salvare il pacchetto. Facoltativamente, aggiornare il nome predefinito del pacchetto e quindi scegliere **OK**.  
  
    -   Per esportare il pacchetto nel file system, selezionare l'opzione **File system** .  
  
         Fare clic sul pulsante Sfoglia **(...)** per individuare la cartella in cui esportare il pacchetto, digitare il nome del file del pacchetto e quindi scegliere **Salva**.  
  
    -   Per eseguire l'esportazione nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] , selezionare l'opzione **Archivio pacchetti SSIS** e specificare il server.  
  
         Fare clic sul pulsante Sfoglia **(...)** , espandere la cartella **Pacchetti SSIS** e selezionare la cartella in cui si vuole salvare il pacchetto. Facoltativamente, immettere un nuovo nome per il pacchetto nella casella di testo **Nome pacchetto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Per aggiornare il livello di protezione del pacchetto, fare clic sul pulsante Sfoglia **(...)** e specificare un livello di protezione diverso usando la finestra di dialogo **Livello di protezione pacchetto**. Se l'opzione **Crittografa tutti i dati sensibili con una password** o **Crittografa tutti i dati con una password** è selezionata, digitare e confermare una password.  
  
8.  Scegliere **OK** per completare l'esportazione.  

## <a name="import-package-dialog-box-ui-reference"></a>Riferimento all'interfaccia utente della finestra di dialogo Importa pacchetto
  Usare la finestra di dialogo **Importa pacchetto** disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]per importare un pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e impostare o modificare il livello di protezione del pacchetto.  
  
### <a name="options"></a>Opzioni  
 **Posizione pacchetto**  
 Selezionare il tipo di percorso di archiviazione da cui importare il pacchetto. Sono disponibili le opzioni seguenti:  
  
 **SQL Server**  
  
 **File system**  
  
 **Archivio pacchetti SSIS**  
  
 **Server**  
 Consente di digitare il nome del server o di selezionarlo nell'elenco.  
  
 **autenticazione**  
 Consente di selezionare l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione è disponibile solo se è stato selezionato il percorso di archiviazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
 **Tipo di autenticazione**  
 Consente di selezionare un tipo di autenticazione.  
  
 **Nome utente**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare un nome utente.  
  
 **Password**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare una password.  
  
 **Percorso pacchetto**  
 Digitare il percorso del pacchetto oppure fare clic sul pulsante Sfoglia **(...)** per individuare il pacchetto.  
  
 **Nome pacchetto**  
 Se lo si desidera, rinominare il pacchetto. Il nome predefinito è il nome del pacchetto da importare.  
  
 **Livello di protezione**  
 Fare clic sul pulsante Sfoglia **(...)** e aggiornare il livello di protezione nella finestra di dialogo **Livello di protezione pacchetto**. Per altre informazioni, vedere [Finestra di dialogo Livello di protezione pacchetto e Livello di protezione del progetto](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="export-package-dialog-box-ui-reference"></a>Riferimento all'interfaccia utente della finestra di dialogo Esporta pacchetto
  Usare la finestra di dialogo **Esporta pacchetto** disponibile in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]per esportare un pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un percorso diverso ed eventualmente modificare il livello di protezione del pacchetto.  
  
### <a name="options"></a>Opzioni  
 **Posizione pacchetto**  
 Consente di selezionare il tipo di archiviazione in cui esportare il pacchetto. Sono disponibili le opzioni seguenti:  
  
 **SQL Server**  
  
 **File system**  
  
 **Archivio pacchetti SSIS**  
  
 **Server**  
 Consente di digitare il nome del server o di selezionarlo nell'elenco.  
  
 **autenticazione**  
 Consente di selezionare l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione è disponibile solo se è stato selezionato il percorso di archiviazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Se possibile, è consigliabile utilizzare l'autenticazione di Windows.  
  
 **Tipo di autenticazione**  
 Consente di selezionare un tipo di autenticazione.  
  
 **Nome utente**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare un nome utente.  
  
 **Password**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare una password.  
  
 **Percorso pacchetto**  
 Digitare il percorso del pacchetto oppure fare clic sul pulsante Sfoglia **(...)** e individuare la cartella in cui archiviare il pacchetto.  
  
 **Livello di protezione**  
 Fare clic sul pulsante Sfoglia **(...)** e aggiornare il livello di protezione nella finestra di dialogo **Livello di protezione pacchetto**. Per altre informazioni, vedere [Finestra di dialogo Livello di protezione pacchetto e Livello di protezione del progetto](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="back-up-and-restore-packages"></a>Eseguire il backup e il ripristino dei pacchetti
  
 I pacchetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possono essere salvati nel file system o in msdb, un database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile eseguire il backup e il ripristino dei pacchetti salvati in msdb usando le funzionalità di backup e ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni sul backup e sul ripristino del database msdb, fare clic su uno degli argomenti seguenti:  
  
-   [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Backup e ripristino di database di sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include l'utilità del prompt dei comandi **dtutil** (dtutil.exec), che può essere usata per gestire i pacchetti. Per altre informazioni, vedere [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="configuration-files"></a>File di configurazione  
 I file di configurazione dei pacchetti vengono archiviati nel file system. Questi file non vengono tuttavia inclusi nel backup del database msdb. Di conseguenza, è necessario assicurarsi che il backup di questi file venga eseguito regolarmente nell'ambito del piano per la sicurezza dei pacchetti salvati in msdb. Per includere configurazioni nel backup del database msdb, è consigliabile usare il tipo di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] invece delle configurazioni basate su file.  
  
### <a name="packages-stored-in-the-file-system"></a>Pacchetti archiviati nel file system  
 Nel piano per il backup del file system del server deve essere incluso il backup dei pacchetti salvati nel file system. Nel file di configurazione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , il cui nome predefinito è MsDtsSrvr.ini.xml, sono elencate le cartelle del server di cui il servizio esegue il monitoraggio. Assicurarsi di eseguire il backup di queste cartelle. I pacchetti potrebbero essere archiviati in altre cartelle del server. Assicurarsi di includere nel backup anche queste cartelle.  

## <a name="see-also"></a>Vedere anche  
 [Servizio Integration Services &#40;servizio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
