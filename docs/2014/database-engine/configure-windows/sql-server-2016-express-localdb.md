---
title: SQL Server 2014 Express local DB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 224facf54b0cde09f97010be472e3cc28754e94b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62756999"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]è una modalità di esecuzione [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] di destinata agli sviluppatori del programma. [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` `LocalDB`l' [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]installazione di copia un set minimo di file necessari per avviare. Una `LocalDB` volta installato, gli sviluppatori avviano una connessione utilizzando una stringa di connessione speciale. Durante la connessione, l'infrastruttura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessaria viene creata automaticamente e avviata, consentendo all'applicazione di usare il database senza attività di configurazione complesse o lunghe. Con Developer Tools gli sviluppatori dispongono di un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che consente di scrivere e verificare il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] senza dover gestire un'istanza del server completa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` viene gestita tramite l' `SqlLocalDB.exe` utilità. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`deve essere utilizzato al posto della funzionalità [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] dell'istanza utente deprecata.  
  
## <a name="installing-localdb"></a>Installazione di LocalDB  
 Il metodo principale di installazione `LocalDB` di consiste nell'utilizzare il programma SqlLocalDB. msi. `LocalDB`è un'opzione per l'installazione di qualsiasi [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]SKU di. Selezionare `LocalDB` nella pagina **Selezione funzionalità** durante l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Può essere presente una sola installazione dei file `LocalDB` binari per ogni versione principale [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . È possibile avviare più processi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e in tutti verranno usati gli stessi file binari. Un'istanza del `LocalDB` è [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] stata avviata perché presenta le stesse limitazioni di[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descrizione  
 Il `LocalDB` programma di installazione utilizza il programma SqlLocalDB. msi per installare i file necessari nel computer. Una volta installato `LocalDB` , è un'istanza [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] di in grado di creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aprire database di. I file del database di sistema per il database sono archiviati nel percorso locale AppData degli utenti che generalmente è nascosto. Ad esempio **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. I file del database utente sono archiviati nel percorso indicato dall'utente, in genere nella cartella **C:\Users\\<user\>\Documents\\**.  
  
 Per ulteriori informazioni sull'inclusione `LocalDB` in un'applicazione, vedere [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] la documentazione [Cenni preliminari sui dati locali](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [procedura dettagliata: creazione di un database SQL Server database](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)locale e [procedura dettagliata: connessione ai dati in un database di SQL Server database locale (Windows Forms)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Per ulteriori informazioni sull'API `LocalDB` , vedere [SQL Server Express riferimento all'API dell'istanza del database locale](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) e [funzione LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 L'utilità SqlLocalDb consente di creare nuove istanze `LocalDB`di, avviare e arrestare un'istanza `LocalDB`di e include opzioni che consentono di gestire `LocalDB`.  Per altre informazioni sull'utilità SqlLocalDb, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 Le regole di confronto dell' `LocalDB` istanza per sono impostate su SQL_Latin1_General_CP1_CI_AS e non possono essere modificate. Le regole di confronto a livello di database, di colonna e di espressione sono supportate normalmente. Ai database indipendenti vengono applicate le regole di confronto dei metadati e di tempdb definite da [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrizioni  
 `LocalDB`Impossibile essere un sottoscrittore della replica di tipo merge.  
  
 `LocalDB`non supporta FILESTREAM.  
  
 `LocalDB`consente solo code locali per Service Broker.  
  
 Un'istanza di `LocalDB` di proprietà degli account predefiniti, ad esempio NT AUTHORITY\SYSTEM, può avere problemi di gestibilità a causa del reindirizzamento di Windows file System; Usare invece un account di Windows normale come proprietario.  
  
### <a name="automatic-and-named-instances"></a>Istanze denominate e automatiche  
 `LocalDB`supporta due tipi di istanze: istanze automatiche e istanze denominate.  
  
-   Le istanze automatiche di `LocalDB` sono pubbliche. Vengono create e gestite automaticamente per l'utente e possono essere usate da qualsiasi applicazione. Un'istanza automatica di `LocalDB` è disponibile per ogni versione `LocalDB` di installata nel computer dell'utente. Le istanze automatiche di `LocalDB` forniscono una gestione senza problemi. Non c'è necessità di creare l'istanza in quanto già funziona. In tal modo è possibile migrare e installare e l'applicazione con facilità in un computer diverso. Se nel computer di destinazione è installata la versione specificata di `LocalDB`, l'istanza automatica di `LocalDB` per quella versione è disponibile anche sul computer di destinazione. Le istanze automatiche di `LocalDB` hanno un modello speciale per il nome dell'istanza che appartiene a uno spazio dei nomi riservato. In questo modo si evitano conflitti di `LocalDB`nomi con istanze denominate di. Il nome per l'istanza automatica è **MSSQLLocalDB**.  
  
-   Le istanze denominate di `LocalDB` sono private. Sono di proprietà di una sola applicazione, responsabile della creazione e della gestione dell'istanza. Le istanze denominate forniscono l'isolamento dalle altre istanze e possono migliorare le prestazioni riducendo la contesa di risorse con altri utenti del database. Le istanze denominate devono essere create in modo esplicito `LocalDB` dall'utente tramite l'API di gestione o in modo implicito tramite il file app. config per un'applicazione gestita (sebbene l'applicazione gestita possa usare anche l'API, se necessario). A ogni istanza denominata `LocalDB` di è associata `LocalDB` una versione che punta al rispettivo set `LocalDB` di file binari. Il nome dell'istanza di `LocalDB` è `sysname` un tipo di dati che può contenere fino a 128 caratteri. Questo comportamento è diverso rispetto alle istanze denominate normali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], che limitano i nomi a nomi NetBIOS normali di 16 caratteri ASCII. Il nome di un'istanza di `LocalDB` può contenere qualsiasi carattere Unicode che sia valido all'interno di un nome file.  Un'istanza denominata che utilizza un nome dell'istanza automatica diventa un'istanza automatica.  
  
 I diversi utenti di un computer possono avere istanze con lo stesso nome. Ogni istanza è un processo diverso in esecuzione come utente diverso.  
  
## <a name="shared-instances-of-localdb"></a>Istanze condivise di LocalDB  
 Per supportare scenari in cui più utenti del computer devono connettersi a una singola istanza di, `LocalDB` `LocalDB` supporta la condivisione dell'istanza. Il proprietario di un'istanza può decidere di consentire agli altri utenti del computer di connettersi all'istanza. Le istanze automatiche e denominate di `LocalDB` possono essere condivise. Per condividere un'istanza di `LocalDB`, un utente ne seleziona un nome condiviso (alias). Poiché il nome condiviso è visibile a tutti gli utenti del computer, questo nome condiviso deve essere univoco nel computer. Il nome condiviso di un'istanza di `LocalDB` ha lo stesso formato dell'istanza denominata di `LocalDB`.  
  
 Solo un amministratore del computer può creare un'istanza condivisa di `LocalDB`. È `LocalDB` possibile annullare la condivisione di un'istanza condivisa di da un amministratore o dal proprietario dell'istanza condivisa di `LocalDB`. Per condividere e annullare la condivisione di un'istanza `LocalDB`di, utilizzare `LocalDBShareInstance` i `LocalDBUnShareInstance` metodi e dell' `LocalDB` API oppure le opzioni Condividi e non condivise dell'utilità SqlLocalDB.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Avvio e connessione a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Connessione all'istanza automatica  
 Il modo più semplice per `LocalDB` usare consiste nel connettersi all'istanza automatica di proprietà dell'utente corrente usando la stringa di connessione **"Server = (local DB) \MSSQLLocalDB; Integrated Security = true"**. Per connettersi a un database specifico usando il nome del file, usare una stringa di connessione simile a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  La prima volta che un utente in un computer tenta di connettersi `LocalDB`a, l'istanza automatica deve essere creata e avviata. Il tempo aggiuntivo necessario per la creazione dell'istanza può determinare un errore di tentativo di connessione generando un messaggio di timeout. In una situazione simile, attendere pochi secondi per consentire il completamento del processo di creazione, quindi riconnettersi.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Creazione e connessione alle istanze denominate  
 Oltre all'istanza automatica, `LocalDB` supporta anche le istanze denominate. Utilizzare il programma SqlLocalDB. exe per creare, avviare e arrestare un'istanza denominata di `LocalDB`. Per altre informazioni su SqlLocalDB.exe, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 Nell'ultima riga sopra indicata vengono restituite informazioni simili alle seguenti.  
  
|||  
|-|-|  
|Nome|"LocalDBApp1"|  
|Versione|\<> versione corrente|  
|Nome condiviso|""|  
|Proprietario|"\<utente di Windows>"|  
|Creazione automatica|No|  
|State|in esecuzione|  
|Ultima ora inizio|\<Data e ora>|  
|Nome pipe dell'istanza|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se l'applicazione usa una versione di .NET prima di 4.0.2 `LocalDB`, è necessario connettersi direttamente al named pipe di. Il valore del nome della pipe dell'istanza è il named pipe su `LocalDB` cui è in ascolto l'istanza di. La parte del nome della pipe dell'istanza dopo il database locale # verrà modificata ogni volta `LocalDB` che viene avviata l'istanza di. Per connettersi all'istanza `LocalDB` di utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], digitare il nome pipe dell'istanza nella casella **nome server** della finestra di dialogo **Connetti a [!INCLUDE[ssDE](../../includes/ssde-md.md)] ** . Dal programma personalizzato è possibile stabilire una connessione all'istanza di `LocalDB` utilizzando una stringa di connessione simile a`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Connessione a un'istanza condivisa di LocalDB  
 Per connettersi a un'istanza condivisa di `LocalDB` Add **.\\ ** (punto + barra rovesciata) alla stringa di connessione per fare riferimento allo spazio dei nomi riservato per le istanze condivise. Ad esempio, per connettersi a un'istanza condivisa di `LocalDB` denominata `AppData` , utilizzare una stringa di connessione `(localdb)\.\AppData` , ad esempio come parte della stringa di connessione. Un utente che si connette a un'istanza `LocalDB` condivisa di di cui non è proprietario deve disporre di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso con autenticazione di Windows o autenticazione di.  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
 Per informazioni sulla risoluzione dei `LocalDB`problemi, vedere [risoluzione dei problemi SQL Server 2012 Express](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx)local DB.  
  
## <a name="permissions"></a>Autorizzazioni  
 Un'istanza di [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` è un'istanza creata da un utente per l'utilizzo. Qualsiasi utente del computer può creare un database utilizzando un'istanza di `LocalDB`, archiviando i file nel proprio profilo utente ed eseguendo il processo con le proprie credenziali. Per impostazione predefinita, l'accesso all'istanza `LocalDB` di è limitato al relativo proprietario. I dati contenuti in `LocalDB` sono protetti da file System accesso ai file di database. Se i file di database dell'utente vengono archiviati in un percorso condiviso, il database può essere aperto da chiunque disponga di file system accesso a tale percorso utilizzando `LocalDB` un'istanza di di cui è proprietario. Se i file di database si trovano in un percorso protetto, ad esempio la cartella dati utente, solo quell'utente e gli amministratori con accesso a quella cartella, possono aprire il database. I `LocalDB` file possono essere aperti solo da un'istanza di `LocalDB` alla volta.  
  
> [!NOTE]  
>  `LocalDB`viene sempre eseguito nel contesto di sicurezza degli utenti. ovvero `LocalDB` non viene mai eseguito con le credenziali del gruppo dell'amministratore locale. Ciò significa che tutti i file di database utilizzati `LocalDB` da un'istanza devono essere accessibili utilizzando l'account di Windows dell'utente proprietario, senza considerare l'appartenenza al gruppo Administrators locale.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md)  
  
  
