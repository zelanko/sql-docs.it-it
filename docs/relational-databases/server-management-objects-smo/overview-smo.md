---
title: Panoramica (SMO) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44e7ca81fd276e8538e19c1a7670daf4da10dde6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097998"
---
# <a name="overview-smo"></a>Panoramica (SMO)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) sono progettati per la gestione a livello di programmazione di oggetti [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile utilizzare SMO per compilare applicazioni di gestione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizzate. Sebbene [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sia un'applicazione potente e completa per la gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in alcuni casi è possibile che sia necessario utilizzare un'applicazione SMO.  
  
 È possibile, ad esempio, che sia necessario semplificare le applicazioni utente che controllano le attività di gestione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per soddisfare le necessità di nuovi utenti e ridurre i costi di formazione. È possibile dovere creare database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizzati o creare un'applicazione per la creazione e il controllo dell'efficienza degli indici. Un'applicazione SMO può anche essere utilizzata per includere perfettamente hardware o software di terze parti nell'applicazione per la gestione di database.  
  
 Poiché SMO è compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, è possibile gestire facilmente un ambiente in cui sono presenti più versioni.  
  
 Le funzionalità in SMO includono quanto segue:  
  
-   Modello a oggetti memorizzato nella cache e creazione ottimizzata delle istanze degli oggetti. Gli oggetti vengono caricati solo quando viene fatto loro riferimento in modo specifico. Le proprietà degli oggetti vengono caricate solo parzialmente quando si creano gli oggetti. Gli oggetti e le proprietà rimanenti vengono caricati quando viene fatto loro riferimento in modo diretto.  
  
-   Esecuzione in batch delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Le istruzioni vengono eseguite in batch per migliorare le prestazioni della rete.  
  
-   Acquisizione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Consente l'acquisizione di qualsiasi operazione in uno script. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] questa funzionalità viene utilizzata per creare uno script di un'operazione anziché eseguirla immediatamente.  
  
-   Gestione dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il provider WMI. I servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere avviati, arrestati e sospesi a livello di codice.  
  
-   Generazione di script avanzata. Gli script [!INCLUDE[tsql](../../includes/tsql-md.md)] possono essere generati per ricreare oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consentono di descrivere le relazioni con altri oggetti nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzo di nomi di risorse univoci (URN). Un URN consente di creare istanze di oggetti SMO e di farvi riferimento.  
  
 In SMO sono inoltre rappresentati come nuovi oggetti o proprietà molte funzionalità e componenti introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Queste nuove funzionalità e componenti includono:  
  
-   Partizionamento di tabelle e indici per l'archiviazione di dati in uno schema di partizione. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
-   Endpoint HTTP per la gestione di richieste SOAP. Per altre informazioni, vedere [implementazione di endpoint](../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md).  
  
-   Isolamento dello snapshot e controllo delle versioni a livello di riga per maggiore concorrenza. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
-   La raccolta di XML Schema, gli indici XML e il tipo di dati XML garantiscono la convalida e l'archiviazione di dati XML. Per altre informazioni, vedere [raccolte di XML Schema &#40;SQL Server&#41; ](../../relational-databases/xml/xml-schema-collections-sql-server.md) e [utilizzando gli schemi XML](../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md).  
  
-   Database di snapshot per la creazione di copie di database in sola lettura.  
  
-   Supporto di [!INCLUDE[ssSB](../../includes/sssb-md.md)] per la comunicazione basata su messaggi. Per altre informazioni, vedere [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md).  
  
-   Supporto di sinonimi per più nomi di oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [sinonimi &#40;motore di Database&#41;](../../relational-databases/synonyms/synonyms-database-engine.md).  
  
-   Gestione di Posta elettronica database consente di creare server, profili e account di posta elettronica in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Posta elettronica database](../../relational-databases/database-mail/database-mail.md).  
  
-   Supporto di Server registrati per la registrazione di informazioni di connessione. Per altre informazioni, vedere [Registra server](../../tools/sql-server-management-studio/register-servers.md).  
  
-   Traccia e riproduzione di eventi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md), [traccia SQL](../../relational-databases/sql-trace/sql-trace.md), [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md), e [degli eventi estesi](../../relational-databases/extended-events/extended-events.md).  
  
-   Supporto di certificati e chiavi per il controllo di sicurezza. Per altre informazioni, vedere [gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
-   Trigger DDL per l'aggiunta di funzionalità quando si verificano eventi DDL. Per altre informazioni, vedere [Trigger DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
 Lo spazio dei nomi SMO è <xref:Microsoft.SqlServer.Management.Smo>. SMO viene implementato come assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Ciò significa che Common Language Runtime (CLR) da [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versione 2.0 deve essere installato prima di utilizzare gli oggetti SMO. Gli assembly SMO vengono installati per impostazione predefinita nel Global Assembly Cache (GAC) con l'opzione SDK di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli assembly si trovano in C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\. Per altre informazioni, vedere la [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentazione.  
  
## <a name="smo-classes"></a>Classi SMO  
 Le classi SMO includono due categorie: classi di istanze e classi di utilità.  
  
 **Classi di istanze**  
  
 Le classi di istanze rappresentano gli oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quali esempio server, database, tabelle, trigger e stored procedure. La classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> viene utilizzata per stabilire una connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e per controllare la modalità di acquisizione dei comandi inviati.  
  
 Gli oggetti dell'istanza SMO formano una gerarchia che rappresenta la gerarchia di un server di database. All'inizio sono presenti le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguiti dai database, quindi dalle tabelle, le colonne, i trigger e così via. Se è presente una relazione che prevede un elemento padre per molti elementi figlio, ad esempio una tabella contenente una o più colonne, l'elemento figlio verrà rappresentato da una raccolta di oggetti. In caso contrario l'elemento figlio sarà rappresentato solo da un oggetto.  
  
 **Classi di utilità**  
  
 Le classi di utilità sono un gruppo di oggetti creato in modo esplicito per eseguire attività specifiche. Sono state divise in diverse gerarchie di oggetti in base alla funzione:  
  
-   Classe di trasferimento. Utilizzata per trasferire lo schema e i dati in un altro database.  
  
-   Classi di backup e ripristino. Utilizzate per eseguire il backup e il ripristino di database.  
  
-   Classe di script. Utilizzata per creare file script per la rigenerazione di oggetti e le relative dipendenze.  
  
## <a name="smo-features"></a>Funzionalità SMO  
 **Prestazioni ottimizzate**  
  
 L'architettura SMO è efficiente in termini di memoria perché vengono create istanze degli oggetti solo parzialmente all'inizio e informazioni sulle proprietà minima è richiesta dal server. La creazione di un'istanza completa degli oggetti viene posticipata fino a quando non viene fatto riferimento all'oggetto in modo esplicito. L'istanza completa di un oggetto viene creata un'istanza quando viene richiesta una proprietà che non fa parte del set di proprietà recuperate inizialmente o quando viene chiamato un metodo che richiede tale proprietà. La transizione tra la creazione di un'istanza parziale e un'istanza completa degli oggetti è visibile all'utente. Inoltre, alcune proprietà che utilizzano molta memoria non vengono mai recuperate, a meno che non venga fatto riferimento alla proprietà in modo esplicito. Un esempio è la proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> della proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>. Tuttavia, la creazione di un'istanza parziale richiede più tempo di round trip in rete e potrebbe non essere la migliore opzione per le prestazioni ottimizzate dell'applicazione.  
  
 È possibile controllare la creazione di un'istanza in base all'ambiente di sistema. La creazione di un'istanza posticipata riduce la quantità di memoria richiesta dall'applicazione, sebbene possa generare molte richieste del server quando viene fatto riferimento alle proprietà.  
  
 Le classi di istanze, ovvero gli oggetti che rappresentano gli oggetti di database reali, possono avere tre livelli di creazione di un'istanza: livello minimo quando vengono lette in un solo blocco solo le proprietà necessarie minime, livello parziale quando vengono lette in un solo blocco tutte le proprietà che utilizzano un quantità di memoria relativamente grande e livello completo. Gli stati tradizionali della creazione di un'istanza sono lo stato completo e lo stato non istanziato. Lo stato parziale aumenta l'efficienza poiché la creazione di un'istanza parziale di un oggetto non contiene valori per il set completo delle proprietà dell'oggetto. Lo stato parziale è lo stato predefinito per un oggetto al quale non viene fatto direttamente riferimento. Quando viene fatto riferimento a una di queste proprietà, viene generato un errore in cui viene richiesta la creazione di un'istanza completa dell'oggetto.  
  
 **Esecuzione dell'acquisizione**  
  
 L'esecuzione diretta è il metodo di esecuzione standard. Le istruzioni vengono inviate direttamente a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appena vengono generate. L'esecuzione dell'acquisizione rappresenta il metodo alternativo.  
  
 L'esecuzione dell'acquisizione consente di acquisire i batch [!INCLUDE[tsql](../../includes/tsql-md.md)] generalmente eseguiti, consentendo così al programmatore SMO di posticipare lo script, archiviarlo per un'esecuzione successiva o fornire un'anteprima per l'utente finale. Ad esempio, un **create database**, un **Crea tabella**e un **Crea indice** istruzione può essere inviata in un unico batch e quindi eseguire come tre passaggi sequenziali. Questa funzionalità viene controllata dall'utente tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>.  
  
 **Provider WMI**  
  
 In SMO sono inclusi gli oggetti del provider WMI, fornendo al programmatore SMO un modello a oggetti semplice che è molto simile alle classi SMO, senza dovere necessariamente comprendere il modello di programmazione rappresentato dallo spazio dei nomi e dai dettagli del provider WMI di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il provider WMI consente di configurare servizi, alias e librerie di rete client e server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Scripting**  
  
 In SMO la creazione di script è stato migliorato e spostati nel **Scripter** classe. Il **Scripter** classe può individuare dipendenze, comprendere le relazioni tra oggetti e consentire la modifica della gerarchia di dipendenze. L'oggetto scripting principale è il **Scripter** oggetto. Sono inoltre disponibili diversi oggetti di supporto che gestiscono le dipendenze e rispondono agli eventi di stato e di errore.  
  
 Il **Scripter** oggetto supporta le seguenti opzioni di scripting avanzate:  
  
-   Scripting semplice in una fase (crea lo script in un unico passaggio)  
  
-   Fase 3 di scripting avanzate (Crea lo script in tre passaggi; individuazione delle dipendenze, la generazione dell'elenco, la generazione di script)  
  
-   Individuazione dipendenze in due modi (consente l'individuazione di dipendenze o di dipendenti)  
  
-   Risposta agli eventi di stato  
  
-   Risposta agli eventi di errore  
  
 **Nomi di risorse univoci**  
  
 Un concetto chiave nell'utilizzo della libreria di oggetti SMO è rappresentato dai nomi di risorse univoci (URN, Unique Resource Name). L'URN utilizza una sintassi simile a XPath. XPath è un percorso della gerarchia utilizzato per specificare un oggetto nel quale ogni livello dispone di qualificatori e funzioni. In SMO l'URN dispone di due elementi: percorso e denominazione degli attributi con funzionalità limitata. Il percorso viene utilizzato per specificare il percorso dell'oggetto mentre la denominazione degli attributi consente un grado di filtraggio.  
  
 Un esempio di URN per un database è:  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 L'URN di un oggetto può essere recuperato facendo riferimento alla proprietà dell'URN. L'oggetto Scripter utilizza inoltre gli URN come parametri che passano riferimenti a oggetti per il metodo di **Scripter** oggetto. Inoltre, è possibile specificare un URN per il **GetSmoObject** metodo per il **Server** oggetto. utilizzato per creare un'istanza dell'oggetto SMO.  
  
## <a name="sql-server-features-represented-in-smo"></a>Funzionalità di SQL Server rappresentate in SMO  
 **Partizionamento di tabelle e indici**  
  
 Il partizionamento di tabelle e indici consente di gestire la distribuzione di dati in tabelle e indici attraverso filegroup. Questa nuova funzionalità viene rappresentata mediante oggetti SMO.  
  
 **EndPoints**  
  
 Le richieste di mirroring del database e SOAP vengono gestite dagli endpoint mediante l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Endpoint>.  
  
 **Controllo delle versioni a livello di riga/isolamento dello snapshot**  
  
 L'isolamento dello snapshot (controllo delle versioni a livello di riga) è rappresentato da nuove proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **XML Schema Namespace, gli indici XML e tipo di dati XML**  
  
 Gli spazi dei nomi di XML Schema sono rappresentati in SMO da una raccolta di oggetti. Gli indici XML sono rappresentati in SMO da un **indice** proprietà dell'oggetto.  
  
 **Miglioramenti della ricerca full-Text**  
  
 In SMO vengono forniti nuovi oggetti che rappresentano i miglioramenti alla ricerca full-text.  
  
 **Verifica pagina**  
  
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> rappresenta le opzioni di verifica pagina del database.  
  
 **Snapshot di database**  
  
 Un database snapshot è una copia di sola lettura di un database specifico in un momento specifico. Un database snapshot può essere specificato tramite la proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **Service Broker**  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] e la relativa funzionalità sono rappresentati da un gruppo di oggetti  
  
 **Miglioramenti degli indici**  
  
 I miglioramenti degli indici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono rappresentati da nuove proprietà nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Index>.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di base relativi a RMO (Replication Management Objects)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
