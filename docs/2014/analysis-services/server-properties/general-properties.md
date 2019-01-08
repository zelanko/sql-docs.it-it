---
title: Proprietà generali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b854692aa00d953ebd8de783104869b784115277
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369143"
---
# <a name="general-properties"></a>Proprietà generali
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà del server elencate nelle tabelle seguenti. In questo argomento vengono documentate le proprietà del server disponibili nel file msmdsrv.ini che non sono incluse in una sezione specifica, ad esempio Sicurezza, Rete o Pool di thread. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Si applica a:** Modalità server multidimensionale e tabulare, se non diversamente specificato  
  
## <a name="non-specific-category"></a>Categoria Non-Specific  
 `AdminTimeout`  
 Proprietà Integer a 32 bit con segno che definisce il timeout per l'amministratore in secondi. Si tratta di una proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Il valore predefinito di questa proprietà è zero (0), corrispondente all'assenza di un timeout.  
  
 `AllowedBrowsingFolders`  
 Proprietà stringa che specifica in un elenco delimitato le cartelle che è possibile esplorare durante il salvataggio, l'apertura e la ricerca di file nelle finestra di dialogo di Analysis Services. È necessario che l'account del servizio Analysis Services abbia letto e scritto le autorizzazioni a qualsiasi cartella aggiunta all'elenco.  
  
 `BackupDir`  
 Proprietà stringa che identifica il nome della directory in cui sono archiviati i file di backup per impostazione predefinita, nel caso in cui un percorso non è specificato come parte del comando Backup.  
  
 `CollationName`  
 Proprietà di stringa che identifica le regole di confronto del server. Per altre informazioni, vedere [Lingue e regole di confronto &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md).  
  
 `CommitTimeout`  
 Proprietà Integer che specifica per quanto tempo (in millisecondi) il server attenderà prima di acquisire un blocco in scrittura allo scopo di eseguire il commit di una transazione. Un periodo di attesa è spesso necessario perché il server deve attendere che eventuali altri blocchi vengano rilasciati prima di acquisire un blocco in scrittura per il commit della transazione.  
  
 Il valore predefinito di questa proprietà è zero (0). Ciò significa che il server attenderà per un periodo di tempo indefinito. Per altre informazioni sulle proprietà correlate al blocco, vedere [SQL Server 2008 R2 Analysis Services Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539)(Guida operativa di SQL Server 2008 R2 Analysis Services).  
  
 `CoordinatorBuildMaxThreads`  
 Proprietà Integer a 32 bit con segno che definisce il numero massimo di thread allocati alla compilazione di indici di partizioni. Per rendere più veloce l'indicizzazione delle partizioni a scapito della quantità di memoria utilizzata, è necessario aumentare il valore di questa proprietà. Per altre informazioni su questa proprietà, vedere [SQL Server 2008 R2 Analysis Services Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539)(Guida operativa di SQL Server 2008 R2 Analysis Services).  
  
 `CoordinatorCancelCount`  
 Proprietà Integer a 32 bit con segno che definisce la frequenza con la quale il server controlla se si è verificato un evento di annullamento (basato su un conteggio di iterazione interno). Per aumentare la frequenza di controllo degli eventi di annullamento, a scapito delle prestazioni generali, è necessario diminuire il valore di questa proprietà.  
  
 `CoordinatorCancelCount` in modalità server tabulare viene ignorato.  
  
 `CoordinatorExecutionMode`  
 Proprietà Integer a 32 bit con segno che definisce il numero massimo di operazioni parallele accettate dal server, comprese operazioni di elaborazione e query. Zero (0) indica che il numero delle operazioni verrà deciso dal server in base a un algoritmo interno. Un numero positivo indica il numero massimo totale delle operazioni. Un numero negativo indica il numero massimo di operazioni per processore.  
  
 `CoordinatorExecutionMode` in modalità server tabulare viene ignorato.  
  
 Il valore predefinito di questa proprietà è -4. Ciò significa che il funzionamento del server è limitato a 4 operazioni parallele per processore. Per altre informazioni su questa proprietà, vedere [SQL Server 2008 R2 Analysis Services Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539)(Guida operativa di SQL Server 2008 R2 Analysis Services).  
  
 `CoordinatorQueryMaxThreads`  
 Proprietà Integer a 32 bit con segno che definisce il numero massimo di thread per segmento di partizione durante la risoluzione delle query. Minore è il numero di utenti concorrenti e maggiore è il valore assegnabile a questa proprietà, a scapito della memoria. Viceversa, se il numero di utenti concorrente è elevato, è necessario abbassare il valore di questa proprietà.  
  
 `CoordinatorShutdownMode`  
 Proprietà booleana che definisce la modalità di arresto del coordinatore. Si tratta di una proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataDir`  
 Proprietà di stringa che consente l'identificazione del nome della directory in cui sono archiviati i dati.  
  
 `DeploymentMode`  
 Consente di determinare il contesto operativo di un'istanza del server Analysis Services. Questa proprietà è definita 'modalità server' in finestre di dialogo, messaggi e documentazione. Questa proprietà viene configurata tramite il programma di installazione di SQL Server in base alla modalità server selezionata durante l'installazione di Analysis Services e deve essere considerata solo per uso interno, usando sempre il valore specificato dal programma di installazione.  
  
 Tra i valori validi per questa proprietà sono inclusi i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Rappresenta il valore predefinito. Specifica la modalità multidimensionale, usata per i database multidimensionali che usano l'archiviazione MOLAP, HOLAP e ROLAP, nonché i modelli di data mining.|  
|1|Consente di specificare le istanze di Analysis Services installate come parte di una distribuzione di PowerPivot per SharePoint. Non modificare la proprietà della modalità di distribuzione dell'istanza di Analysis Services che è parte di un'installazione di PowerPivot per SharePoint. I dati PowerPivot non verranno più eseguiti nel server se si cambia modalità.|  
|2|Specifica la modalità tabulare usata per l'hosting dei database del modello tabulare che usano l'archiviazione in memoria o DirectQuery.|  
  
 Ogni modalità comporta l'esclusione dell'altra. In un server configurato per la modalità tabulare non è possibile eseguire i database di Analysis Services che contengono cubi e dimensioni. Se l'hardware del computer sottostante può supportare tale condizione, è possibile installare più istanze di Analysis Services nello stesso computer e configurare ogni istanza per l'utilizzo di una modalità di distribuzione diversa. Analysis Services è un'applicazione a elevato utilizzo di risorse. La distribuzione di più istanze sullo stesso sistema viene consigliata solo per server di fascia alta.  
  
 `EnableFast1033Locale`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `ExternalCommandTimeout`  
 Proprietà Integer che definisce il timeout in secondi per i comandi inviati a server esterni, incluse le origini dati relazionali e i server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esterni.  
  
 Il valore predefinito di questa proprietà è 3600 (secondi).  
  
 `ExternalConnectionTimeout`  
 Proprietà Integer che definisce il timeout in secondi per la creazione di connessioni a server esterni, incluse le origini dati relazionali e i server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esterni. Questa proprietà viene ignorata se nella stringa di connessione è specificato un timeout di connessione.  
  
 Il valore predefinito di questa proprietà è 60 (secondi).  
  
 `ForceCommitTimeout`  
 Proprietà Integer che specifica quanto tempo (millisecondi) deve trascorrere prima che un commit annulli altri comandi che precedono quello corrente, incluse le query in corso. In questo modo la transazione di commit procederà annullando le operazioni a priorità più bassa, ad esempio le query.  
  
 Il valore predefinito di questa proprietà è 30 secondi (30000 millisecondi). Ciò significa che non verrà imposto un timeout agli altri comandi finché la transazione di commit non aspetta 30 secondi.  
  
> [!NOTE]  
>  Le query e i processi annullati da questo evento restituiranno il seguente messaggio di errore: "`Server: The operation has been cancelled`"  
  
 Per altre informazioni su questa proprietà, vedere [SQL Server 2008 R2 Analysis Services Operations Guide](https://go.microsoft.com/fwlink/?LinkID=225539)(Guida operativa di SQL Server 2008 R2 Analysis Services).  
  
> [!IMPORTANT]  
>  `ForceCommitTimeout` si applica ai comandi di elaborazione dei cubi e alle operazioni di writeback.  
  
 `IdleConnectionTimeout`  
 Proprietà Integer che specifica un timeout, espresso in secondi, per le connessioni inattive.  
  
 Il valore predefinito di questa proprietà è zero (0). Ciò significa che non verrà imposto un timeout per le connessioni inattive.  
  
 `IdleOrphanSessionTimeout`  
 Proprietà Integer che definisce per quanti secondi le sessioni isolate (orfane) vengono mantenute nella memoria del server. Una sessione orfana è una sessione a cui non è associata alcuna connessione. Il valore predefinito è 120 secondi.  
  
 `InstanceVisible`  
 Proprietà booleana che indica se è l'istanza del server è visibile alle richieste di individuazione di istanze provenienti dal servizio per SQL Server Browser. Il valore predefinito è True. Se si imposta questa proprietà su false, l'istanza non sarà visibile a SQL Server Browser.  
  
 `Language`  
 Proprietà stringa che definisce la lingua, inclusi i messaggi di errore e la formattazione dei numeri. Questa proprietà ha la priorità sulla proprietà CollationName.  
  
 Il valore predefinito di questa proprietà è vuoto. Ciò significa che la lingua viene definita dalla proprietà CollationName.  
  
 `LogDir`  
 Proprietà stringa che identifica il nome della directory contenente i log del server. Questa proprietà viene applicata solo quando per la registrazione vengono utilizzati file su disco invece di tabelle di database (condizione predefinita).  
  
 `MaxIdleSessionTimeout`  
 Proprietà Integer che definisce il timeout massimo in secondi per le sessioni inattive. L'impostazione predefinita è zero (0). Ciò significa che non si verifica mai un timeout per le sessioni. Le sessioni inattive verranno comunque rimosse se il server presenta vincoli di risorse.  
  
 `MinIdleSessionTimeout`  
 Proprietà Integer che definisce il timeout minimo in secondi per le sessioni inattive. Il valore predefinito è 2700 secondi. Trascorso questo tempo, al server è consentito terminare la sessione inattiva, operazione che viene eseguita solo quando è richiesta memoria.  
  
 `Port`  
 Proprietà Integer che definisce il numero di porta su cui il server rimarrà in attesa di connessioni client. Se questa proprietà non viene impostata, il server trova in modo dinamico la prima porta non utilizzata.  
  
 Il valore predefinito di questa proprietà è zero (0) al quale per impostazione predefinita viene assegnata la porta 2383. Per altre informazioni sulla configurazione della porta, vedere [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 `ServerTimeout`  
 Proprietà Integer che definisce il timeout, in secondi, per le query. L'impostazione predefinita è 3600 secondi (o 60 minuti). Il valore zero (0) indica che non si verificherà alcun timeout per le query.  
  
 `TempDir`  
 Proprietà stringa che specifica il percorso per l'archiviazione dei file temporanei utilizzati durante operazioni quali elaborazione o ripristino. Il valore predefinito di questa proprietà è determinato dal programma di installazione. Se questa proprietà non viene impostata, il valore predefinito è la directory dati.  
  
## <a name="requestprioritization-category"></a>Categoria RequestPrioritization  
 `Enabled`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `StatisticsStoreSize`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà del Server in Analysis Services](server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
