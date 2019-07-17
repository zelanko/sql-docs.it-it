---
ms.openlocfilehash: 1394414db170826fa96ca51a5d35ff8dea199310
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68212268"
---
Questo articolo offre una panoramica delle soluzioni di continuità aziendale per la disponibilità elevata e il ripristino di emergenza in SQL Server. 

Un'attività comune di cui deve tenere conto chiunque esegua una distribuzione di SQL Server è verificare se tutte le istanze cruciali di SQL Server e i database all'interno delle stesse sono disponibili quando gli utenti finali e aziendali ne hanno bisogno, ovvero in orario di ufficio o 24 ore su 24. L'obiettivo è fare in modo che le interruzioni delle attività aziendali siano minime o inesistenti. Questo concetto è noto anche come continuità aziendale.

SQL Server 2017 introduce molte nuove funzionalità o miglioramenti di quelle già esistenti, alcune delle quali riguardano la disponibilità. L'elemento più importante aggiunto a SQL Server 2017 è il supporto per SQL Server nelle distribuzioni di Linux. Per un elenco completo delle nuove funzionalità in SQL Server 2017, vedere l'argomento [Novità di SQL Server](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017).

Questo articolo descrive in particolare gli scenari di disponibilità in SQL Server 2017, nonché le funzionalità di disponibilità, sia nuove che ottimizzate, offerte da SQL Server 2017. Gli scenari includono soluzioni ibride in grado di coprire le distribuzioni di SQL Server sia in Windows Server che in Linux, nonché le soluzioni che consentono di aumentare il numero di copie leggibili di un database. Questo articolo non tratta le opzioni di disponibilità esterne a SQL Server, ad esempio quelle offerte dalla virtualizzazione, ma tutti gli argomenti trattati riguardano le installazioni di SQL Server in una macchina virtuale guest sia nel cloud pubblico, sia in hosting in un server hypervisor locale.

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>Scenari di SQL Server 2017 che usano le funzionalità di disponibilità

Gruppi di disponibilità, FCI e log shipping possono essere usati in molti modi e non necessariamente solo ai fini della disponibilità. Le funzionalità di disponibilità possono essere usate sostanzialmente in quattro modi:

* Disponibilità elevata
* Ripristino di emergenza
* Migrazioni e aggiornamenti
* Scalabilità orizzontale delle copie leggibili di uno o più database

Ogni sezione descrive le funzionalità rilevanti che possono essere usate in uno scenario specifico. L'unica funzionalità non coperta è la [replica di SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication). Benché non sia ufficialmente designata come funzionalità di disponibilità dell'ambiente Always On, viene spesso usata per rendere ridondanti i dati in determinati scenari. La replica verrà aggiunta a SQL Server in Linux in una versione futura.

> [!IMPORTANT] 
> Le funzionalità di disponibilità di SQL Server non sostituiscono la necessità di adottare una strategia efficace e adeguatamente testata per il backup e il ripristino, aspetto imprescindibile di qualsiasi soluzione di disponibilità.

### <a name="high-availability"></a>Disponibilità elevata

È importante verificare che il database o le istanze di SQL Server siano disponibili nel caso in cui si riscontri un problema a livello locale in un data center o una singola area del cloud. Questa sezione spiega in che modo le funzionalità di disponibilità di SQL Server possono essere utili per svolgere tale attività. Tutte le funzionalità descritte sono disponibili sia in Windows Server che in Linux. 

#### <a name="always-on-availability-groups"></a>Gruppi di disponibilità Always On

Introdotti in SQL Server 2012, i gruppi di disponibilità Always On offrono una protezione a livello di database in cui ogni transazione di un database viene inviata a un'altra istanza, nota come replica, che contiene una copia di quel database in uno stato speciale. Un gruppo di disponibilità può essere distribuito in Standard o Enterprise Edition.  Le istanze che fanno parte di un gruppo di disponibilità possono essere autonome o istanze del cluster di failover Always On (FCI), descritte nella sezione successiva. Poiché le transazioni vengono inviate a una replica in tempo reale, i gruppi di disponibilità sono consigliati in situazioni che richiedono valori inferiori per il punto di recupero e gli obiettivi del tempo di recupero. Lo spostamento dei dati tra le repliche può essere sincrono o asincrono. Enterprise Edition consente fino a tre repliche, inclusa quella primaria, sincrone. Un gruppo di disponibilità ha una copia del database con funzioni di lettura/scrittura complete nella replica primaria, mentre tutte le repliche secondarie non ricevono le transazioni direttamente da utenti finali o applicazioni. 

> [!NOTE] 
> Always On è un termine generico per le funzionalità di disponibilità in SQL Server e si riferisce sia ai gruppi di disponibilità che alle istanze del cluster di failover. Always On non è il nome della funzionalità gruppo di disponibilità.

Poiché i gruppi di disponibilità assicurano la protezione solo a livello di database e non a livello di istanza, tutto ciò che non viene acquisito nel log delle transazioni o configurato nel database dovrà essere sincronizzato manualmente per ogni replica secondaria. Alcuni esempi di oggetti che devono essere sincronizzati manualmente sono gli accessi a livello di istanza, i server collegati e SQL Server Agent - processi.

Un gruppo di disponibilità ha anche un altro componente denominato listener, che consente alle applicazioni e agli utenti finali di connettersi senza dover sapere quale istanza di SQL Server ospita la replica primaria. Ogni gruppo di disponibilità ha il proprio listener. Le implementazioni del listener sono leggermente diverse in Windows Server rispetto a Linux, ma la funzionalità e la modalità di utilizzo sono le stesse. L'immagine seguente illustra un gruppo di disponibilità basato su Windows Server che usa Windows Server Failover Cluster (WSFC). Sia in Linux che in Windows Server è necessario un cluster sottostante a livello di sistema operativo per la disponibilità. Nell'esempio viene illustrata una configurazione semplice a due server, o nodi, in cui un cluster WSFC è il cluster sottostante. 

![Gruppo di disponibilità semplice](media/sql-server-ha-story/image1.png)
 
Standard Edition ed Enterprise Edition hanno valori massimi diversi per quanto riguarda le repliche. Un gruppo di disponibilità in Standard Edition, noto come gruppo di disponibilità di base, supporta due repliche, una primaria e una secondaria, con un singolo database nel gruppo di disponibilità. Enterprise Edition non solo consente la configurazione di più database in un unico gruppo di disponibilità, ma può anche avere fino a nove repliche in totale, una primaria e otto secondarie. Enterprise Edition offre anche altri vantaggi facoltativi, ad esempio le repliche secondarie leggibili, la possibilità di eseguire copie di backup da una replica secondaria e altro ancora.

>[!NOTE]
> Il mirroring del database, deprecato in SQL Server 2012, non è disponibile nella versione di SQL Server per Linux e non verrà aggiunto. I clienti che usano ancora il mirroring del database devono iniziare a pianificare la migrazione ai gruppi di disponibilità, che sostituiscono il mirroring del database.

Rispetto alla disponibilità, i gruppi di disponibilità possono offrire il failover automatico o manuale. Il failover automatico può verificarsi se è configurato lo spostamento sincrono dei dati e i database nella replica primaria e secondaria sono in uno stato sincronizzato. Purché venga usato il listener e l'applicazione usi una versione successiva di .NET (3.5 con un aggiornamento o 4.0 e versioni successive), il failover viene gestito in modo da non incidere, o avere un impatto minimo, sugli utenti finali se si usa un listener. Il failover per trasformare una replica secondaria nella nuova replica primaria può essere configurato in modo da essere automatico o manuale e in genere viene misurato in secondi.

Nell'elenco che segue sono evidenziate alcune differenze tra Windows Server e Linux rispetto ai gruppi di disponibilità:
* A causa delle differenze di funzionamento del cluster sottostante tra Linux e Windows Server, tutti i failover, manuali o automatici, dei gruppi di disponibilità vengono eseguiti usando il cluster di Linux. Nelle distribuzioni dei gruppi di disponibilità basati su Windows Server i failover manuali devono essere eseguiti usando SQL Server. I failover automatici vengono gestiti dal cluster sottostante sia in Windows Server che in Linux. 
* In SQL Server 2017 la configurazione consigliata per i gruppi di disponibilità in Linux sarà un minimo di tre repliche. Ciò è dovuto il modo in cui funziona il cluster sottostante. Una soluzione ottimizzata per una configurazione a due repliche sarà disponibile dopo il rilascio.
* In Linux il nome comune usato da ogni listener è definito in DNS e non nel cluster come in Windows Server.

In SQL Server 2017 sono disponibili alcune nuove funzionalità e miglioramenti ai gruppi di disponibilità:

* Tipi di cluster
* REQUIRED_SECONDARIES_TO_COMMIT
* Supporto ottimizzato di Microsoft Distributed Transaction Coordinator (DTC) per le configurazioni basate su Windows Server
* Scenari di scalabilità orizzontale aggiuntivi per i database di sola lettura (descritti più avanti in questo articolo)

##### <a name="always-on-availability-group-cluster-types"></a>Tipi di cluster del gruppo di disponibilità Always On

Il modulo di disponibilità predefinito del clustering in Windows Server è abilitato da una funzionalità nota come clustering di failover. Consente di creare un cluster WSFC da usare con un gruppo di disponibilità o un'istanza FCI. L'integrazione per i gruppi di disponibilità e le istanze FCI è gestita da DLL delle risorse compatibili con i cluster presenti in SQL Server. 

Ogni distribuzione di Linux supportata ha una propria versione della soluzione cluster Pacemaker. SQL Server 2017 in Linux supporta l'uso di Pacemaker. Pacemaker è una soluzione in stack aperta che ogni distribuzione può quindi integrare con il proprio stack. Benché le distribuzioni includano Pacemaker, la soluzione non è integrata come la funzionalità Clustering di failover in Windows Server.

Un cluster di failover di Windows Server e una soluzione Pacemaker sono più simili che differenti. Entrambi consentono di prendere singoli server e combinarli in una configurazione per garantire la disponibilità e si basano su concetti come risorse, vincoli (anche se implementati in modo diverso), failover e così via. Per supportare Pacemaker sia per i gruppi di disponibilità, sia per le configurazioni di istanze FCI, incluso ad esempio il failover automatico, Microsoft offre il pacchetto mssql-server-ha, che è simile, ma non esattamente identico, alle DLL delle risorse in un cluster WSFC, per Pacemaker. Una delle differenze tra un cluster WSFC e Pacemaker è che non esistono risorse nome di rete in Pacemaker, ovvero il componente che consente di astrarre il nome del listener (o il nome dell'istanza FCI) per un cluster WSFC. DNS offre la risoluzione dei nomi in Linux.

A causa della differenza nello stack di cluster, è necessario apportare alcune modifiche per i gruppi di disponibilità, poiché SQL Server deve gestire alcuni dei metadati gestiti in modo nativo da un cluster WSFC. La modifica più [!IMPORTANT] è l'introduzione di un tipo di cluster per un gruppo di disponibilità. È archiviato in sys.availability_groups nelle colonne cluster_type e cluster_type_desc. Esistono tre tipi di cluster:

* WSFC 
* External
* None

Tutti i gruppi di disponibilità che richiedono la disponibilità devono usare un cluster sottostante, che nel caso di SQL Server 2017 significa un cluster WSFC o Pacemaker. Per i gruppi di disponibilità basati su Windows Server che usano un cluster WSFC sottostante, il tipo di cluster predefinito è WSFC e non è necessario impostarlo. Per i gruppi di disponibilità basati su Linux, quando si crea il gruppo di disponibilità, il tipo di cluster deve essere impostato su External. L'integrazione con Pacemaker viene configurata dopo la creazione del gruppo di disponibilità, mentre per un cluster WSFC, si esegue al momento della creazione.

Un tipo di cluster None può essere usato con gruppi di disponibilità sia di Windows Server che di Linux. Impostare il tipo di cluster su None indica che il gruppo di disponibilità non richiede un cluster sottostante. Ciò significa che SQL Server 2017 è la prima versione di SQL Server che supporta i gruppi di disponibilità senza un cluster, ma questo vantaggio è controbilanciato dal fatto che questa configurazione non è supportata come soluzione a disponibilità elevata. 

> [!IMPORTANT] 
> SQL Server 2017 non consente di modificare un tipo di cluster per un gruppo di disponibilità dopo che è stato creato. Non è quindi possibile trasformare un gruppo di disponibilità di tipo None in External o WSFC o viceversa. 

Per gli utenti che vogliono semplicemente aggiungere altre copie di sola lettura di un database o apprezzano le funzionalità offerte dai gruppi di disponibilità per la migrazione o gli aggiornamenti ma non vogliono essere vincolati all'ulteriore complessità di un cluster sottostante o alla replica, un gruppo di disponibilità con un tipo di cluster None è una soluzione ideale. Per altre informazioni, vedere le sezioni [Migrazioni e aggiornamenti](#Migrations) e [Scalabilità in lettura](#ReadScaleOut). 

La schermata riportata di seguito illustra il supporto per i diversi tipi di cluster in SSMS. È necessario che sia in esecuzione la versione 17.1 o successiva. La schermata seguente è tratta dalla versione 17.2.

![Opzioni del gruppo di disponibilità SSMS](media/sql-server-ha-story/image2.png)
 
##### <a name="requiredsynchronizedsecondariestocommit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

SQL Server 2016 ha incrementato il supporto per il numero di repliche sincrone da due a tre in Enterprise Edition. Tuttavia, se una replica secondaria viene sincronizzata ma nell'altra si verifica un problema, non esiste un modo per controllare il comportamento in modo da indicare alla replica primaria di attendere la replica che si comporta in modo errato o consentirle di continuare. Ciò significa che la replica primaria a un certo punto continuerebbe a ricevere traffico in scrittura anche se la replica secondaria non è in uno stato sincronizzato, ovvero si ha una perdita di dati nella replica secondaria.
In SQL Server 2017 ora è disponibile un'opzione in grado di controllare il comportamento dell'azione che si verifica quando sono presenti repliche sincrone denominate REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT. L'opzione funziona come indicato di seguito:
* I tre valori possibili sono: 0, 1 e 2
* Il valore è il numero di repliche secondarie che devono essere sincronizzate, con implicazioni per la perdita di dati, la disponibilità di gruppo di disponibilità e il failover
* Per i cluster WSFC e il tipo di cluster None il valore predefinito è 0 e può essere impostato manualmente su 1 o 2
* Per il tipo di cluster External, per impostazione predefinita, il meccanismo di cluster imposta il valore, che può essere sostituito manualmente. Per tre repliche sincrone, il valore predefinito sarà 1.
In Linux, il valore per REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT è impostato sulla risorsa gruppo di disponibilità nel cluster. In Windows viene impostato con Transact-SQL.

Un valore superiore a 0 garantisce una maggiore protezione dei dati, poiché se il numero di repliche secondarie richiesto non è disponibile, la replica primaria non sarà disponibile finché non viene risolto. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT influisce anche sul comportamento del failover, poiché il failover automatico non può verificarsi se il numero corretto di repliche secondarie non è nello stato appropriato. In Linux il valore 0 non consente il failover automatico, quindi in Linux, quando si usano repliche sincrone con failover automatico, il valore impostato deve essere superiore a 0 per ottenere il failover automatico. 0 in Windows Server è il comportamento di SQL Server 2016 e versioni precedenti.

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>Supporto avanzato per Microsoft Distributed Transaction Coordinator

Prima di SQL Server 2016, distribuire istanze FCI era l'unico modo per ottenere la disponibilità in SQL Server per le applicazioni che richiedono transazioni distribuite che usano automaticamente DTC. Una transazione distribuita può essere eseguita in due modi:
* Una transazione che si estende su più database nella stessa istanza di SQL Server
* Una transazione che si estende su più di un'istanza di SQL Server o può implicare un'origine dati non di SQL Server

SQL Server 2016 ha introdotto un supporto parziale per DTC con i gruppi di disponibilità tipici del secondo scenario. SQL Server 2017 rappresenta un ulteriore passo avanti poiché supporta entrambi gli scenari con DTC.

Un altro miglioramento apportato al supporto DTC per i gruppi di disponibilità consiste nel fatto che in SQL Server 2016 il supporto per DTC può essere abilitato per un gruppo di disponibilità solo quando si crea il gruppo e non si può aggiungere in un secondo momento. In SQL Server 2017 il supporto per DTC può essere aggiunto a un gruppo di disponibilità anche dopo la creazione del gruppo.

>[!NOTE]
> Il supporto per DTC può essere configurato solo per i database in istanze di SQL Server basate su Windows Server. Se DTC è un requisito per l'applicazione, è necessario usare Windows Server come sistema operativo per la distribuzione di SQL Server e non è possibile usare Linux. 

#### <a name="always-on-failover-cluster-instances"></a>Istanze del cluster di failover Always On
Le installazioni in cluster sono una funzionalità di SQL Server a partire dalla versione 6.5. Le istanze FCI sono un metodo efficace per garantire la disponibilità per l'intera installazione di SQL Server, nota come istanza. Ciò significa che tutti gli elementi all'interno dell'istanza, tra cui database, SQL Server Agent - processi, server collegati e così via, verranno spostati in un altro server nel caso in cui si verifichi un problema con il server sottostante. Tutte le istanze FCI richiedono un'archiviazione condivisa, anche se disponibile attraverso la rete. Le risorse dell'istanza FCI possono essere eseguite da, ed essere di proprietà di, un solo nodo alla volta. Nell'immagine seguente il primo nodo del cluster è proprietario dell'istanza FCI, quindi è anche proprietario delle risorse di archiviazione condivise associate, come indica la linea continua tra il nodo e la risorsa di archiviazione.

![Istanza del cluster di failover](media/sql-server-ha-story/image3.png)
 
Dopo un failover la proprietà cambia come illustra l'immagine seguente.

![Dopo il failover](media/sql-server-ha-story/image4.png)
 
La perdita di dati è zero con un'istanza FCI, ma l'archiviazione condivisa sottostante è un singolo punto di errore poiché è presente una sola copia dei dati. Le istanze FCI vengono spesso combinate con un altro metodo di disponibilità, ad esempio un gruppo di disponibilità o il log shipping, per avere copie ridondanti dei database. Il metodo aggiuntivo distribuito deve usare una risorsa di archiviazione fisicamente separata dall'istanza FCI. Quando l'istanza FCI effettua il failover a un altro nodo, si interrompe in un nodo e inizia in un altro, come se si spegnesse e riaccendesse un server. Un'istanza FCI passa attraverso il normale processo di recupero, ovvero viene eseguito il rollforward di tutte le transazioni che lo richiedono e per tutte le transazioni incomplete viene eseguito il rollback. Di conseguenza, il database è coerente da un punto dati al momento dell'errore o del failover manuale, quindi non vi è perdita di dati. I database sono disponibili solo al termine del recupero, quindi il tempo di recupero dipende da molti fattori ed è in genere più lungo del failover effettuato in un gruppo di disponibilità. Lo svantaggio è che quando si esegue il failover in un gruppo di disponibilità, può essere necessario eseguire ulteriori operazioni per poter usare un database, ad esempio abilitare un processo di SQL Server Agent.

Come il gruppo di disponibilità, le istanze FCI estrapolano il nodo del cluster sottostante in cui sono ospitate. Un'istanza FCI mantiene sempre lo stesso nome. Le applicazioni e gli utenti finali non si connettono mai ai nodi e viene usato il nome univoco assegnato all'istanza FCI. Un'istanza FCI può far parte di un gruppo di disponibilità come una delle istanze in cui viene ospitata una replica primaria o secondaria.

Nell'elenco che segue sono evidenziate alcune differenze tra Windows Server e Linux rispetto alle istanze FCI:

* In Windows Server un'istanza FCI è parte del processo di installazione. Un'istanza FCI in Linux viene configurata dopo l'installazione di SQL Server.
* Linux supporta solo una singola installazione di SQL Server per ogni host, in modo che tutte le istanze FCI siano un'istanza predefinita. Windows Server supporta fino a 25 istanze FCI per ogni WSFC.
* Il nome comune usato dalle istanze FCI in Linux è definito in DNS e deve essere lo stesso della risorsa creata per l'istanza FCI.

#### <a name="log-shipping"></a>Log shipping
Se il punto di recupero e gli obiettivi del tempo di recupero sono più flessibili o se i database non sono considerati cruciali, il log shipping è un'altra funzionalità di disponibilità collaudata in SQL Server. In base ai backup nativi di SQL Server, il processo per il log shipping genera automaticamente i backup del log delle transazioni, li copia in una o più istanze, note come warm standby, e applica automaticamente i backup del log delle transazioni a tale standby. Il log shipping usa SQL Server Agent - processi per automatizzare il processo di backup, copia e applicazione dei backup del log delle transazioni.

![Log shipping](media/sql-server-ha-story/image5.png)
 
Senza dubbio il principale vantaggio offerto dal log shipping in alcune capacità è che prende in considerazione l'errore umano. L'applicazione dei log delle transazioni può subire un ritardo. Quindi, se ad esempio qualcuno rilascia un oggetto UPDATE senza una clausola WHERE, lo standby può non contenere la modifica ed è quindi possibile usarlo mentre si ripara il sistema primario. Benché il log shipping sia facile da configurare, il passaggio dall'istanza primaria al warm standby, noto come modifica del ruolo, è sempre manuale. Una modifica del ruolo viene avviata attraverso Transact-SQL e, come per un gruppo di disponibilità, tutti gli oggetti non acquisiti nel log delle transazioni devono essere sincronizzati manualmente. Il log shipping deve inoltre essere configurato per ogni database, mentre un singolo gruppo di disponibilità può contenere più database. A differenza di un gruppo di disponibilità o un'istanza FCI, il log shipping non è in grado di astrarre le modifiche di ruolo. Le applicazioni devono essere in grado di gestire questa situazione. È possibile ricorrere a tecniche come l'alias DNS (CNAME), ma esistono pro e contro, ad esempio il tempo necessario per l'aggiornamento di DNS dopo il passaggio.

## <a name="disaster-recovery"></a>Ripristino di emergenza

Quando la località di disponibilità primaria è interessata da un evento catastrofico come un terremoto o un'inondazione, l'azienda deve essere pronta a portare i propri sistemi online in altre località. Questa sezione spiega in che modo le funzionalità di disponibilità di SQL Server possono contribuire alla continuità delle attività.

### <a name="always-on-availability-groups"></a>Gruppi di disponibilità Always On

Uno dei vantaggi offerti dai gruppi di disponibilità è che sia la disponibilità elevata che il ripristino di emergenza possono essere configurati usando una sola funzionalità. Se non è necessario garantire la disponibilità elevata anche per l'archiviazione condivisa, è molto più semplice avere repliche che sono locali in un data center per la disponibilità elevata e remote in altri data center per il ripristino di emergenza, ognuna con archiviazione separata. Avere copie aggiuntive del database è il compromesso per garantire la ridondanza. Di seguito è riportato un esempio di gruppo di disponibilità che si estende in più data center. Una sola replica primaria è responsabile della sincronizzazione costante di tutte le repliche secondarie.

![Gruppo di disponibilità](media/sql-server-ha-story/image6.png)
 
All'esterno di un gruppo di disponibilità con tipo di cluster None, un gruppo di disponibilità richiede che tutte le repliche siano parte dello stesso cluster sottostante, sia che si tratti di WSFC o Pacemaker. Ciò significa che nell'immagine precedente il cluster WSFC viene esteso per lavorare in due diversi data center e questo accresce la complessità, indipendentemente dalla piattaforma (Windows Server o Linux). L'estensione dei cluster oltre una certa distanza aggiunge complessità. Introdotto in SQL Server 2016, un gruppo di disponibilità distribuito consente a un gruppo di disponibilità di estendersi su gruppi di disponibilità configurati in cluster diversi. In questo modo si disaccoppia il requisito in base al quale tutti i nodi devono far parte dello stesso cluster e si semplifica notevolmente la configurazione del ripristino di emergenza. Per altre informazioni sui gruppi di disponibilità distribuiti, vedere [Gruppi di disponibilità distribuiti](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups).

![Gruppo di disponibilità distribuito](media/sql-server-ha-story/image11.png)
 
### <a name="always-on-failover-cluster-instances"></a>Istanze del cluster di failover Always On

Le istanze FCI possono essere usate per il ripristino di emergenza. Come con un normale gruppo di disponibilità, il meccanismo di cluster sottostante deve essere esteso anche a tutte le posizioni e questo aggiunge complessità. C'è un'altra considerazione da fare per le istanze FCI: l'archiviazione condivisa. Gli stessi dischi devono essere disponibili nei siti primari e secondari, quindi è necessario un metodo esterno, ad esempio una funzionalità offerta dal produttore della risorsa di archiviazione a livello di hardware o l'uso di Replica di archiviazione in Windows Server, per garantire che i dischi utilizzati dall'istanza FCI esistano altrove. 

![FCI Always On](media/sql-server-ha-story/image8.png)
 
### <a name="log-shipping"></a>Log shipping
Il log shipping è uno dei metodi usati da più tempo per il ripristino di emergenza dei database di SQL Server. Il log shipping viene spesso usato in combinazione con i gruppi di disponibilità e le istanze FCI per offrire un ripristino di emergenza semplice ed economico in situazioni che possono essere complesse a causa dell'ambiente, delle competenze amministrative o del budget. Analogamente alla disponibilità elevata per il log shipping, molti ambienti ritardano il caricamento di un log delle transazioni per tenere conto dell'errore umano.

## <a name = "Migrations"></a> Migrazioni e aggiornamenti

Quando in un'azienda si distribuiscono nuove istanze o si aggiornano quelle meno recenti, non si possono tollerare interruzioni prolungate. Questa sezione spiega come usare le funzionalità di disponibilità di SQL Server per ridurre al minimo il tempo di inattività durante processi pianificati come la modifica dell'architettura, il passaggio da un server a un altro, la modifica della piattaforma (ad esempio da Windows Server a Linux o viceversa) o durante l'applicazione di patch.

> [!NOTE]
> Si possono usare anche altri metodi, ad esempio l'uso dei backup e il ripristino degli stessi in altre posizioni, per le migrazioni e gli aggiornamenti. Tali metodi non sono trattati in questo documento. 

### <a name="always-on-availability-groups"></a>Gruppi di disponibilità Always On

Un'istanza esistente che contiene uno o più gruppi di disponibilità può essere aggiornata sul posto a SQL Server 2017. L'operazione richiederà un certo tempo di inattività, che però si può ridurre al minimo con una corretta pianificazione. 

Se l'obiettivo è la migrazione a nuovi server e non la modifica della configurazione (incluso il sistema operativo o la versione di SQL Server), tali server possono essere aggiunti come nodi al cluster sottostante esistente e aggiunti al gruppo di disponibilità. Quando la replica o le repliche sono nello stato corretto, si può eseguire un failover manuale in un nuovo server, quindi i server meno recenti possono essere rimossi dal gruppo di disponibilità e, infine, ritirati. 

I gruppi di disponibilità distribuiti sono anche un altro metodo per eseguire la migrazione a una nuova configurazione o l'aggiornamento di SQL Server. Poiché un gruppo di disponibilità distribuito supporta diversi gruppi di disponibilità sottostanti in architetture diverse, è possibile ad esempio passare da SQL Server 2016 in esecuzione in Windows Server 2012 R2 a SQL Server 2017 in esecuzione in Windows Server 2016. 

![Gruppo di disponibilità distribuito](media/sql-server-ha-story/image10.png)

Infine, i gruppi di disponibilità con un tipo di cluster None possono essere usati anche per la migrazione o l'aggiornamento. Non è possibile combinare e far corrispondere i tipi di cluster in una configurazione tipica di gruppi di disponibilità, quindi tutte le repliche devono essere di tipo None. Un gruppo di disponibilità distribuito può essere usato per estendere gruppi di disponibilità configurati con diversi tipi di cluster. Questo metodo è supportato anche in piattaforme diverse del sistema operativo.

Tutte le varianti dei gruppi di disponibilità per le migrazioni e gli aggiornamenti consentono di eseguire nel tempo la sincronizzazione dei dati, ovvero la parte del lavoro più dispendiosa in termini di tempo. Al momento di avviare il passaggio alla nuova configurazione, il trasferimento comporterà una breve interruzione e non un lungo periodo di inattività in cui devono essere completate tutte le operazioni, inclusa la sincronizzazione dei dati. 

I gruppi di disponibilità possono ridurre i tempi di inattività durante l'applicazione di patch del sistema operativo sottostante eseguendo manualmente il failover dalla replica primaria a una replica secondaria mentre viene completata l'applicazione di patch. Dal punto di vista del sistema operativo, questa procedura è più comune in Windows Server poiché spesso, ma non sempre, la manutenzione del sistema operativo sottostante può richiedere un riavvio. L'applicazione di patch in Linux a volte richiede un riavvio, ma questo avviene raramente. 

[L'applicazione di patch alle istanze di SQL Server che fanno parte di un gruppo di disponibilità](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances) può anche ridurre al minimo i tempi di inattività in base alla complessità dell'architettura del gruppo di disponibilità. Per applicare patch ai server che fanno parte di un gruppo di disponibilità, le patch devono essere applicate prima a una replica secondaria. Applicate le patch al numero corretto di repliche, viene effettuato manualmente il failover della replica primaria in un altro nodo per eseguire l'aggiornamento. A questo punto si possono aggiornare anche tutte le repliche secondarie rimanenti. 

### <a name="always-on-failover-cluster-instances"></a>Istanze del cluster di failover Always On

Le istanze FCI da sole non sono in grado di offrire un supporto per una migrazione o un aggiornamento tradizionale. È necessario configurare un gruppo di disponibilità o log shipping per i database nell'istanza FCI e tutti gli altri oggetti interessati. Tuttavia, le istanze FCI in Windows Server sono ancora un'opzione diffusa per l'applicazione di patch alle istanze di Windows Server sottostanti. Può essere avviato un failover manuale, che consente di interrompere brevemente l'attività anziché rendere l'istanza non disponibile per tutto il tempo richiesto dall'applicazione delle patch a Windows Server.
È possibile aggiornare un'istanza FCI anziché SQL Server 2017. Per informazioni, vedere [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance).

### <a name="log-shipping"></a>Log shipping

Il log shipping è ancora un'opzione molto diffusa per eseguire sia la migrazione che l'aggiornamento dei database. Analogamente ai gruppi di disponibilità, ma questa volta usando il log delle transazioni come metodo di sincronizzazione, la propagazione dei dati può essere avviata molto prima del passaggio da un server all'altro. Al momento del passaggio, dopo che tutto il traffico è stato interrotto in corrispondenza dell'origine, è necessario estrarre, copiare e applicare un log delle transazioni finale alla nuova configurazione. A questo punto, il database può essere portato online. Il log shipping in genere è più tollerante rispetto alle reti più lente e, anche se il passaggio può avere una durata leggermente maggiore rispetto al passaggio eseguito usando un gruppo di disponibilità o un gruppo di disponibilità distribuito, normalmente viene misurato in minuti, non in ore, giorni o settimane.

Analogamente ai gruppi di disponibilità, il log shipping offre la possibilità di passare a un altro server in caso di applicazione di patch.

### <a name="other-sql-server-deployment-methods-and-availability"></a>Altri metodi di distribuzione di SQL Server e disponibilità

Esistono altri due metodi di distribuzione per SQL Server in Linux: contenitori e uso di Azure (o un altro provider di cloud pubblico). L'esigenza generale di disponibilità presentata in questo documento esiste indipendentemente dalla modalità di distribuzione di SQL Server. Questi due metodi richiedono alcune considerazioni speciali per quanto riguarda la disponibilità elevata di SQL Server.

I [contenitori con Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker) rappresentano una nuova modalità di distribuzione di SQL Server, per Windows Server o Linux. Un contenitore è un'immagine completa di SQL Server pronta per l'esecuzione. Tuttavia, attualmente non esiste un supporto nativo per il clustering, quindi nemmeno per la disponibilità elevata diretta o il ripristino di emergenza. Al momento le opzioni che consentono di rendere disponibili i database di SQL Server usando i contenitori sono log shipping e backup e ripristino. Benché si possa configurare un gruppo di disponibilità con tipo di cluster None, come indicato in precedenza, questa soluzione non è una reale configurazione di disponibilità. Microsoft è alla ricerca di soluzioni per abilitare i gruppi di disponibilità o le istanze FCI usando i contenitori. 

Se si stanno usando i contenitori e si perde un contenitore, in base alla piattaforma del contenitore, è possibile distribuirlo di nuovo e associarlo all'archiviazione condivisa usata. Parte di questo meccanismo viene messa a disposizione dall'agente di orchestrazione del contenitore. Benché si produca una certa resilienza, si avrà un periodo di inattività associato al recupero del database e la disponibilità non è realmente elevata come sarebbe usando un gruppo di disponibilità o un'istanza FCI. 

Le macchine virtuali IaaS Linux possono essere distribuite con SQL Server installato con Azure. Analogamente alle installazioni locali, un'installazione supportata richiede l'uso di STONITH (Shoot the Other Node in the Head), che è esterno a Pacemaker. STONITH è disponibile attraverso agenti di fencing della disponibilità. Alcune distribuzioni li includono come parte della piattaforma, altri si affidano a fornitori esterni di hardware e software. Controllare la distribuzione di Linux preferita per vedere quali moduli di STONITH sono disponibili in modo da poter distribuire una soluzione supportata nel cloud pubblico.

## <a name="cross-platform-and-linux-distribution-interoperability"></a>Interoperabilità della distribuzione Linux e multipiattaforma

Con SQL Server supportato sia in Windows Server che in Linux, questa sezione illustra gli scenari in cui le piattaforme possono essere usate insieme ai fini della disponibilità e per altri scopi, nonché la situazione in cui le soluzioni incorporano più di una distribuzione Linux.

Prima di analizzare gli scenari multipiattaforma e di interoperabilità, è necessario indicare due aspetti:

* Non esistono scenari in cui un'istanza FCI o un gruppo di disponibilità basati su WSFC funzionano direttamente con un'istanza FCI o un gruppo di disponibilità basati su Linux. Un cluster WSFC non può essere esteso da un nodo Pacemaker e viceversa. 
* La combinazione delle distribuzioni Linux non è supportata con le istanze FCI o un gruppo di disponibilità con tipo di cluster External. Tutte le repliche del gruppo di disponibilità in tale scenario devono essere configurate non solo per la stessa distribuzione Linux, ma anche per la stessa versione. Le due modalità che consentono il funzionamento di SQL Server tra le due piattaforme o più distribuzioni di Linux sono i gruppi di disponibilità e il log shipping.

## <a name="distributed-availability-groups"></a>Gruppi di disponibilità distribuiti 

I gruppi di disponibilità distribuiti sono progettati in modo da estendere le configurazioni con gruppi di disponibilità e i due cluster sottostanti ai gruppi di disponibilità possono essere due cluster WSFC, o distribuzioni Linux, diversi o essere uno in un cluster WSFC e l'altro in Linux. Un gruppo di disponibilità distribuito sarà il metodo principale per ottenere una soluzione multipiattaforma. Un gruppo di disponibilità distribuito è anche la soluzione principale per le migrazioni, ad esempio la conversione di un'infrastruttura SQL Server basata su Windows Server in un'infrastruttura basata su Linux, se questo è l'obiettivo dell'azienda. Come indicato in precedenza, i gruppi di disponibilità, e in particolare i gruppi di disponibilità distribuiti, consentono di ridurre il periodo di tempo in cui un'applicazione non è disponibile per l'uso. Un esempio di gruppo di disponibilità distribuito che si estende in un cluster WSFC e Pacemaker è illustrato di seguito.

![Gruppo di disponibilità distribuito](media/sql-server-ha-story/image9.png)
 
Se un gruppo di disponibilità è configurato con un tipo di cluster None, è in grado di estendere Windows Server e Linux, nonché più distribuzioni Linux. Poiché non si tratta di una configurazione con disponibilità elevata reale, non deve essere usata per le distribuzioni cruciali, ma per gli scenari di scalabilità in lettura o di migrazione/aggiornamento.

## <a name="log-shipping"></a>Log shipping

Poiché il log shipping si basa essenzialmente su backup e ripristino, non esistono differenze nei database, nelle strutture di file e così via tra SQL Server in Windows Server e SQL Server in Linux. Ciò significa che è possibile configurare il log shipping tra un'installazione di SQL Server basata su Windows Server e una di Linux nonché tra le distribuzioni Linux. Tutti gli altri elementi rimangono invariati. L'unico problema è che il log shipping, proprio come un gruppo di disponibilità, non funziona se la versione principale di SQL Server dell'origine è successiva alla versione di SQL Server della destinazione. 

## <a name = "ReadScaleOut"></a>Scalabilità in lettura

Da quando sono state introdotte in SQL Server 2012, le repliche secondarie possono essere usate per le query di sola lettura. L'operazione può essere eseguita in due modi con un gruppo di disponibilità: consentendo l'accesso diretto alla replica secondaria e [configurando il routing di sola lettura](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server), che richiede l'uso del listener.  SQL Server 2016 ha introdotto la possibilità di bilanciare il carico delle connessioni di sola lettura attraverso il listener usando un algoritmo round robin, che consente la diffusione delle richieste di sola lettura in tutte le repliche leggibili. 

> [!NOTE]
> Le repliche secondarie leggibili sono una funzionalità presente solo in Enterprise Edition e ogni istanza che ospita una replica leggibile deve avere una licenza di SQL Server.

Il ridimensionamento delle copie leggibili di un database usando i gruppi di disponibilità è stato introdotto con i gruppi di disponibilità distribuiti in SQL Server 2016. Questo consente alle aziende di avere copie di sola lettura del database non solo a livello locale, ma anche a livello regionale e globale con esigenze minime in termini di configurazione e di ridurre il traffico di rete e la latenza grazie all'esecuzione locale delle query. Ogni replica primaria di un gruppo di disponibilità può inizializzare altri due gruppi di disponibilità anche se non è la copia con funzioni di lettura/scrittura complete, quindi ogni gruppo di disponibilità distribuito può supportare fino a 27 copie dei dati leggibili. 

![Gruppo di disponibilità distribuito](media/sql-server-ha-story/image11.png)

A partire da SQL Server 2017, è possibile creare una soluzione di sola lettura near real time con i gruppi di disponibilità configurati con un cluster di tipo None. Se l'obiettivo è usare i gruppi di disponibilità per le repliche secondarie leggibili e non per la disponibilità, questa operazione elimina la complessità dell'uso di un cluster WSFC o Pacemaker e offre i vantaggi in termini di leggibilità di un gruppo di disponibilità in un metodo di distribuzione più semplice. 

L'unico problema di una certa entità è che non essendo presente un cluster sottostante con tipo di cluster None, la configurazione del routing di sola lettura è un po' diversa. Dalla prospettiva di SQL Server, è comunque necessario un listener per il routing delle richieste anche se non è presente un cluster. Anziché configurare un listener tradizionale, viene usato l'indirizzo IP o il nome della replica primaria. La replica primaria viene quindi usata per il routing delle richieste di sola lettura.

Un warm standby del log shipping può essere tecnicamente configurato per l'uso dei dati leggibili ripristinando il database con STANDBY. Tuttavia, poiché i log delle transazioni richiedono l'uso esclusivo del database per il ripristino, che gli utenti non possono accedere al database durante tale attività. Per questo motivo il log shipping non è affatto la soluzione ideale, soprattutto se sono richiesti dati near real time. 

Un aspetto da considerare per tutti gli scenari di scalabilità in lettura con gruppi di disponibilità è che, a differenza della replica transazionale in cui tutti i dati sono live, ogni replica secondaria non è in uno stato in cui è possibile applicare indici univoci e la replica è una copia esatta di quella primaria. Ciò significa che se gli indici sono necessari per la creazione di report o i dati devono essere modificati, l'operazione deve essere eseguita nei database della replica primaria. Se è necessaria questa flessibilità, la replica è una soluzione migliore per i dati leggibili.

## <a name="summary"></a>Riepilogo

Le istanze e i database di SQL Server 2017 possono essere resi altamente disponibili usando le stesse funzionalità sia in Windows Server che in Linux. Oltre ai normali scenari di disponibilità per disponibilità elevata e ripristino di emergenza a livello locale, è possibile ridurre i tempi di inattività associati gli aggiornamenti e alle migrazioni con le funzionalità di disponibilità di SQL Server. I gruppi di disponibilità consentono inoltre di avere a disposizione copie aggiuntive di un database come parte della stessa architettura per scalare orizzontalmente le copie leggibili. Se si distribuisce una nuova soluzione usando SQL Server 2017 o si prevede di eseguire un aggiornamento, SQL Server 2017 offre la disponibilità e l'affidabilità necessarie.
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png
