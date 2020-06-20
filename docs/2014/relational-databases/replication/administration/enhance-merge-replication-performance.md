---
title: Migliorare le prestazioni della replica di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 443ce7c1da881edfe2c3b40d27e352498d416cc0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061613"
---
# <a name="enhance-merge-replication-performance"></a>Miglioramento delle prestazioni della replica di tipo merge
  Dopo aver valutato i suggerimenti relativi alle prestazioni generali descritti in [Miglioramento delle prestazioni generali della replica](enhance-general-replication-performance.md), è opportuno considerare questi ulteriori aspetti specifici della replica di tipo merge.  
  
## <a name="database-design"></a>Progettazione di database  
  
-   Colonne di indice utilizzate in filtri di riga e filtri join.  
  
     Se si applica un filtro di riga a un articolo pubblicato, è necessario creare un indice per ogni colonna specificata nella clausola WHERE del filtro. In assenza di un indice, ogni riga della tabella deve essere letta da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per determinare se debba essere inclusa o meno nella partizione. In presenza dell'indice, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è in grado di individuare rapidamente le righe da includere. L'elaborazione più rapida si ottiene quando tramite la replica è possibile risolvere completamente la clausola WHERE del filtro solo in base all'indice.  
  
     È inoltre importante indicizzare tutte le colonne utilizzate nei filtri join. A ogni esecuzione dell'agente di merge viene eseguita la ricerca della tabella di base per determinare quali righe della tabella padre e delle tabelle correlate sono incluse in una partizione. La creazione di un indice delle colonne unite in join consente di evitare la lettura di ogni riga della tabella da parte di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ogni esecuzione dell'agente di merge.  
  
     Per altre informazioni sui filtri, vedere [Filtrare i dati pubblicati per la replica di tipo merge](../merge/filter-published-data-for-merge-replication.md).  
  
-   ‏Si considerino le tabelle in fase di sovranormalizzazione che includono tipi di dati LOB (Large Object).  
  
     Quando viene eseguita la sincronizzazione, è possibile che l'agente di merge debba leggere e trasferire l'intera riga di dati da un server di pubblicazione o un Sottoscrittore. Se la riga include colonne con dati LOB, questo processo può richiedere l'allocazione di memoria aggiuntiva e influire negativamente sulle prestazioni anche se tali colonne non sono state aggiornate. Per ridurre la probabilità di tale impatto negativo sulle prestazioni, è possibile inserire le colonne LOB in una tabella distinta utilizzando una relazione uno-a-uno con la parte rimanente della riga di dati. I tipi di dati `text`, `ntext` e `image` sono deprecati. Se è necessario includere dati LOB, è consigliabile utilizzare rispettivamente i tipi di dati `varchar(max)`, `nvarchar(max)` e `varbinary(max)`.  
  
## <a name="publication-design"></a>Progettazione della pubblicazione  
  
-   Impostare il livello di compatibilità della pubblicazione su 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva).  
  
     A meno che uno o più Sottoscrittori utilizzino una versione diversa di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], specificare che la pubblicazione deve supportare solo [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. Ciò consente di sfruttare le nuove funzionalità e le ottimizzazioni delle prestazioni.  
  
-   Utilizzare impostazioni appropriate relative al periodo di memorizzazione della pubblicazione.  
  
     Il periodo di memorizzazione della pubblicazione, ovvero il periodo di tempo massimo prima che una sottoscrizione debba essere sincronizzata, determina la durata dell'archiviazione dei metadati di rilevamento. Un valore elevato può influire sulle prestazioni di elaborazione e archiviazione. Per ulteriori informazioni sull'impostazione del periodo di memorizzazione della pubblicazione, vedere [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md).  
  
-   Utilizzare articoli di solo download per le tabelle modificate solo nel server di pubblicazione. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### <a name="filter-design-and-use"></a>Progettazione e utilizzo dei filtri  
  
-   Limitare la complessità delle clausole dei filtri di riga.  
  
     Limitando la complessità dei criteri di filtro è possibile migliorare le prestazioni durante la valutazione da parte dell'agente di merge delle modifiche delle righe da inviare ai Sottoscrittori. Evitare di utilizzare selezioni secondarie all'interno delle clausole dei filtri di riga. Considerare, invece, l'opportunità di utilizzare filtri di join, in genere più efficienti se utilizzati per partizionare i dati di una tabella in base alla clausola del filtro di riga di un'altra tabella. Per altre informazioni sui filtri, vedere [Filtrare i dati pubblicati per la replica di tipo merge](../merge/filter-published-data-for-merge-replication.md).  
  
-   Utilizzare partizioni pre-calcolate con filtri con parametri (funzionalità utilizzata per impostazione predefinita). Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
     Le partizioni pre-calcolate impongono vari limiti al funzionamento dei filtri. Se l'applicazione non è in grado di rispettare tali limiti, impostare l'opzione **keep_partition_changes** su **True**. Ciò consente di migliorare le prestazioni. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Utilizzare partizioni non sovrapposte se i dati vengono filtrati ma non condivisi tra gli utenti.  
  
     La replica consente di ottimizzare le prestazioni dei dati che non vengono condivisi tra partizioni o sottoscrizioni. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Evitare di creare gerarchie di filtri join complesse.  
  
     I filtri join composti da più di cinque tabelle possono avere un impatto decisivo sulle prestazioni durante l'elaborazione di tipo merge. Se è necessario generare filtri join per cinque o più tabelle, è consigliabile optare per altre soluzioni:  
  
    -   Evitare di filtrare le tabelle che fungono principalmente da tabelle di ricerca, le tabelle di dimensioni ridotte e le tabelle non soggette a modifica, che è preferibile inserire nella pubblicazione senza ricorrere ad alcun filtro. È consigliabile utilizzare filtri join solo tra tabelle che devono essere partizionate tra i Sottoscrittori. Per altre informazioni, vedere [Join Filters](../merge/join-filters.md).  
  
    -   Considerare la denormalizzazione della progettazione del database o l'utilizzo di una tabella di mapping qualora in un join siano presenti molte tabelle. Ad esempio, se un venditore necessita solo dei dati relativi ai propri clienti e per associare un cliente a un determinato venditore sono necessari sei join, considerare l'opportunità di aggiungere alla tabella dei clienti una colonna che identifica il venditore. I dati del venditore sono ridondanti, ma i costi della denormalizzazione delle tabelle vengono compensati in una certa misura dai vantaggi a livello delle prestazioni per la partizione della replica.  
  
    -   Per migliorare le prestazioni delle partizioni pre-calcolate quando i batch contengono molte modifiche ai dati, progettare l'applicazione con attenzione. Assicurare che le modifiche ai dati nella tabella padre in un filtro join vengano apportate prima delle corrispondenti modifiche nelle tabelle figlio.  
  
-   Impostare l'opzione **join_unique_key** su **1** se la logica lo consente.  
  
     Impostando questo parametro su **1** , la relazione tra le tabelle figlio e le tabelle padre in un filtro join sarà di tipo uno-a-uno o uno-a-molti. Impostare questo parametro su **1** solo se esiste un vincolo nella colonna di join della tabella figlio che garantisce l'univocità. Un'impostazione non corretta del parametro su **1** può impedire la convergenza dei dati. Per altre informazioni, vedere [Join Filters](../merge/join-filters.md).  
  
-   Non eseguire batch con molte modifiche se si utilizzano partizioni pre-calcolate.  
  
     Se l'agente di merge viene eseguito dopo un batch che contiene molte modifiche ai dati, tenterà di suddividere il batch di grandi dimensioni in batch minori. Nel frattempo altri processi dell'agente di merge potrebbero risultare bloccati. Provare a ridurre il numero di modifiche contenute in un batch e ad eseguire l'agente di merge tra i batch. Se non è possibile, aumentare il valore di **generation_leveling_threshold** per la pubblicazione.  
  
## <a name="subscription-considerations"></a>Considerazioni sulle sottoscrizioni  
  
-   Scaglionare le pianificazioni di sincronizzazione delle sottoscrizioni.  
  
     Nel caso in cui un numero elevato di Sottoscrittori esegua la sincronizzazione con un server di pubblicazione, considerare l'opportunità di scaglionare le pianificazioni in modo che gli agenti di merge vengano eseguiti in momenti diversi. Per altre informazioni, vedere [Specify Synchronization Schedules](../specify-synchronization-schedules.md).  
  
## <a name="merge-agent-parameters"></a>Parametri dell'agente di merge  
 Per informazioni sull'agente di merge e sui relativi parametri, vedere [Replication Merge Agent](../agents/replication-merge-agent.md).  
  
-   Aggiornare tutti i Sottoscrittori per le sottoscrizioni pull a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva.  
  
     Se si aggiorna il Sottoscrittore a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva, viene aggiornato anche l'agente di merge utilizzato dalle sottoscrizioni nel Sottoscrittore. Per poter utilizzare molte delle nuove funzionalità e ottimizzazioni delle prestazioni, è necessario l'agente di merge di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva.  
  
-   Se la sincronizzazione di una sottoscrizione avviene con una connessione veloce e le modifiche vengono inviate dal server di pubblicazione e dal Sottoscrittore, usare il parametro **-ParallelUploadDownload** per l'agente di merge.  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]è stato introdotto un nuovo agente di merge parametro: **-ParallelUploadDownload**. L'impostazione di questo parametro consente di elaborare in parallelo le modifiche caricate nel server di pubblicazione e le modifiche scaricate nel Sottoscrittore. Ciò è utile negli ambienti caratterizzati da volumi di traffico elevati con un'ampia larghezza di banda di rete. I parametri degli agenti possono essere specificati nei profili agente e dalla riga di comando. Per altre informazioni, vedere:  
  
    -   [Usare i profili agenti di replica](../agents/replication-agent-profiles.md)  
  
    -   [Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica &#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
-   Provare ad aumentare il valore del parametro **-MakeGenerationInterval** , in particolare se la sincronizzazione prevede più caricamenti che download dai Sottoscrittori.  
  
-   Quando si sincronizzano righe di dati con un'ingente quantità di dati, ad esempio righe con colonne LOB, la sincronizzazione tramite il Web può richiedere l'allocazione di memoria aggiuntiva e ridurre le prestazioni. Ciò si verifica quando l'agente di merge genera un messaggio XML contenente un numero troppo elevato di righe di dati con ingenti quantità di dati. Se l'agente di merge utilizza una quantità eccessiva di risorse durante la sincronizzazione tramite il Web, ridurre il numero di righe inviate in un singolo messaggio in uno dei modi seguenti:  
  
    -   Utilizzare il profilo agente a collegamento lento per l'agente di merge. Per altre informazioni, vedere [Replication Agent Profiles](../agents/replication-agent-profiles.md).  
  
    -   Ridurre i parametri **- DownloadGenerationsPerBatch** e **- UploadGenerationsPerBatch** per l'agente di merge a un valore pari a 10 o meno. Il valore predefinito di questi parametri è 50.  
  
## <a name="snapshot-considerations"></a>Considerazioni sugli snapshot  
  
-   Creare una colonna ROWGUIDCOL nelle tabelle di grandi dimensioni prima di generare lo snapshot iniziale.  
  
     La replica di tipo merge richiede che ogni tabella pubblicata includa una colonna ROWGUIDCOL. Se la colonna ROWGUIDCOL non è disponibile quando l'agente snapshot crea i file di snapshot iniziali, l'agente dovrà innanzitutto aggiungere e popolare la colonna ROWGUIDCOL. Per migliorare le prestazioni delle operazioni di generazione di snapshot durante la replica di tipo merge, creare la colonna ROWGUIDCOL in tutte le tabelle prima della pubblicazione. Anche se, per impostazione predefinita, l'agente snapshot utilizza il nome**rowguid** , a tale colonna può essere assegnato qualsiasi nome che includa le funzionalità seguenti relative al tipo di dati:  
  
    -   Un tipo di dati UNIQUEIDENTIFIER.  
  
    -   Un valore predefinito di tipo NEWSEQUENTIALID() o NEWID(). Per garantire un migliore livello di prestazioni durante l'inserimento e il rilevamento di modifiche, è consigliabile utilizzare NEWSEQUENTIALID().  
  
    -   Il set di proprietà ROWGUIDCOL.  
  
    -   Un indice univoco nella colonna.  
  
-   Creare snapshot preliminari e/o consentire ai Sottoscrittori di richiedere la generazione e l'applicazione di snapshot alla prima sincronizzazione.  
  
     Utilizzare una o entrambe le opzioni per generare snapshot per le pubblicazioni che utilizzando filtri con parametri. Se non si specifica alcuna opzione, le sottoscrizioni vengono inizializzate tramite una serie di istruzioni SELECT e INSERT, anziché tramite l'utilità **bcp** . Questo processo risulta decisamente più lento. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="maintenance-and-monitoring-considerations"></a>Considerazioni sulla manutenzione e sul monitoraggio  
  
-   Eseguire occasionalmente la reindicizzazione delle tabelle di sistema per la replica di tipo merge.  
  
     Come parte della manutenzione per la replica di tipo merge, controllare occasionalmente l'aumento delle dimensioni delle tabelle di sistema associate alla replica di tipo merge: **MSmerge_contents**, **MSmerge_genhistory**e **MSmerge_tombstone**, **MSmerge_current_partition_mappings**e **MSmerge_past_partition_mappings**. Reindicizzare periodicamente queste tabelle. Per altre informazioni, vedere [Riorganizzare e ricompilare gli indici](../../indexes/reorganize-and-rebuild-indexes.md).  
  
-   Monitorare le prestazioni della sincronizzazione utilizzando la scheda **Cronologia sincronizzazione** in Monitoraggio replica.  
  
     Per la replica di tipo merge in Monitoraggio replica nella scheda **Cronologia sincronizzazione** vengono visualizzate statistiche dettagliate di ogni articolo elaborato durante la sincronizzazione, inclusa la quantità di tempo impiegato in ogni fase di elaborazione (caricamento delle modifiche, download delle modifiche e così via). Ciò può essere utile per individuare tabelle specifiche che determinano rallentamenti ed è l'opzione migliore per risolvere problemi relativi alle prestazioni delle sottoscrizioni di tipo merge. Per altre informazioni sulla visualizzazione di statistiche dettagliate, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
