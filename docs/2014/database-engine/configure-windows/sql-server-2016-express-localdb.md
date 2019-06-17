---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62756999"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` è una modalità di esecuzione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinata agli sviluppatori. `LocalDB` installazione copiato un set minimo di file necessari per avviare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Una volta `LocalDB` è installato, gli sviluppatori avviano una connessione usando una stringa di connessione speciale. Durante la connessione, l'infrastruttura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessaria viene creata automaticamente e avviata, consentendo all'applicazione di usare il database senza attività di configurazione complesse o lunghe. Con Developer Tools gli sviluppatori dispongono di un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che consente di scrivere e verificare il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] senza dover gestire un'istanza del server completa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` viene gestito usando il `SqlLocalDB.exe` utilità. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` deve essere usato al posto di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] funzionalità dell'istanza utente è stato deprecato.  
  
## <a name="installing-localdb"></a>Installazione di LocalDB  
 Il metodo principale di installazione `LocalDB` consiste nell'usare il programma Sqllocaldb. `LocalDB` è un'opzione di installazione di qualsiasi SKU di [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. Selezionare `LocalDB` nella **Feature Selection** pagina durante l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Può essere presente solo un'installazione del `LocalDB` i file binari per ogni versione principale [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versione. È possibile avviare più processi del [!INCLUDE[ssDE](../../includes/ssde-md.md)] e in tutti verranno usati gli stessi file binari. Un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] avviata come il `LocalDB` ha le stesse limitazioni di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descrizione  
 Il `LocalDB` programma di installazione Usa il programma Sqllocaldb per installare i file necessari nel computer. Una volta installato, `LocalDB` è un'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] che può creare e aprire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database. I file del database di sistema per il database sono archiviati nel percorso locale AppData degli utenti che generalmente è nascosto. Ad esempio **C:\Users\\<user\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\** . I file del database utente sono archiviati nel percorso indicato dall'utente, in genere nella cartella **C:\Users\\<user\>\Documents\\** .  
  
 Per altre informazioni sull'inclusione `LocalDB` in un'applicazione, vedere la [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentazione [Cenni preliminari sui dati locali](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [procedura dettagliata: Creazione di un Database LocalDB SQL Server](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx), e [procedura dettagliata: Connessione ai dati in un Database LocalDB SQL Server (Windows Form)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Per altre informazioni sul `LocalDB` API, vedere [SQL Server Express LocalDB istanza API Reference](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) e [funzione LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 L'utilità SqlLocalDb è possibile creare nuove istanze del `LocalDB`, avviare e arrestare un'istanza di `LocalDB`e include opzioni che consentono di gestire `LocalDB`.  Per altre informazioni sull'utilità SqlLocalDb, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 Le regole di confronto di istanza per `LocalDB` è impostato su SQL_Latin1_General_CP1_CI_AS e non può essere modificato. Le regole di confronto a livello di database, di colonna e di espressione sono supportate normalmente. Ai database indipendenti vengono applicate le regole di confronto dei metadati e di tempdb definite da [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 `LocalDB` non può essere un sottoscrittore di replica di tipo merge.  
  
 `LocalDB` non supporta FILESTREAM.  
  
 `LocalDB` consente solo code locali per Service Broker.  
  
 Un'istanza di `LocalDB` di proprietà di account predefiniti, ad esempio NT AUTHORITY\SYSTEM, può avere i problemi di gestibilità a causa di un reindirizzamento del file system windows; Usare invece un account di windows normale come proprietario.  
  
### <a name="automatic-and-named-instances"></a>Istanze denominate e automatiche  
 `LocalDB` supporta due tipi di istanze: ovvero istanze automatiche e istanze denominate.  
  
-   Le istanze automatiche di `LocalDB` sono pubblici. Vengono create e gestite automaticamente per l'utente e possono essere usate da qualsiasi applicazione. Un'istanza automatica di `LocalDB` esiste per ogni versione di `LocalDB` installato nel computer dell'utente. Le istanze automatiche di `LocalDB` fornire una gestione continua dell'istanza. Non c'è necessità di creare l'istanza in quanto già funziona. In tal modo è possibile migrare e installare e l'applicazione con facilità in un computer diverso. Se nel computer di destinazione è installata la versione specificata di `LocalDB`, l'istanza automatica di `LocalDB` per quella versione è disponibile anche sul computer di destinazione. Le istanze automatiche di `LocalDB` dispongono di un modello speciale per il nome dell'istanza che appartiene a uno spazio dei nomi riservato. Ciò impedisce i conflitti di nome con le istanze denominate di `LocalDB`. Il nome per l'istanza automatica è **MSSQLLocalDB**.  
  
-   Le istanze denominate di `LocalDB` sono private. Sono di proprietà di una sola applicazione, responsabile della creazione e della gestione dell'istanza. Le istanze denominate forniscono l'isolamento dalle altre istanze e possono migliorare le prestazioni riducendo la contesa di risorse con altri utenti del database. Istanze denominate devono essere create in modo esplicito dall'utente tramite il `LocalDB` API di gestione o in modo implicito tramite l'app. config di file per un'applicazione gestita (sebbene anche l'applicazione gestita può usare l'API, se lo si desidera). Ogni istanza denominata di `LocalDB` è associato un `LocalDB` versione che punta al relativo set di `LocalDB` i file binari. Il nome dell'istanza di un `LocalDB` è `sysname` dati digitare e può avere fino a 128 caratteri. I nomi delle istanze denominate normali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] invece possono essere solo nomi NetBIOS normali di 16 caratteri ASCII. Il nome di un'istanza di `LocalDB` può contenere qualsiasi carattere Unicode che siano validi all'interno di un nome di file.  Un'istanza denominata che utilizza un nome dell'istanza automatica diventa un'istanza automatica.  
  
 I diversi utenti di un computer possono avere istanze con lo stesso nome. Ogni istanza è un processo diverso in esecuzione come utente diverso.  
  
## <a name="shared-instances-of-localdb"></a>Istanze condivise di LocalDB  
 Per supportare scenari dove più utenti del computer devono connettersi a una singola istanza di `LocalDB`, `LocalDB` supporta la condivisione dell'istanza. Il proprietario di un'istanza può decidere di consentire agli altri utenti del computer di connettersi all'istanza. Le istanze automatiche e denominate di `LocalDB` possono essere condivisi. Per condividere un'istanza di `LocalDB`, un utente ne seleziona un nome condiviso (alias). Poiché il nome condiviso è visibile a tutti gli utenti del computer, questo nome condiviso deve essere univoco nel computer. Il nome condiviso per un'istanza di `LocalDB` ha lo stesso formato dell'istanza denominata di `LocalDB`.  
  
 Solo un amministratore del computer può creare un'istanza condivisa di `LocalDB`. Un'istanza condivisa di `LocalDB` può essere annullata da un amministratore o dal proprietario dell'istanza condivisa di `LocalDB`. Per condividere e annullare la condivisione di un'istanza di `LocalDB`, usare il `LocalDBShareInstance` e `LocalDBUnShareInstance` metodi del `LocalDB` API, o la condivisione e opzioni annullata la condivisione dell'utilità SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Avvio e connessione a LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Connessione all'istanza automatica  
 Il modo più semplice da utilizzare `LocalDB` consiste nel connettersi all'istanza automatica dell'utente corrente usando la stringa di connessione **"Server = (localdb) \MSSQLLocalDB;Integrated Security = true"** . Per connettersi a un database specifico usando il nome del file, usare una stringa di connessione simile a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"** .  
  
> [!NOTE]  
>  La prima volta un utente in un computer tenta di connettersi a `LocalDB`, l'istanza automatica deve essere creato e avviato. Il tempo aggiuntivo necessario per la creazione dell'istanza può determinare un errore di tentativo di connessione generando un messaggio di timeout. In una situazione simile, attendere pochi secondi per consentire il completamento del processo di creazione, quindi riconnettersi.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Creazione e connessione alle istanze denominate  
 Oltre all'istanza automatica, `LocalDB` supporta anche istanze denominate. Utilizzare il programma SqlLocalDB.exe per creare, avviare e arrestare un'istanza denominata di `LocalDB`. Per altre informazioni su SqlLocalDB.exe, vedere [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
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
|Version|\<Versione corrente>|  
|Nome condiviso|""|  
|Proprietario|"\<utente di Windows>"|  
|Creazione automatica|No|  
|State|esecuzione|  
|Ultima ora inizio|\<Data e ora>|  
|Nome pipe dell'istanza|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se l'applicazione usa una versione di .NET precedente 4.0.2 è necessario connettersi direttamente alla named pipe del `LocalDB`. Il valore nome pipe dell'istanza è la named pipe su cui l'istanza di `LocalDB` è in ascolto. La parte del nome pipe dell'istanza dopo che LOCALDB # verrà modificata a ogni avvio dell'istanza di `LocalDB` viene avviato. Per connettersi all'istanza di `LocalDB` usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], digitare il nome pipe dell'istanza nel **nome Server** finestra del **connettersi a [!INCLUDE[ssDE](../../includes/ssde-md.md)]**  nella finestra di dialogo. Dal programma personalizzato è possibile stabilire una connessione all'istanza di `LocalDB` usando una stringa di connessione simile a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Connessione a un'istanza condivisa di LocalDB  
 Per connettersi a un'istanza condivisa di `LocalDB` aggiungere **.\\**  (punto + barra rovesciata) alla stringa di connessione per fare riferimento a spazio dei nomi riservato per le istanze condivise. Ad esempio, per connettersi a un'istanza condivisa di `LocalDB` denominate `AppData` usano una stringa di connessione, ad esempio `(localdb)\.\AppData` come parte della stringa di connessione. Un utente che si connette a un'istanza condivisa del `LocalDB` di cui è proprietario non deve avere un'autenticazione di Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso con autenticazione.  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
 Per informazioni sulla risoluzione dei problemi `LocalDB`, vedere [risoluzione dei problemi di SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permissions  
 Un'istanza di [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` è un'istanza creata da un utente per l'uso. Qualsiasi utente nel computer può creare un database utilizzando un'istanza di `LocalDB`, archiviando i file nel proprio profilo utente ed eseguendo il processo con le relative credenziali. Per impostazione predefinita, l'accesso all'istanza di `LocalDB` è limitato al relativo proprietario. I dati contenuti nel `LocalDB` è protetta da accesso al file system ai file di database. Se i file di database utente vengono archiviati in un percorso condiviso, il database può essere aperto da qualsiasi utente con accesso al file system in quel percorso usando un'istanza di `LocalDB` che sono proprietari. Se i file di database si trovano in un percorso protetto, ad esempio la cartella dati utente, solo quell'utente e gli amministratori con accesso a quella cartella, possono aprire il database. Il `LocalDB` i file possono essere aperti solo da un'istanza del `LocalDB` alla volta.  
  
> [!NOTE]  
>  `LocalDB` viene eseguito sempre nel contesto di sicurezza dell'utente. vale a dire, `LocalDB` non viene mai eseguito con le credenziali dal gruppo Administrators locale. Ciò significa che tutti i file di database usati da un `LocalDB` istanza deve essere accessibile mediante l'account di Windows dell'utente proprietario, senza considerare l'appartenenza al gruppo Administrators locale.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità SqlLocalDB](../../tools/sqllocaldb-utility.md)  
  
  
