---
title: SQL Server 2016 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b3886ac725556683a3b20d8c3cd513b2fe5949f1
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617718"
---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft SQL Server 2016 Express **LocalDB** è una funzionalità di [SQL Server Express](../../sql-server/editions-and-components-of-sql-server-2016.md) destinata agli sviluppatori. È disponibile in SQL Server 2016 Express with Advanced Services.  

 Con l'installazione del**database locale** viene copiato un set di file minimo necessario per avviare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Una volta installato LocalDB, è possibile avviare una connessione tramite una stringa di connessione speciale. Durante la connessione, l'infrastruttura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessaria viene creata automaticamente e avviata, consentendo all'applicazione di usare il database senza attività di configurazione complesse. Con Developer Tools gli sviluppatori dispongono di un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che consente di scrivere e verificare il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] senza dover gestire un'istanza del server completa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 
 
 ## <a name="try-it-out"></a>Per provarlo: 
  
-   Per scaricare e installare SQL Server 2016 Express, passare ai **[download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads)**. LocalDB è una funzionalità selezionabile durante l'installazione ed è disponibile quando si scarica il supporto. Se si scarica il supporto, scegliere **Express Advanced** o il pacchetto **Local DB** tramite il **programma di installazione di Visual Studio**. Nel **programma di installazione di Visual Studio**, è possibile installare SQL Server Express Local DB nel contesto del carico di lavoro **Sviluppo per desktop .NET** o come componente singolo.

   > [!TIP]
   > È anche possibile installare Local DB insieme a Visual Studio 2017. Durante l'installazione di Visual Studio selezionare il carico di lavoro **Sviluppo per desktop .NET**, che include SQL Server Express Local DB.
  
-   Se si ha un account di Azure,  fare clic **[qui](https://azure.microsoft.com/services/virtual-machines/sql-server/)** per creare rapidamente una macchina virtuale in cui è già installato [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .  
  
## <a name="install-localdb"></a>Installare LocalDB  
 Installare **LocalDB** tramite l'installazione guidata o usando il programma SqlLocalDB.msi. **LocalDB** è un'opzione dell'installazione di [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. 
 
Selezionare **LocalDB** nella pagina **Selezione funzionalità** durante l'installazione. È possibile un'unica installazione dei file binari di **LocalDB** per ogni versione principale del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . È possibile avviare più processi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e in tutti verranno usati gli stessi file binari. Un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] avviata come **LocalDB** presenta le stesse limitazioni di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  

 Un'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** viene gestita con l'utilità **SqlLocalDB.exe** . [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** deve essere usato al posto della funzionalità dell'istanza utente [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] deprecata. 
  
## <a name="description"></a>Descrizione  
 Il programma di installazione di **LocalDB** usa il programma SqlLocalDB.msi per installare i file necessari nel computer. Una volta installato, **LocalDB** è un'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] con cui è possibile creare e aprire database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I file del database di sistema per il database sono archiviati nel percorso locale AppData degli utenti che generalmente è nascosto. Ad esempio **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. I file del database utente sono archiviati nel percorso indicato dall'utente, in genere nella cartella **C:\Users\\<user\>\Documents\\**.  
  
 Per altre informazioni su come includere **LocalDB** in un'applicazione, vedere la documentazione su [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] relativa a [ Cenni preliminari sui dati locali](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/ms233817(v=vs.110)), [Procedura dettagliata: Creazione di un database LocalDB di SQL Server](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/ms233763(v=vs.110)) e [Procedura dettagliata: Connessione ai dati di un database SQL Server Express LocalDB (Windows Form)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/ms171890(v=vs.110)).  
  
 Per altre informazioni sull'API **LocalDB**, vedere [Riferimento al database locale di SQL Server Express](../../relational-databases/sql-server-express-localdb-reference.md).  
  
 Con l'utilità SqlLocalDb è possibile creare nuove istanze di **LocalDB**, avviare e arrestare un'istanza di **LocalDB**, nonché includere opzioni per consentire la gestione di **LocalDB**.  Per altre informazioni sull'utilità SqlLocalDb, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 Le regole di confronto dell'istanza per **LocalDB** sono impostate su SQL_Latin1_General_CP1_CI_AS e non possono essere modificate. Le regole di confronto a livello di database, di colonna e di espressione sono supportate normalmente. Ai database indipendenti vengono applicate le regole di confronto dei metadati e di tempdb definite da [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 **LocalDB** non può essere un Sottoscrittore della replica di tipo merge.  
  
 **LocalDB** non supporta FILESTREAM.  
  
 **LocalDB** consente solo code locali per Service Broker.  
  
 Un'istanza di **LocalDB** di proprietà degli account predefiniti, ad esempio NT AUTHORITY\SYSTEM, può avere problemi di gestibilità a causa del reindirizzamento del file system di Windows. Usare invece un account di Windows normale come proprietario.  
  
### <a name="automatic-and-named-instances"></a>Istanze denominate e automatiche  
 **LocalDB** supporta due tipi di istanze, ovvero istanze automatiche e istanze denominate.  
  
-   Le istanze automatiche di **LocalDB** sono pubbliche. Vengono create e gestite automaticamente per l'utente e possono essere usate da qualsiasi applicazione. Un'istanza automatica di **LocalDB** esiste per ogni versione di **LocalDB** installato nel computer dell'utente. Le istanze automatiche di **LocalDB** forniscono una gestione continua dell'istanza. Non c'è necessità di creare l'istanza in quanto già funziona. In tal modo è possibile migrare e installare e l'applicazione con facilità in un computer diverso. Se nel computer di destinazione è installata la versione specificata di **LocalDB** , l'istanza automatica di **LocalDB** per quella versione è disponibile anche sul computer di destinazione. Le istanze automatiche di **LocalDB** dispongono di un modello speciale per il nome dell'istanza che appartiene a uno spazio dei nomi riservato. In tal modo si evitano conflitti di nomi con le istanze denominate di **LocalDB**. Il nome per l'istanza automatica è **MSSQLLocalDB**.  
  
-   Le istanze denominate di **LocalDB** sono private. Sono di proprietà di una sola applicazione, responsabile della creazione e della gestione dell'istanza. Le istanze denominate forniscono l'isolamento dalle altre istanze e possono migliorare le prestazioni riducendo la contesa di risorse con altri utenti del database. Le istanze denominate devono essere create in modo esplicito dall'utente tramite l'API di gestione di **LocalDB** o in modo implicito tramite il file app.config per un'applicazione gestita, sebbene anche l'applicazione gestita possa usare l'API. Ogni istanza denominata di **LocalDB** dispone di una versione associata di **LocalDB** che punta al relativo set di file binari di **LocalDB** . Il nome di un'istanza di **LocalDB** è composto dal tipo di dati **sysname** e da un massimo di 128 caratteri. I nomi delle istanze denominate normali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] invece possono essere solo nomi NetBIOS normali di 16 caratteri ASCII. Nel nome di un'istanza di **LocalDB** può essere incluso qualsiasi carattere Unicode che sia valido all'interno di un nome file.  Un'istanza denominata che utilizza un nome dell'istanza automatica diventa un'istanza automatica.  
  
 I diversi utenti di un computer possono avere istanze con lo stesso nome. Ogni istanza è un processo diverso in esecuzione come utente diverso.  
  
## <a name="shared-instances-of-localdb"></a>Istanze condivise di LocalDB  
 Per supportare scenari dove più utenti del computer devono connettersi a una sola istanza di **LocalDB**, **LocalDB** supporta la condivisione dell'istanza. Il proprietario di un'istanza può decidere di consentire agli altri utenti del computer di connettersi all'istanza. È possibile condividere le istanze automatiche e denominate di **LocalDB** . Per condividere un'istanza di **LocalDB** , un utente ne seleziona un nome condiviso (alias). Poiché il nome condiviso è visibile a tutti gli utenti del computer, questo nome condiviso deve essere univoco nel computer. Il nome condiviso di un'istanza di **LocalDB** ha lo stesso formato dell'istanza denominata di **LocalDB**.  
  
 Solo un amministratore del computer può creare un'istanza condivisa di **LocalDB**. La condivisione di un'istanza di **LocalDB** può essere annullata da un amministratore o dal proprietario dell'istanza condivisa di **LocalDB**. Per condividere e annullare la condivisione di un'istanza di **LocalDB**, usare i metodi `LocalDBShareInstance` e `LocalDBUnShareInstance` dell'API **LocalDB** o le opzioni di condivisione e annullamento della condivisione dell'utilità SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Avvio e connessione a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Connessione all'istanza automatica  
 Il modo più semplice per usare **LocalDB** consiste nel connettersi all'istanza automatica dell'utente corrente usando la stringa di connessione **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"**. Per connettersi a un database specifico usando il nome del file, usare una stringa di connessione simile a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  La prima volta che un utente prova a connettersi a **LocalDB**in un computer, l'istanza automatica deve essere creata e avviata. Il tempo aggiuntivo necessario per la creazione dell'istanza può determinare un errore di tentativo di connessione generando un messaggio di timeout. In una situazione simile, attendere pochi secondi per consentire il completamento del processo di creazione, quindi riconnettersi.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Creazione e connessione alle istanze denominate  
 Oltre all'istanza automatica, **LocalDB** supporta anche istanze denominate. Usare il programma SqlLocalDB.exe per creare, avviare e arrestare un'istanza denominata di **LocalDB**. Per altre informazioni su SqlLocalDB.exe, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 Nell'ultima riga sopra indicata vengono restituite informazioni simili alle seguenti.  
  
|||  
|-|-|  
|nome|"LocalDBApp1"|  
|Versione|\<Versione corrente>|  
|Nome condiviso|""|  
|Proprietario|"\<utente di Windows>"|  
|Creazione automatica|no|  
|State|esecuzione|  
|Ultima ora inizio|\<Data e ora>|  
|Nome pipe dell'istanza|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se nell'applicazione viene usato una versione di .NET precedente alla versione 4.0.2 è necessario connettersi direttamente alla named pipe di **LocalDB**. Il valore Nome pipe dell'istanza è la named pipe su cui l'istanza di **LocalDB** è in ascolto. La parte del nome pipe dell'istanza successiva a LOCALDB# verrà modificata a ogni avvio dell'istanza di **LocalDB**. Per connettersi all'istanza di **LocalDB** tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], immettere il nome pipe dell'istanza nella casella **Nome server** della finestra di dialogo **Connetti al [!INCLUDE[ssDE](../../includes/ssde-md.md)]**. Dal programma personalizzato è possibile stabilire una connessione all'istanza di **LocalDB** usando una stringa di connessione simile a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Connessione a un'istanza condivisa di LocalDB  
 Per connettersi a un'istanza condivisa di **LocalDB** aggiungere **.\\** (punto + barra rovesciata) alla stringa di connessione per fare riferimento allo spazio dei nomi riservato per le istanze condivise. Ad esempio, per connettersi a un'istanza condivisa di **LocalDB** denominata `AppData` usare `(localdb)\.\AppData` come stringa di connessione. Un utente che si connette a un'istanza condivisa di **LocalDB** di cui non è proprietario, deve disporre di un account di accesso con autenticazione di Windows o autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
 Per informazioni sulla risoluzione dei problemi di **LocalDB**, vedere la pagina relativa alla [risoluzione dei problemi di SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permissions  
 Un'istanza di [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** è un'istanza creata da un utente per l'uso personale. Qualsiasi utente del computer è in grado di creare un database mediante un'istanza di **LocalDB**, archiviando i file nel relativo percorso utente ed eseguendo il processo con le relative credenziali. Per impostazione predefinita, l'accesso all'istanza di **LocalDB** è limitato al relativo proprietario. I dati contenuti in **LocalDB** sono protetti dall'accesso ai file di database tramite il file system. Se i file di database dell'utente vengono archiviati in un percorso condiviso, il database può essere aperto da qualsiasi utente con accesso al file system in quel percorso usando un'istanza di **LocalDB** di cui è proprietario. Se i file di database si trovano in un percorso protetto, ad esempio la cartella dati utente, solo quell'utente e gli amministratori con accesso a quella cartella, possono aprire il database. I file di **LocalDB** possono essere aperti solo da un'istanza di **LocalDB** alla volta.  
  
> [!NOTE]  
>  **LocalDB** viene eseguito sempre nel contesto di sicurezza dell'utente. Questo significa che **LocalDB** non viene mai eseguito con credenziali del gruppo di amministratori locali. Di conseguenza, tutti i file di database usati da un'istanza di **LocalDB** devono essere accessibili usando l'account di Windows dell'utente proprietario, senza considerare l'appartenenza al gruppo di amministratori locali.  
  
## <a name="see-also"></a>Vedere anche  

[Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md)
