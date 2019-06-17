---
title: Overview (SMO) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b66a0c9efc94d648eba2f4d4f8cff779def413fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131794"
---
# <a name="overview-smo"></a>Panoramica (SMO)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) sono progettati per la gestione a livello di programmazione di oggetti [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile utilizzare SMO per compilare applicazioni di gestione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizzate. Sebbene [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sia un'applicazione potente e completa per la gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], in alcuni casi è possibile che sia necessario utilizzare un'applicazione SMO.  
  
 È possibile, ad esempio, che sia necessario semplificare le applicazioni utente che controllano le attività di gestione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per soddisfare le necessità di nuovi utenti e ridurre i costi di formazione. È possibile dovere creare database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizzati o creare un'applicazione per la creazione e il controllo dell'efficienza degli indici. Un'applicazione SMO può anche essere utilizzata per includere perfettamente hardware o software di terze parti nell'applicazione per la gestione di database.  
  
 Il modello a oggetti SMO estende e sostituisce il modello a oggetti SQL-DMO (Distributed Management Objects). Rispetto a SQL-DMO, SMO migliora prestazioni, controllo e semplicità di utilizzo. La maggior parte della funzionalità di SQL-DMO è inclusa in SMO e sono disponibili diverse classi nuove che supportano le nuove funzionalità presenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il modello a oggetti è intuitivo e, se possibile, consente l'utilizzo della terminologia di SQL-DMO per semplificare il trasferimento delle competenze.  
  
 Poiché SMO è compatibile con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, è possibile gestire facilmente un ambiente in cui sono presenti più versioni.  
  
 Di seguito sono elencate le nuove funzionalità di SMO:  
  
-   Modello a oggetti memorizzato nella cache e creazione ottimizzata delle istanze degli oggetti. Gli oggetti vengono caricati solo quando viene fatto loro riferimento in modo specifico. Le proprietà degli oggetti vengono caricate solo parzialmente quando si creano gli oggetti. Gli oggetti e le proprietà rimanenti vengono caricati quando viene fatto loro riferimento in modo diretto.  
  
-   Esecuzione in batch delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Le istruzioni vengono eseguite in batch per migliorare le prestazioni della rete.  
  
-   Acquisizione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Consente l'acquisizione di qualsiasi operazione in uno script. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] questa funzionalità viene utilizzata per creare uno script di un'operazione anziché eseguirla immediatamente.  
  
-   Gestione dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il provider WMI. I servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere avviati, arrestati e sospesi a livello di codice.  
  
-   Generazione di script avanzata. Gli script [!INCLUDE[tsql](../../includes/tsql-md.md)] possono essere generati per ricreare oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consentono di descrivere le relazioni con altri oggetti nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzo di nomi di risorse univoci (URN). Un URN consente di creare istanze di oggetti SMO e di farvi riferimento.  
  
 In SMO sono inoltre rappresentati come nuovi oggetti o proprietà molte funzionalità e componenti introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Queste nuove funzionalità e componenti includono:  
  
-   Partizionamento di tabelle e indici per l'archiviazione di dati in uno schema di partizione. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
-   Endpoint HTTP per la gestione di richieste SOAP. Per altre informazioni, vedere [implementazione di endpoint](tasks/implementing-endpoints.md).  
  
-   Isolamento dello snapshot e controllo delle versioni a livello di riga per maggiore concorrenza. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../native-client/features/working-with-snapshot-isolation.md).  
  
-   La raccolta di XML Schema, gli indici XML e il tipo di dati XML garantiscono la convalida e l'archiviazione di dati XML. Per altre informazioni, vedere [raccolte di XML Schema &#40;SQL Server&#41; ](../xml/xml-schema-collections-sql-server.md) e [utilizzando gli schemi XML](tasks/using-xml-schemas.md).  
  
-   Database di snapshot per la creazione di copie di database in sola lettura.  
  
-   Supporto di [!INCLUDE[ssSB](../../includes/sssb-md.md)] per la comunicazione basata su messaggi. Per altre informazioni, vedere [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md).  
  
-   Supporto di sinonimi per più nomi di oggetti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [sinonimi &#40;motore di Database&#41;](../synonyms/synonyms-database-engine.md).  
  
-   Gestione di Posta elettronica database consente di creare server, profili e account di posta elettronica in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Posta elettronica database](../database-mail/database-mail.md).  
  
-   Supporto di Server registrati per la registrazione di informazioni di connessione. Per altre informazioni, vedere [Registra server](../../ssms/register-servers/register-servers.md).  
  
-   Traccia e riproduzione di eventi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md), [traccia SQL](../sql-trace/sql-trace.md), [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md), e [degli eventi estesi](../extended-events/extended-events.md).  
  
-   Supporto di certificati e chiavi per il controllo di sicurezza. Per altre informazioni, vedere [gerarchia di crittografia](../security/encryption/encryption-hierarchy.md).  
  
-   Trigger DDL per l'aggiunta di funzionalità quando si verificano eventi DDL. Per altre informazioni, vedere [Trigger DDL](../triggers/ddl-triggers.md).  
  
 Lo spazio dei nomi SMO è <xref:Microsoft.SqlServer.Management.Smo>. SMO viene implementato come assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Ciò significa che Common Language Runtime (CLR) da [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versione 2.0 deve essere installato prima di utilizzare gli oggetti SMO. Gli assembly SMO vengono installati per impostazione predefinita nel Global Assembly Cache (GAC) con l'opzione SDK di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli assembly si trovano in [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]. Per altre informazioni, vedere la [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentazione.  
  
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
  
## <a name="new-smo-features"></a>Nuove funzionalità SMO  
 **Prestazioni ottimizzate**  
  
 In SQL-DMO l'enumerazione degli oggetti richiedeva la creazione di un'istanza completa di ogni oggetto all'interno di una raccolta. Tale operazione non è efficiente in termini di rete e footprint di memoria. In molte situazioni è possibile creare l'istanza di un oggetto senza fare riferimento in modo esplicito alla maggior parte delle relative proprietà.  
  
 L'architettura SMO è più efficiente in termini di memoria poiché inizialmente viene creata solo un'istanza parziale degli oggetti e le informazioni minime sulle proprietà vengono richieste dal server. La creazione di un'istanza completa degli oggetti viene posticipata fino a quando non viene fatto riferimento all'oggetto in modo esplicito. L'istanza completa di un oggetto viene creata un'istanza quando viene richiesta una proprietà che non fa parte del set di proprietà recuperate inizialmente o quando viene chiamato un metodo che richiede tale proprietà. La transizione tra la creazione di un'istanza parziale e un'istanza completa degli oggetti è visibile all'utente. Inoltre, alcune proprietà che utilizzano molta memoria non vengono mai recuperate, a meno che non venga fatto riferimento alla proprietà in modo esplicito. Un esempio è la proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> della proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>. Tuttavia, la creazione di un'istanza parziale richiede più tempo di round trip in rete e potrebbe non essere la migliore opzione per le prestazioni ottimizzate dell'applicazione.  
  
 È possibile controllare la creazione di un'istanza in base all'ambiente di sistema. La creazione di un'istanza posticipata riduce la quantità di memoria richiesta dall'applicazione, sebbene possa generare molte richieste del server quando viene fatto riferimento alle proprietà.  
  
 Le classi di istanze, ovvero gli oggetti che rappresentano gli oggetti di database reali, possono avere tre livelli di creazione di un'istanza: livello minimo quando vengono lette in un solo blocco solo le proprietà necessarie minime, livello parziale quando vengono lette in un solo blocco tutte le proprietà che utilizzano un quantità di memoria relativamente grande e livello completo. Gli stati tradizionali della creazione di un'istanza sono lo stato completo e lo stato non istanziato. Lo stato parziale aumenta l'efficienza poiché la creazione di un'istanza parziale di un oggetto non contiene valori per il set completo delle proprietà dell'oggetto. Lo stato parziale è lo stato predefinito per un oggetto al quale non viene fatto direttamente riferimento. Quando viene fatto riferimento a una di queste proprietà, viene generato un errore in cui viene richiesta la creazione di un'istanza completa dell'oggetto.  
  
 **Esecuzione dell'acquisizione**  
  
 L'esecuzione diretta è il metodo di esecuzione standard. Le istruzioni vengono inviate direttamente a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appena vengono generate. L'esecuzione dell'acquisizione rappresenta il metodo alternativo.  
  
 L'esecuzione dell'acquisizione consente di acquisire i batch [!INCLUDE[tsql](../../includes/tsql-md.md)] generalmente eseguiti, consentendo così al programmatore SMO di posticipare lo script, archiviarlo per un'esecuzione successiva o fornire un'anteprima per l'utente finale. È possibile ad esempio inviare in un unico batch un'istruzione `create database`, un'istruzione `create table` e un'istruzione `create index` ed effettuare l'esecuzione come tre passaggi sequenziali. Questa funzionalità viene controllata dall'utente tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>.  
  
 **Provider WMI**  
  
 In SMO sono inclusi gli oggetti del provider WMI, fornendo al programmatore SMO un modello a oggetti semplice che è molto simile alle classi SMO, senza dovere necessariamente comprendere il modello di programmazione rappresentato dallo spazio dei nomi e dai dettagli del provider WMI di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il provider WMI consente di configurare servizi, alias e librerie di rete client e server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Scripting**  
  
 In SMO la generazione di script è stata migliorata e spostata nella classe `Scripter`. Il `Scripter` classe può individuare dipendenze, comprendere le relazioni tra oggetti e consentire la modifica della gerarchia di dipendenze. L'oggetto scripting principale è l'oggetto `Scripter`. Sono inoltre disponibili diversi oggetti di supporto che gestiscono le dipendenze e rispondono agli eventi di stato e di errore.  
  
 L'oggetto `Scripter` supporta le seguenti opzioni di scripting avanzate:  
  
-   Scripting semplice in una fase (crea lo script in un unico passaggio)  
  
-   Scripting avanzato in tre fasi (crea lo script in tre passaggi: individuazione dipendenze, generazione elenchi e generazione script)  
  
-   Individuazione dipendenze in due modi (consente l'individuazione di dipendenze o di dipendenti)  
  
-   Risposta agli eventi di stato  
  
-   Risposta agli eventi di errore  
  
 **Nomi di risorse univoci**  
  
 Un concetto chiave nell'utilizzo della libreria di oggetti SMO è rappresentato dai nomi di risorse univoci (URN, Unique Resource Name). L'URN utilizza una sintassi simile a XPath. XPath è un percorso della gerarchia utilizzato per specificare un oggetto nel quale ogni livello dispone di qualificatori e funzioni. In SMO l'URN dispone di due elementi: percorso e denominazione degli attributi con funzionalità limitata. Il percorso viene utilizzato per specificare il percorso dell'oggetto mentre la denominazione degli attributi consente un grado di filtraggio.  
  
 Un esempio di URN per un database è:  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 L'URN di un oggetto può essere recuperato facendo riferimento alla proprietà dell'URN. L'oggetto Scripter utilizza inoltre gli URN come parametri che passano i riferimenti all'oggetto al metodo dell'oggetto `Scripter`. Inoltre, è possibile specificare un URN per il **GetSmoObject** metodo il `Server` oggetto. utilizzato per creare un'istanza dell'oggetto SMO.  
  
## <a name="new-sql-server-features-represented-in-smo"></a>Nuove funzionalità di SQL Server rappresentate in SMO  
 **Partizionamento di tabelle e indici**  
  
 Il partizionamento di tabelle e indici consente di gestire la distribuzione di dati in tabelle e indici attraverso filegroup. Questa nuova funzionalità viene rappresentata mediante oggetti SMO.  
  
 **EndPoints**  
  
 Le richieste di mirroring del database e SOAP vengono gestite dagli endpoint mediante l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Endpoint>.  
  
 **Controllo delle versioni a livello di riga/isolamento dello snapshot**  
  
 L'isolamento dello snapshot (controllo delle versioni a livello di riga) è rappresentato da nuove proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **XML Schema Namespace, gli indici XML e tipo di dati XML**  
  
 Gli spazi dei nomi di XML Schema sono rappresentati in SMO da una raccolta di oggetti. Gli indici XML sono rappresentati in SMO da una proprietà dell'oggetto `Index`.  
  
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
  
## <a name="smo-and-sql-dmo"></a>SMO e SQL-DMO  
 Il modello a oggetti SMO sostituisce SQL-DMO. SMO supporta [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Supporta più attività di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e contiene molte funzionalità nuove di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. SMO è progettato per essere più efficiente e fornire un maggiore controllo.  
  
 La libreria DMO è un modello a oggetti COM, mentre SMO viene implementato come assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. I componenti COM sono librerie che forniscono funzionalità riutilizzabili per le applicazioni e per la programmazione di applicazioni non gestite. Gli assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] forniscono funzionalità riutilizzabili per [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per la scrittura di applicazioni in codice gestito.  
  
 Durante la transizione alla tecnologia [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile avere applicazioni scritte in parte in codice gestito e in parte in codice non gestito. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] consente di interfacciarsi con i componenti COM che richiedono un assembly di interoperabilità primario. È necessario un wrapper di runtime per SQL-DMO in modo che possa essere chiamato da un'applicazione basata su [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di base relativi a RMO (Replication Management Objects)](../replication/concepts/replication-management-objects-concepts.md)  
  
  
