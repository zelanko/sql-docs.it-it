---
title: Architettura e gestione del log delle transazioni SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 4d1a4f97-3fe4-44af-9d4f-f884a6eaa457
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3e1063f41afce526afcde90c61950e9234ae7517
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000541"
---
# <a name="sql-server-transaction-log-architecture-and-management"></a>Architettura e gestione del log delle transazioni di SQL Server

[!INCLUDE[appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In ogni database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è incluso un log delle transazioni in cui vengono registrate tutte le transazioni e le modifiche apportate dalle transazioni stesse al database. Il log delle transazioni è un componente fondamentale del database e, in caso di errore di sistema, può essere necessario per ripristinare la coerenza del database. In questa guida vengono fornite informazioni sull'architettura fisica e logica del log delle transazioni. Le informazioni sull'architettura consentono di gestire più efficacemente i log delle transazioni.  

  
##  <a name="transaction-log-logical-architecture"></a><a name="Logical_Arch"></a>Architettura logica del log delle transazioni  

 Il log delle transazioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] funziona in modo logico come se si trattasse di una stringa di record di log. Ogni record di log è identificato da un numero di sequenza del file di log (LSN). Ogni nuovo record di log viene scritto nell'estremità finale logica del log con un LSN maggiore di quello del record precedente. I record di log vengono archiviati in sequenza man mano che vengono creati. Ogni record di log contiene l'ID della transazione a cui appartiene. Tutti i record di log associati a ogni transazione sono collegati singolarmente in una catena tramite puntatori ai record precedenti che consentono di eseguire più rapidamente il rollback della transazione.  
  
 Nei record di log relativi alle modifiche dei dati vengono registrate le operazioni logiche eseguite oppure immagini dei dati precedenti e successive alla modifica. Un'immagine precedente la modifica è una copia dei dati eseguita prima dell'operazione, mentre un'immagine successiva alla modifica è una copia dei dati eseguita dopo l'operazione.  
  
 La procedura necessaria per recuperare un'operazione varia a seconda del tipo di record di log:  
  
-   Operazione logica registrata  
  
    -   Per eseguire il rollforward dell'operazione logica, questa viene eseguita nuovamente.  
  
    -   Per eseguire il rollback dell'operazione logica, questa viene eseguita al contrario.  
  
-   Immagine precedente e successiva (alla modifica dei dati) registrata  
  
    -   Per eseguire il rollforward dell'operazione, viene applicata l'immagine successiva.  
  
    -   Per eseguire il rollback dell'operazione, viene applicata l'immagine precedente.  
  
 Nel log delle transazioni vengono registrati molti tipi di operazioni, tra cui:  
  
-   L'inizio e la fine di ogni transazione.  
  
-   Tutte le modifiche apportate ai dati, ovvero inserimento, aggiornamento o eliminazione, comprese le modifiche apportate da stored procedure di sistema o istruzioni DDL (Data Definition Language) a qualsiasi tabella, incluse le tabelle di sistema.  
  
-   Tutte le allocazioni o deallocazioni di pagina e di extent.  
  
-   Operazioni di creazione o eliminazione di una tabella o di un indice.  
  
 Nel log vengono registrate anche le operazioni di rollback. Ogni transazione riserva una determinata quantità di spazio nel log delle transazioni per garantire che nel log sia disponibile spazio sufficiente per supportare un rollback causato da un'istruzione di rollback esplicita o dal verificarsi di un errore. La quantità di spazio riservata varia in base alle operazioni eseguite nella transazione, ma in genere equivale alla quantità di spazio utilizzata per registrare nel log ogni operazione. Lo spazio riservato viene liberato al completamento della transazione.  
  
  La sezione del file di log dal primo record di log che deve essere presente per la corretta esecuzione del rollback a livello di database all'ultimo record di log scritto è definita parte attiva del log o *log attivo*. Questa sezione del log è necessaria per il recupero completo del database. Non è possibile troncare nessuna parte del log attivo. Il numero di sequenza del file di log (LSN) di questo primo record di log è noto come LSN minimo del recupero (*MinLSN*).  
  
##  <a name="transaction-log-physical-architecture"></a><a name="physical_arch"></a> Architettura fisica del log delle transazioni  

 Del log delle transazioni di un database viene eseguito il mapping su uno o più file fisici. Concettualmente, il file di log è una stringa di record di log. Fisicamente, la sequenza di record di log viene archiviata in modo efficiente nel set di file fisici che implementano il log delle transazioni. È necessario che sia disponibile almeno un file di log per ogni database.  
  
 In [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] ogni file di log fisico viene diviso internamente in diversi file di log virtuali. I file di log virtuali non hanno dimensioni fisse e non è previsto un numero fisso di file di log virtuali per un file di log fisico. Il [!INCLUDE[ssDE](../includes/ssde-md.md)] definisce dinamicamente le dimensioni dei file di log virtuali durante la creazione o l'estensione. Il [!INCLUDE[ssDE](../includes/ssde-md.md)] tende a mantenere ridotto il numero di file virtuali. Le dimensioni dei file virtuali dopo l'estensione di un file di log corrispondono alla somma delle dimensioni del log esistente e del nuovo incremento del file. Le dimensioni o il numero di file di log virtuali non possono essere configurati o impostati dagli amministratori.  
  
 I file di log virtuali influenzano le prestazioni del sistema solo se i file di log fisici sono definiti da valori bassi di *size* e *growth_increment* . Il valore *size* indica le dimensioni iniziali del file di log mentre il valore *growth_increment* indica la quantità di spazio aggiunta al file ogni volta che è necessario dello spazio nuovo. Se le dimensioni dei file di log aumentano in modo considerevole in seguito a una serie di piccoli incrementi, in essi verrà incluso un numero elevato di file di log virtuali. Questo potrebbe provocare un rallentamento delle operazioni di avvio del database e di backup e ripristino del log. È consigliabile assegnare ai file di log un valore *size* simile a quello delle dimensioni finali necessarie e un valore *growth_increment* relativamente alto. Per altre informazioni su questi parametri, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
 Il log delle transazioni è un file circolare. Si consideri, ad esempio, un database con un file di log fisico diviso in quattro file di log virtuali. Quando viene creato il database, il file di log logico comincia all'inizio del file di log fisico. Vengono aggiunti nuovi record di log alla fine del log logico, che si espandono verso la fine del log fisico. Il troncamento del log libera tutti i log virtuali i cui record vengono visualizzati tutti davanti al numero minimo di sequenza del file di log (MinLSN, Minimum Log Sequence Number) per il recupero. *MinLSN* è il numero di sequenza del file di log del record di log meno recente necessario per un corretto rollback a livello di database. Il log delle transazioni del database di esempio sarebbe simile a quello illustrato nella figura seguente.  
  
 ![File di log diviso in quattro file di log virtuali](media/tranlog3.gif "File di log diviso in quattro file di log virtuali")  
  
 Quando la fine del log logico raggiunge la fine del file di log fisico, i nuovi record di log vengono nuovamente inseriti a partire dall'inizio del file di log fisico.  
  
 ![I record del log vengono riportati all'inizio del file di log](media/tranlog4.gif "I record del log vengono riportati all'inizio del file di log")  
  
 Questo ciclo viene ripetuto all'infinito, a condizione che la fine del log logico non raggiunga mai l'inizio del log stesso. Se i vecchi record di log vengono troncati abbastanza frequentemente in modo da lasciare sempre spazio sufficiente per i nuovi record di log creati fino al checkpoint successivo, il log non viene mai riempito completamente. Se, tuttavia, la fine del log logico raggiunge l'inizio del log stesso, può verificarsi uno dei due eventi indicati di seguito:  
  
-   Se è abilitata l'impostazione FILEGROWTH per il log e sul disco vi è spazio disponibile, il file viene esteso in base al valore specificato nel parametro *growth_increment* e i nuovi record di log vengono aggiunti all'estensione. Per altre informazioni sull'impostazione FILEGROWTH, vedere [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
-   Se l'impostazione FILEGROWTH non è attiva oppure se lo spazio libero sul disco in cui risiede il file di log è inferiore a quello specificato in *growth_increment*, viene generato un errore 9002.  
  
 Se il log include più file di log fisici, il log logico utilizzerà tutti i file di log fisici prima di tornare all'inizio del primo file di log fisico.  
  
### <a name="log-truncation"></a>Troncamento del log  

 Il troncamento del log è essenziale per evitare il riempimento del log. Il troncamento del log comporta l'eliminazione dei file di log virtuali inattivi dal log delle transazioni logico di un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , liberando spazio nel log logico per il riutilizzo da parte del log delle transazioni fisico. Se un log delle transazioni non viene mai troncato, è possibile che le sue dimensioni aumentino fino a occupare tutto lo spazio su disco allocato ai file di log fisici. Tuttavia, prima che sia possibile troncare il log, è necessario eseguire un'operazione su checkpoint. Tramite un checkpoint vengono scritte le pagine modificate in memoria correnti, note come pagine dirty, e le informazioni sul log delle transazioni dalla memoria sul disco. Quando viene eseguito il checkpoint, la parte inattiva del log delle transazioni viene contrassegnata come riutilizzabile. Successivamente, tale parte inattiva potrà essere liberata mediante il troncamento del log. Per altre informazioni sui checkpoint, vedere [Checkpoint di database &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 Nelle figure seguenti viene illustrato un log delle transazioni prima e dopo il troncamento. Nella prima figura viene illustrato un log delle transazioni che non è mai stato troncato. Attualmente, il log logico utilizza quattro file di log virtuali. Il log logico inizia prima del primo file di log virtuale e termina al log virtuale 4. Il record MinLSN si trova nel log virtuale 3. I log virtuali 1 e 2 contengono solo record di log inattivi. Questi record possono essere troncati. Il log virtuale 5 è ancora inutilizzato e non fa parte del log logico corrente.  
  
 ![Log delle transazioni con quattro log virtuali](media/tranlog2.gif "Log delle transazioni con quattro log virtuali")  
  
 Nella seconda figura è illustrata la struttura del log dopo il troncamento. I log virtuali 1 e 2 sono stati liberati per il riutilizzo. Il log logico ora inizia all'inizio del log virtuale 3. Il log virtuale 5 è ancora inutilizzato e non fa parte del log logico corrente.  
  
 ![File di log diviso in quattro file di log virtuali](media/tranlog3.gif "File di log diviso in quattro file di log virtuali")  
  
 A meno che non venga posticipato per qualche motivo, il troncamento del log viene effettuato automaticamente dopo gli eventi seguenti:  
  
-   Nel modello di recupero con registrazione minima, dopo un checkpoint.  
  
-   Nel modello di recupero con registrazione completa o modello di recupero con registrazione minima delle operazioni bulk, dopo un backup del log se dal backup precedente si è verificato un checkpoint.  
  
 Il troncamento del log può essere posticipato da diversi fattori. Se si verifica un ritardo elevato nel troncamento del log, lo spazio del log delle transazioni può esaurirsi. Per informazioni, vedere [fattori che possono ritardare il troncamento del log](../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation) e [risolvere i problemi relativi a un log delle transazioni completo &#40;SQL Server errore 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
##  <a name="write-ahead-transaction-log"></a><a name="WAL"></a>Log delle transazioni write-ahead  

 In questa sezione viene descritto il ruolo del log delle transazioni write-ahead nella registrazione delle modifiche dei dati sul disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa un log write-ahead (WAL) che garantisce che le modifiche apportate ai dati non vengano scritte nel disco prima del record di log corrispondente. In questo modo, è possibile mantenere le proprietà ACID per una transazione.  
  
 Per comprendere il funzionamento dei log write-ahead, è importante conoscere la modalità con cui i dati modificati vengono scritti sul disco. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mantiene una cache buffer in cui vengono lette le pagine di dati quando questi ultimi devono essere recuperati. Quando una pagina viene modificata nella cache buffer, non viene immediatamente riscritta nel disco, ma viene contrassegnata come *dirty*. A una pagina di dati possono essere associate più scritture logiche prima di essere scritta fisicamente sul disco. Per ogni scrittura logica, viene inserito un record del log delle transazioni nella cache del log, per registrare la modifica. I record di log devono essere scritti sul disco prima che la pagina dirty associata venga rimossa dalla cache buffer e scritta sul disco. Tramite il processo di gestione dei checkpoint viene eseguita periodicamente l'analisi della cache buffer alla ricerca di buffer con pagine di un database specifico e tutte le pagine dirty vengono scritte nel disco. I checkpoint consentono di risparmiare tempo durante un successivo recupero, grazie alla creazione di un punto in cui è certo che tutte le pagine dirty siano state scritte sul disco.  
  
 La scrittura di una pagina di dati modificata dalla cache buffer al disco viene definita scaricamento della pagina. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dispone della logica tramite cui viene impedito lo scaricamento di una pagina dirty prima della scrittura del record di log associato. I record di log vengono scritti su disco dopo che è stato eseguito il commit delle transazioni.  
  
##  <a name="transaction-log-backups"></a><a name="Backups"></a>Backup del log delle transazioni  

 In questa sezione vengono introdotti concetti relativi al backup e al ripristino, vale a dire all'applicazione, di log delle transazioni. In base ai modelli di recupero con registrazione completa e con registrazione minima delle operazioni bulk, per poter recuperare i dati è necessario eseguire backup di routine dei log delle transazioni (*backup del log*). È possibile eseguire il backup del log mentre è in esecuzione un qualsiasi backup completo. Per altre informazioni sui modelli di recupero, vedere [Backup e ripristino di database SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Prima di creare il primo backup del log, è necessario creare un backup completo, ad esempio un backup del database oppure il primo di un set di backup di file. Il ripristino di un database solo tramite backup di file può essere un'operazione complessa. Quando possibile, è pertanto consigliabile iniziare con un backup completo del database. Eseguire quindi regolarmente il backup del log delle transazioni. In questo modo, è possibile non solo limitare al minimo il rischio di perdita dei dati, ma anche abilitare il troncamento del log delle transazioni. In genere, il troncamento del log delle transazioni viene eseguito dopo ogni backup del log convenzionale,  
  
 È consigliabile eseguire backup del log sufficientemente frequenti da soddisfare i requisiti aziendali e, in particolare, il requisito inerente la tolleranza per eventuali perdite di dati, che potrebbero ad esempio verificarsi in seguito al danneggiamento dell'unità dei log. La frequenza appropriata per l'esecuzione dei backup del log viene determinata in base al raggiungimento di un compromesso tra la tolleranza per il rischio di perdita dei dati e la quantità di backup del log che è possibile archiviare, gestire e potenzialmente ripristinare. Potrebbe essere sufficiente eseguire un backup del log ogni 15 - 30 minuti. Se nella propria azienda è necessario limitare al minimo il rischio di perdita dei dati, valutare se eseguire i backup del log con una maggiore frequenza. L'esecuzione di backup del log più frequenti offre il vantaggio aggiuntivo di un aumento della frequenza del troncamento del log, con una conseguente riduzione delle dimensioni dei file di log.  
  
 Per limitare il numero di backup dei log che è necessario ripristinare, è fondamentale eseguire regolarmente il backup dei dati. Ad esempio, è possibile pianificare un backup completo del database una volta la settima e backup differenziali del database una volta al giorno.  
  
### <a name="the-log-chain"></a>Catena di log  

 Una sequenza continua di backup del log è denominata *catena di log*. Una catena di log ha inizio con un backup completo del database. In genere, una nuova catena di log viene creata solo quando si esegue il backup del database per la prima volta oppure dopo il passaggio dal modello di recupero con registrazione minima al modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk. Se si sceglie di non sovrascrivere i set di backup esistenti durante la creazione di un backup completo del database, la catena di log esistente rimane intatta. Con la catena di log intatta, è possibile ripristinare il database da qualsiasi backup completo del database nel set di supporti, seguito da tutti i backup del log successivi tramite il punto di recupero specifico. Il punto di recupero può essere la fine dell'ultimo backup del log o un punto di recupero specifico in uno dei backup del log. Per altre informazioni, vedere [Backup di log delle transazioni &#40;SQL Server&#41;](../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Per ripristinare un database al punto in cui si è verificato l'errore, è necessario che la catena di log sia intatta. In altre parole, è necessario che una sequenza non interrotta di backup del log delle transazioni si estenda fino al punto di errore. Il punto in cui la sequenza del log deve iniziare dipende dal tipo di backup dei dati che si sta ripristinando, ovvero un backup del database, parziale o di file. Nel caso di un backup del database o parziale, la sequenza di backup del log si deve estendere dalla fine di un backup del database o parziale. Nel caso di un set di backup di file, la sequenza di backup del log si deve estendere dall'inizio di un intero set di backup di file. Per altre informazioni, vedere [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
### <a name="restore-log-backups"></a>Ripristinare i backup di log  

 Il ripristino di un backup del log determina il rollforward delle modifiche registrate nel log delle transazioni in modo da ricreare l'esatto stato del database esistente all'inizio dell'operazione di backup del log. Quando si ripristina un database, è necessario ripristinare i backup del log creati dopo il backup completo del database ripristinato oppure dall'inizio del primo backup di file ripristinato. In genere, dopo il ripristino del backup dei dati o del backup differenziale più recente, è necessario ripristinare una serie di backup del log fino al punto di recupero desiderato. Recuperare quindi il database. Verrà eseguito il rollback di tutte le transazioni incomplete nel momento in cui è iniziato il recupero e verrà attivata la modalità online per il database. Dopo il recupero del database, non è possibile ripristinare altri backup. Per altre informazioni, vedere [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
## <a name="additional-reading"></a>Altre letture  

 Per ulteriori informazioni sul log delle transazioni, vedere gli articoli e i documenti riportati di seguito.  
  
 [Informazioni sulla registrazione e il recupero in SQL Server di Paul Randall](https://technet.microsoft.com/magazine/2009.02.logging.aspx)  
  
 [Gestione del log delle transazioni di SQL Server di Tony Davis e Gail Shaw](http://www.simple-talk.com/books/sql-books/sql-server-transaction-log-management-by-tony-davis-and-gail-shaw/)  
  
  
