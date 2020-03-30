---
title: Migliorare le prestazioni generali della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Snapshot Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- performance [SQL Server replication], general considerations
- transactional replication, performance
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 8ac6758c3856858f6b10b17184705022aa51a62e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288189"
---
# <a name="enhance-general-replication-performance"></a>Miglioramento delle prestazioni generali della replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  È possibile migliorare le prestazioni generali di tutti i tipi di replica nell'applicazione e nella rete attenendosi alle istruzioni riportate in questo argomento.  
  
## <a name="server-and-network"></a>Server e rete  
  
-   Impostare la quantità minima e massima di memoria allocata a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].  
  
     Per impostazione predefinita, nel [!INCLUDE[ssDE](../../../includes/ssde-md.md)] i requisiti di memoria possono variare dinamicamente in base alle risorse di sistema disponibili. Per evitare che durante le attività di replica la memoria risulti insufficiente, impostare la quantità minima di memoria disponibile tramite l'opzione **min server memory** . Per evitare che il sistema operativo richieda memoria del disco, è inoltre possibile impostare una quantità massima di memoria mediante l'opzione **max server memory** . Per altre informazioni, vedere [Opzioni di configurazione del server Server Memory](../../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
-   Verificare la corretta allocazione dei file di dati e dei file di log del database. Utilizzare un'unità disco distinta per il log delle transazioni di tutti i database interessati dalla replica.  
  
     Per ridurre i tempi di scrittura delle transazioni, archiviare i file di log in un'unità disco diversa da quella in cui è archiviato il database. È possibile eseguire il mirroring dell'unità utilizzando la modalità 1 della tecnologia RAID (Redundant Array of Inexpensive Disks), se è necessario implementare la tolleranza di errore. Per gli altri file di database utilizzare RAID 0 o 0+1, a seconda delle esigenze specifiche di tolleranza di errore. Questo metodo è ottimale indipendentemente dal fatto che venga utilizzata o meno la replica.  
  
-   Valutare l'opportunità di aggiungere memoria ai server utilizzati per la replica, in particolare al server di distribuzione.  
  
-   Utilizzare computer multiprocessore.  
  
     Gli agenti di replica sono in grado di utilizzare processori aggiuntivi del server. In sistemi con utilizzo elevato della CPU è consigliabile installare una CPU più veloce o più CPU.  
  
-   Utilizzare una rete veloce.  
  
     La rete può rappresentare un significativo collo di bottiglia per le prestazioni, in particolare per la replica transazionale. È possibile migliorare notevolmente la propagazione delle modifiche nei Sottoscrittori utilizzando una rete veloce pari a 100 megabit al secondo (Mbps) o superiore. Se la rete è lenta, specificare le impostazioni di rete e i parametri degli agenti appropriati.  
  
## <a name="database-design"></a>Progettazione di database  
  
-   Seguire le procedure consigliate per la progettazione del database.  
  
     Un database replicato generalmente usufruisce delle stesse ottimizzazioni delle prestazioni di un database non replicato. È tuttavia consigliabile utilizzare gli indici con attenzione nel Sottoscrittore, tenendo presente che è necessario indicizzare la colonna chiave primaria nel Sottoscrittore, ma che ulteriori indici possono influire sulle prestazioni relative alle operazioni di inserimento, aggiornamento ed eliminazione.  
  
-   Valutare l'opportunità di impostare l'opzione di database READ_COMMITTED_SNAPSHOT.  
  
     Per ridurre la contesa tra l'attività dell'utente e quella dell'agente di replica, impostare questa opzione per i database di pubblicazione e sottoscrizione:  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Prestare attenzione alla logica dell'applicazione nei trigger.  
  
     La logica di business nei trigger definiti dall'utente nel Sottoscrittore può rallentare la replica delle modifiche in quest'ultimo:  
  
    -   Per la replica transazionale, può essere più conveniente includere tale logica in stored procedure personalizzate che consentono di applicare i comandi replicati. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
    -   Per la replica di tipo merge, può essere più conveniente utilizzare i gestori delle logiche di business. Per altre informazioni, vedere [Eseguire logiche di business durante la sincronizzazione di tipo merge](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
     Se si utilizzano trigger per mantenere l'integrità referenziale in tabelle pubblicate per la replica di tipo merge, specificare l'ordine di elaborazione delle tabelle in modo da ridurre il numero di tentativi necessari per l'agente di merge. Per altre informazioni, vedere [Specify merge replication options](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Specificare le opzioni per la replica di tipo merge).  
  
-   Limitare l'utilizzo dei tipi di dati LOB (Large Object).  
  
     Tali dati richiedono uno spazio di archiviazione e un'elaborazione maggiori rispetto ad altri tipi di dati di colonna. Non includere queste colonne negli articoli a meno che non sia necessario per l'applicazione in uso. I tipi di dati **text**, **ntext**e **image** sono deprecati. Se è necessario includere dati LOB, è consigliabile utilizzare rispettivamente i tipi di dati **varchar(max)** , **nvarchar(max)** e **varbinary(max)** .  
  
     Per la replica transazionale, provare a utilizzare il profilo dell'agente di distribuzione denominato **Profilo di distribuzione per flussi OLEDB**. Per altre informazioni, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="publication-design"></a>Progettazione della pubblicazione  
  
-   Pubblicare solo i dati necessari.  
  
     La semplicità di impostazione della replica favorisce la tendenza a pubblicare una quantità di dati maggiore di quella effettivamente necessaria con il conseguente utilizzo di risorse aggiuntive nei database di distribuzione e nei file di snapshot e la diminuzione della velocità effettiva dei dati richiesti. Evitare la pubblicazione di tabelle non necessarie e aggiornare le pubblicazioni con una frequenza minore.  
  
-   Ridurre i conflitti mediante la progettazione della pubblicazione e il comportamento dell'applicazione.  
  
     La modifica dei dati nei Sottoscrittori è consentita nella replica di tipo merge, nella replica transazionale con sottoscrizioni aggiornabili e nella replica transazionale peer-to-peer. La replica di tipo merge e la replica transazionale con sottoscrizioni aggiornabili supportano conflitti di dati se una determinata riga viene aggiornata in più nodi tra le sincronizzazioni. La replica peer-to-peer non supporta conflitti di dati e le modifiche dei dati devono essere partizionate. Indipendentemente dal tipo di replica utilizzato, è consigliabile partizionare le modifiche quando possibile, in modo da ridurre l'elaborazione richiesta per il rilevamento e la risoluzione dei conflitti.  
  
     Le modifiche possono essere partizionate pubblicando subset di dati in ogni Sottoscrittore oppure facendo in modo che un'applicazione indirizzi le modifiche relative a una specifica riga a uno determinato nodo:  
  
    -   La replica di tipo merge supporta la pubblicazione dei subset di dati utilizzando filtri con parametri con una singola pubblicazione. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
    -   La replica transazionale supporta la pubblicazione dei subset di dati utilizzando filtri statici con più pubblicazioni. Per altre informazioni, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Utilizzare i filtri di riga in modo razionale.  
  
     Quando una pubblicazione transazionale include uno o più articoli che utilizzano filtri di riga, l'agente di lettura log deve applicare il filtro a ogni riga interessata da un aggiornamento relativo alla tabella durante l'analisi del log delle transazioni. Questo, pertanto, influisce sulla velocità effettiva dell'agente di lettura log.  
  
     Analogamente, la replica di tipo merge deve valutare le righe modificate o eliminate per stabilire quali Sottoscrittori devono riceverle. Se si utilizzano i filtri di riga per ridurre i dati richiesti da un Sottoscrittore, questo tipo di elaborazione risulta più complesso e lento rispetto alla pubblicazione di tutte le righe di una tabella. Tenere conto che i minori requisiti di archiviazione in ogni Sottoscrittore sono controbilanciati dalla necessità di ottimizzazione della velocità effettiva. Per altre informazioni sui filtri, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
## <a name="subscription-considerations"></a>Considerazioni sulle sottoscrizioni  
  
-   Utilizzare sottoscrizioni pull se il numero di Sottoscrittori è elevato.  
  
     L'agente di distribuzione e l'agente di merge vengono eseguiti nel server di distribuzione per le sottoscrizioni push e nei Sottoscrittori per le sottoscrizioni pull. L'utilizzo delle sottoscrizioni pull può migliorare le prestazioni spostando l'elaborazione dell'agente dal server di distribuzione ai Sottoscrittori. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Provare a reinizializzare la sottoscrizione in caso di forte ritardo dei Sottoscrittori.  
  
     Se è necessario inviare ai Sottoscrittori quantità di modifiche elevate, può essere più conveniente reinizializzarle tutte con un nuovo snapshot anziché utilizzare la replica per spostare le singole modifiche. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
     Per la replica transazionale, nella scheda **Comandi non distribuiti** di Monitoraggio replica vengono visualizzate informazioni relative al numero di transazioni presenti nel database di distribuzione e non ancora distribuite in un Sottoscrittore e al tempo stimato per la relativa distribuzione. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="snapshot-considerations"></a>Considerazioni sugli snapshot  
  
-   Eseguire l'agente snapshot solo quando è necessario e non nei periodi di massima attività.  
  
     L'agente snapshot esegue la copia bulk dei dati provenienti dalla tabella pubblicata del server di pubblicazione in un file incluso nella cartella snapshot del server di distribuzione. Il processo di generazione di uno snapshot può richiedere un utilizzo elevato delle risorse e pertanto se ne sconsiglia la pianificazione nei periodi di massima attività.  
  
-   Utilizzare uno snapshot in modalità nativa a meno che non sia richiesto uno snapshot in modalità carattere.  
  
     Utilizzare lo snapshot predefinito in modalità nativa per tutti i Sottoscrittori tranne quelli non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e quelli che eseguono [!INCLUDE[ssEW](../../../includes/ssew-md.md)], i quali richiedono uno snapshot in modalità carattere.  
  
-   Utilizzare un'unica cartella snapshot per pubblicazione.  
  
     Quando si specificano le proprietà di una pubblicazione correlate alla posizione dello snapshot, è possibile scegliere di generare file di snapshot nella cartella snapshot predefinita e/o alternativa. Per generare file di snapshot in entrambe le posizioni è necessario spazio di archiviazione aggiuntivo e un'ulteriore elaborazione durante l'esecuzione dell'agente snapshot.  
  
-   Installare la cartella snapshot in un'unità locale sul server di distribuzione non utilizzata per l'archiviazione di file di database o di log.  
  
     L'agente snapshot esegue una scrittura sequenziale dei dati nella cartella snapshot. Installando la cartella snapshot in un'unità separata da quella in cui risiedono i file di database o di log è possibile ridurre la contesa tra i dischi e completare più rapidamente il processo di snapshot.  
  
-   Quando si crea il database di sottoscrizione nel Sottoscrittore, provare a specificare un modello di recupero con registrazione minima o con registrazione minima delle operazioni bulk. Questo consente la registrazione minima degli inserimenti bulk eseguiti durante l'applicazione dello snapshot nel Sottoscrittore. Se necessario, dopo aver applicato lo snapshot al database di sottoscrizione, è possibile passare a un modello di recupero differente (con i database replicati è consentito l'utilizzo di uno qualsiasi dei modelli di recupero). Per informazioni sulla selezione di un modello di recupero, vedere [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
-   Provare a utilizzare la cartella snapshot alternativa e gli snapshot compressi sui supporti rimovibili per le reti a larghezza di banda ridotta.  
  
     La compressione dei file di snapshot nella cartella snapshot alternativa può ridurre i requisiti di archiviazione su disco degli snapshot e semplificare il trasferimento dei file di snapshot sui supporti rimovibili.  
  
     Gli snapshot compressi, in alcuni casi, consentono di migliorare le prestazioni relative al trasferimento di file di snapshot in rete. La compressione dello snapshot richiede, tuttavia, un'ulteriore elaborazione da parte dell'agente snapshot per la generazione dei file di snapshot e da parte dell'agente di distribuzione o dell'agente di merge per l'applicazione di tali file. Questo può rallentare il processo di generazione degli snapshot e, in alcuni casi, aumentare il tempo necessario per applicarli. Inoltre, poiché non è possibile riprendere gli snapshot compressi in caso di errore della rete, tali snapshot non sono adatti per le reti non affidabili. Quando si utilizzano snapshot compressi in rete, è necessario considerare tutti i pro e contro. Per altre informazioni, vedere [Modificare le opzioni snapshot](../../../relational-databases/replication/snapshot-options.md). 
-   Provare a inizializzare una sottoscrizione manualmente.  
  
     In alcuni scenari, ad esempio quelli che comportano l'utilizzo di set di dati iniziali di grandi dimensioni, è preferibile inizializzare una sottoscrizione utilizzando un metodo diverso dallo snapshot. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
## <a name="agent-parameters"></a>Parametri degli agenti  
  
-   Ridurre i livelli di dettaglio degli agenti di replica eccetto durante le operazioni iniziali di verifica, monitoraggio o debug.  
  
     Ridurre i parametri **–HistoryVerboseLevel** e **–OutputVerboseLevel** degli agenti di distribuzione o di merge. per ridurre il numero di nuove righe inserite ai fini del rilevamento della cronologia e dell'output degli agenti. I messaggi precedenti sulla cronologia con lo stesso stato vengono invece aggiornati in base alle nuove informazioni relative alla cronologia. Aumentare i livelli di dettaglio ai fini della verifica, del monitoraggio e del debug in modo da ottenere il maggior numero possibile di informazioni sull'attività degli agenti.  
  
-   Usare il parametro **–MaxBCPThreads** dell'agente snapshot, dell'agente di merge e dell'agente di distribuzione in modo che il numero di thread specificati non superi il numero di processori installati nel computer. Questo parametro specifica il numero di operazioni di copia bulk che è possibile eseguire in parallelo quando lo snapshot viene creato e applicato.  
  
-   Usare il parametro **–UseInprocLoader** dell'agente di distribuzione e dell'agente di merge, tenendo presente che non è possibile usarlo se le tabelle pubblicate includono colonne XML. Grazie alla specifica di tale parametro, l'agente utilizzerà il comando BULK INSERT al momento dell'applicazione dello snapshot.  
  
 I parametri degli agenti possono essere specificati nei profili agente e dalla riga di comando. Per altre informazioni, vedere:  
  
-   [Usare i profili agenti di replica](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
  
