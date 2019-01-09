---
title: Strategie di backup e ripristino della replica snapshot e della replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication], snapshot replication
- restoring [SQL Server replication], transactional replication
- snapshot replication [SQL Server], backup and restore
- restoring [SQL Server replication], snapshot replication
- recovery [SQL Server replication], transactional replication
- transactional replication, backup and restore
- recovery [SQL Server replication], snapshot replication
- sync with backup [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: a8afcdbc-55db-4916-a219-19454f561f9e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 43be13027d1460ec407239140cd4306be76a445e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823516"
---
# <a name="strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication"></a>Strategie per il backup e il ripristino della replica snapshot e della replica transazionale
  Quando si progetta una strategia di backup e ripristino per la replica snapshot e la replica transazionale, è necessario considerare le tre aree di fattori seguenti:  
  
-   Database di cui eseguire il backup.  
  
-   Impostazioni di backup per la replica transazionale.  
  
-   Passaggi richiesti per ripristinare un database, i quali variano in base al tipo di replica e alle opzioni scelte.  
  
 In questo argomento vengono illustrate le tre aree elencate in precedenza. Per altre informazioni sul backup e il ripristino per la pubblicazione Oracle, vedere [Backup e ripristino di server di pubblicazione Oracle](../non-sql/backup-and-restore-for-oracle-publishers.md).  
  
## <a name="backing-up-databases"></a>Backup di database  
 Per la replica snapshot e la replica transazionale è necessario effettuare a intervalli regolari il backup dei database seguenti:  
  
-   Database di pubblicazione nel server di pubblicazione.  
  
-   Database di distribuzione nel database di distribuzione.  
  
-   Database di sottoscrizione in ogni Sottoscrittore.  
  
-   Database di sistema **master** e **msdb** nel server di pubblicazione, nel database di distribuzione e in tutti i Sottoscrittori. È necessario che il backup di questi database venga eseguito contemporaneamente e che venga inoltre eseguito nello stesso momento di quello del relativo database di replica. Eseguire ad esempio il backup dei database **master** e **msdb** nel server di pubblicazione nello stesso momento in cui si esegue il backup del database di pubblicazione. Se il database di pubblicazione viene ripristinato, verificare che i database **master** e **msdb** siano consistenti con il database di pubblicazione in termini di impostazioni e configurazione della replica.  
  
 Se si eseguono backup regolari del log, le eventuali modifiche correlate alla replica dovrebbero essere incluse nei backup del log. Se non si eseguono i backup del log, è necessario eseguire un backup ogni volta che un'impostazione relativa alla replica viene modificata. Per altre informazioni, vedere [Common Actions Requiring an Updated Backup](common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-settings-for-transactional-replication"></a>Impostazioni di backup per la replica transazionale  
 La replica transazionale implica l'utilizzo dell'opzione **sync with backup** , che può essere impostata nel database di distribuzione e nel database di pubblicazione:  
  
-   Si consiglia di impostare sempre questa opzione nel database di distribuzione.  
  
     L'impostazione di questa opzione nel database di distribuzione impedisce che le transazioni nel log del database di pubblicazione vengano troncate fino al relativo backup nel database di distribuzione. È possibile ripristinare lo stato del database di distribuzione al momento dell'ultimo backup. Eventuali transazioni mancanti verranno recapitate dal database di pubblicazione al database di distribuzione. La replica continua senza interruzioni.  
  
     L'impostazione di questa opzione nel database di distribuzione non influisce sulla latenza di replica. L'opzione ritarderà tuttavia il troncamento del log nel database di pubblicazione fino a quando non viene eseguito il backup delle transazioni corrispondenti nel database di distribuzione. Ciò può comportare la creazione di un log delle transazioni di dimensioni maggiori nel database di pubblicazione.  
  
-   Si consiglia di impostare questa opzione nel database di pubblicazione se l'applicazione in uso tollera un'ulteriore latenza.  
  
     L'impostazione di questa opzione nel database di pubblicazione garantisce che le transazioni vengano recapitate al database di distribuzione solo dopo che è stato eseguito il backup nel database di pubblicazione. Nel server di pubblicazione è quindi possibile ripristinare il backup più recente del database di pubblicazione, evitando che il database di distribuzione disponga di transazioni che risultino mancanti nel database di pubblicazione ripristinato.  
  
     La latenza e la velocità effettiva sono interessate da questo aspetto, in quanto le transazioni possono essere recapitate al database di distribuzione solo dopo che ne è stato eseguito il backup nel server di pubblicazione. Se ad esempio viene eseguito un backup del log delle transazioni ogni cinque minuti, si verifica un'ulteriore latenza di cinque minuti tra l'esecuzione del commit di una transazione nel server di pubblicazione e il recapito della transazione al database di distribuzione e successivamente al Sottoscrittore.  
  
    > [!NOTE]  
    >  L'opzione **sync with backup** garantisce la consistenza tra il database di pubblicazione e il database di distribuzione, ma non offre alcuna garanzia contro la perdita dei dati. Se ad esempio il log delle transazioni viene perso, le transazioni di cui è stato eseguito il commit dopo l'ultimo backup del log non saranno disponibili nel database di pubblicazione o nel database di distribuzione. Questo comportamento è identico a quello di un database non replicato.  
  
 **Per impostare l'opzione sync with backup**  
  
-   Programmazione [!INCLUDE[tsql](../../../includes/tsql-md.md)] della replica: [Abilitare backup coordinati per la replica transazionale &#40;programmazione Transact-SQL della replica&#41;](enable-coordinated-backups-for-transactional-replication.md)  
  
## <a name="restoring-databases-involved-in-replication"></a>Ripristino di database interessati da una replica  
 È possibile ripristinare tutti i database in una topologia di replica se sono disponibili backup recenti e viene eseguita la procedura appropriata. La procedura di ripristino per il database di pubblicazione dipende dal tipo di replica e dalle opzioni utilizzate, mentre quella per tutti gli altri database è indipendente da tali fattori.  
  
 La replica supporta il ripristino dei database replicati nello stesso server e nello stesso database da cui è stato creato il backup. Se si ripristina un backup di un database replicato in un altro server o database, le impostazioni di replica non potranno essere mantenute. In questo caso, è necessario ricreare tutte le pubblicazioni e le sottoscrizioni dopo il ripristino dei backup.  
  
### <a name="publisher"></a>Server di pubblicazione  
 Sono disponibili procedure di ripristino per i tipi di replica seguenti:  
  
-   Replica snapshot  
  
-   Replica transazionale di sola lettura  
  
-   Replica transazionale con sottoscrizioni aggiornabili  
  
-   Replica transazionale peer-to-peer  
  
 Il ripristino dei database **msdb** e **master** , descritti in questa sezione, è identico per tutti i quattro tipi.  
  
#### <a name="publication-database-snapshot-replication"></a>Database di pubblicazione: Replica snapshot  
  
1.  Ripristinare il backup più recente del database di pubblicazione. Andare al passaggio 2.  
  
2.  Il backup del database di pubblicazione contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, il ripristino viene completato. In caso contrario, andare al passaggio 3.  
  
3.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Il ripristino viene completato.  
  
     Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
#### <a name="publication-database-read-only-transactional-replication"></a>Database di pubblicazione: Replica transazionale di sola lettura  
  
1.  Ripristinare il backup più recente del database di pubblicazione. Andare al passaggio 2.  
  
2.  L'opzione **sync with backup** era abilitata nel database di pubblicazione prima dell'errore? In caso affermativo, andare al passaggio 3. In caso contrario, andare al passaggio 5.  
  
     Se l'opzione è abilitata, la query `SELECT DATABASEPROPERTYEX('<PublicationDatabaseName>', 'IsSyncWithBackup')` restituisce "1".  
  
3.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, il ripristino viene completato. In caso contrario, andare al passaggio 4.  
  
4.  Le informazioni di configurazione nel database di pubblicazione ripristinato non sono aggiornate. È pertanto necessario assicurarsi che i Sottoscrittori dispongano di tutti i comandi in sospeso nel database di distribuzione, quindi eliminare e ricreare la configurazione della replica.  
  
    1.  Eseguire l'agente di distribuzione fino a completare la sincronizzazione in tutti i Sottoscrittori dei comandi in sospeso nel database di distribuzione. Verificare che tutti i comandi vengano recapitati ai Sottoscrittori utilizzando la scheda **Comandi non distribuiti** in Monitoraggio replica oppure eseguendo una query sulla vista [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) nel database di distribuzione. Andare al passaggio b.  
  
         Per altre informazioni su come eseguire l'agente di distribuzione, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
         Per altre informazioni su come verificare i comandi, vedere [Visualizzare comandi replicati e altre informazioni nel database di distribuzione &#40;programmazione Transact-SQL della replica&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Il ripristino viene completato.  
  
         Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
         Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
5.  L'opzione **sync with backup** non è stata impostata nel database di pubblicazione. Le transazioni che non sono state incluse nel backup ripristinato potrebbero pertanto essere state recapitate al database di distribuzione e ai Sottoscrittori. È a questo punto necessario assicurarsi che i Sottoscrittori dispongano di tutti i comandi in sospeso nel database di distribuzione, quindi applicare manualmente al database di pubblicazione eventuali transazioni non incluse nel backup ripristinato.  
  
    > [!IMPORTANT]  
    >  Questo processo può comportare il ripristino delle tabelle pubblicate in base a una temporizzazione più recente rispetto a quella di altre tabelle non pubblicate ripristinate dal backup.  
  
    1.  Eseguire l'agente di distribuzione fino a completare la sincronizzazione in tutti i Sottoscrittori dei comandi in sospeso nel database di distribuzione. Verificare che tutti i comandi vengano recapitati ai Sottoscrittori utilizzando la scheda **Comandi non distribuiti** in Monitoraggio replica oppure eseguendo una query sulla vista [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) nel database di distribuzione. Andare al passaggio b.  
  
         Per altre informazioni su come eseguire l'agente di distribuzione, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
         Per altre informazioni su come verificare i comandi, vedere [Visualizzare comandi replicati e altre informazioni nel database di distribuzione &#40;programmazione Transact-SQL della replica&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
    2.  Utilizzare l' [utilità tablediff](../../../tools/tablediff-utility.md) o un altro strumento per sincronizzare manualmente il server di pubblicazione con il Sottoscrittore. Questa operazione consente di recuperare i dati del database di sottoscrizione non inclusi nel backup del database di pubblicazione. Andare al passaggio c.  
  
         Per altre informazioni sull'utilità **tablediff**, vedere [Confrontare tabelle replicate al fine di individuare le differenze &#40;programmazione della replica&#41;](compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, eseguire la stored procedure [sp_replrestart](/sql/relational-databases/system-stored-procedures/sp-replrestart-transact-sql) per risincronizzare i metadati del server di pubblicazione con i metadati del database di distribuzione. Il ripristino viene completato. In caso contrario, andare al passaggio d.  
  
    4.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Il ripristino viene completato.  
  
         Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
         Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-transactional-replication-with-updating-subscriptions"></a>Database di pubblicazione: Replica transazionale con sottoscrizioni aggiornabili  
  
1.  Ripristinare il backup più recente del database di pubblicazione. Andare al passaggio 2.  
  
2.  Eseguire l'agente di distribuzione fino a completare la sincronizzazione in tutti i Sottoscrittori dei comandi in sospeso nel database di distribuzione. Verificare che tutti i comandi vengano recapitati ai Sottoscrittori utilizzando la scheda **Comandi non distribuiti** in Monitoraggio replica oppure eseguendo una query sulla vista [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) nel database di distribuzione. Andare al passaggio 3.  
  
     Per altre informazioni su come eseguire l'agente di distribuzione, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
     Per altre informazioni su come verificare i comandi, vedere [Visualizzare comandi replicati e altre informazioni nel database di distribuzione &#40;programmazione Transact-SQL della replica&#41;](../monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
3.  Se si usano sottoscrizioni ad aggiornamento in coda, connettersi a ogni Sottoscrittore ed eliminare tutte le righe dalla tabella [MSreplication_queue &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/msreplication-queue-transact-sql) nel database di sottoscrizione. Andare al passaggio 4.  
  
    > [!NOTE]  
    >  Se si utilizzano sottoscrizioni ad aggiornamento in coda e le tabelle contengono colonne Identity, è necessario assicurarsi che dopo un ripristino vengano assegnati gli intervalli di valori Identity corretti. Per altre informazioni, vedere [Replicare colonne Identity](../publish/replicate-identity-columns.md).  
  
4.  È a questo punto necessario assicurarsi che i Sottoscrittori dispongano di tutti i comandi in sospeso nel database di distribuzione, quindi applicare manualmente al database di pubblicazione eventuali transazioni non incluse nel backup ripristinato.  
  
    > [!IMPORTANT]  
    >  Questo processo può comportare il ripristino delle tabelle pubblicate in base a una temporizzazione più recente rispetto a quella di altre tabelle non pubblicate ripristinate dal backup.  
  
    1.  Eseguire l'agente di distribuzione fino a completare la sincronizzazione in tutti i Sottoscrittori dei comandi in sospeso nel database di distribuzione. Verificare che tutti i comandi vengano recapitati ai Sottoscrittori utilizzando Monitoraggio replica oppure eseguendo una query sulla vista [MSdistribution_status](/sql/relational-databases/system-views/msdistribution-status-transact-sql) nel database di distribuzione. Andare al passaggio b.  
  
    2.  Utilizzare l' [tablediff Utility](../../../tools/tablediff-utility.md) o un altro strumento per sincronizzare manualmente il server di pubblicazione con il Sottoscrittore. Questa operazione consente di recuperare i dati del database di sottoscrizione non inclusi nel backup del database di pubblicazione. Andare al passaggio c.  
  
         Per altre informazioni sull'utilità **tablediff**, vedere [Confrontare tabelle replicate al fine di individuare le differenze &#40;programmazione della replica&#41;](compare-replicated-tables-for-differences-replication-programming.md).  
  
    3.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, eseguire la stored procedure [sp_replrestart](/sql/relational-databases/system-stored-procedures/sp-replrestart-transact-sql) per risincronizzare i metadati del server di pubblicazione con i metadati del database di distribuzione. Il ripristino viene completato. In caso contrario, andare al passaggio d.  
  
    4.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Il ripristino viene completato.  
  
         Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
         Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
#### <a name="publication-database-peer-to-peer-transactional-replication"></a>Database di pubblicazione: Replica transazionale peer-to-peer  
 Nella procedura seguente i database di pubblicazione **A**, **B**e **C** sono inclusi in una topologia di replica transazionale peer-to-peer. I database **A** e **C** sono online e funzionano correttamente. Il database **B** è il database da ripristinare. Il processo descritto, specialmente i passaggi 7, 10 e 11, è molto simile al processo per l'aggiunta di un nodo a una topologia peer-to-peer. Il modo più semplice per eseguire questi passaggi consiste nell'utilizzare la Configurazione guidata topologia peer-to-peer, ma è possibile utilizzare anche stored procedure.  
  
1.  Eseguire gli agenti di distribuzione per sincronizzare le sottoscrizioni nei database **A** e **C**. Andare al passaggio 2.  
  
     Per altre informazioni su come eseguire l'agente di distribuzione, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
2.  Se il database di distribuzione usato da **B** è ancora disponibile, eseguire gli agenti di distribuzione per sincronizzare le sottoscrizioni tra i database **B** e **A** e tra i database B e **C**. Andare al passaggio 3.  
  
3.  Rimuovere i metadati dal database di distribuzione usato da **B** eseguendo [sp_removedistpublisherdbreplication](/sql/relational-databases/system-stored-procedures/sp-removedistpublisherdbreplication-transact-sql) nel database di distribuzione per **B**. Andare al passaggio 4.  
  
4.  Nei database **A** e **C** eliminare le sottoscrizioni della pubblicazione nel database **B**. Andare al passaggio 5.  
  
     Per ulteriori informazioni sull'eliminazione delle sottoscrizioni, vedere [Subscribe to Publications](../subscribe-to-publications.md).  
  
5.  Eseguire un backup del log oppure un backup completo del database **A**. Andare al passaggio 6.  
  
6.  Ripristinare il backup del database **A** nel database **B**. Il database **B** contiene ora i dati del database **A**, ma non la configurazione della replica. Quando si ripristina un backup in un altro server, la replica viene rimossa. La replica è stata quindi rimossa dal database **B**. Andare al passaggio 7.  
  
7.  Ricreare la pubblicazione nel database **B** e quindi ricreare le sottoscrizioni tra i database **A** e **B**. Le sottoscrizioni che interessano il database **C** vengono gestite in una fase successiva.  
  
    1.  Ricreare la pubblicazione nel database **B**. Andare al passaggio b.  
  
    2.  Ricreare la sottoscrizione nel database **B** della pubblicazione nel database **A**, specificando che è necessario inizializzare la sottoscrizione con un backup, ovvero impostando il valore **initialize with backup** per il parametro **@sync_type** di [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Andare al passaggio c.  
  
    3.  Ricreare la sottoscrizione nel database **A** della pubblicazione nel database **B**, specificando che nel Sottoscrittore sono già disponibili i dati, ovvero impostando il valore **replication support only** per il parametro **@sync_type** di [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Andare al passaggio 8.  
  
8.  Eseguire gli agenti di distribuzione per sincronizzare le sottoscrizioni nei database **A** e **B**. In presenza di eventuali colonne Identity nelle tabelle pubblicate, andare al passaggio 9. In caso contrario, andare al passaggio 10.  
  
9. In seguito al ripristino, l'intervallo di valori Identity assegnato a ogni tabella nel database **A** verrà usato anche nel database **B**. Assicurarsi che il database **B** ripristinato abbia ricevuto tutte le modifiche del database **B** bloccato propagate nel database **A** e nel database **C** e quindi reinizializzare l'intervallo di valori Identity per ogni tabella.  
  
    1.  Eseguire [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) nel database **B** e recuperare il parametro di output **@request_id**. Andare al passaggio b.  
  
    2.  Per impostazione predefinita, l'agente di distribuzione è impostato per l'esecuzione continua. I token dovrebbero pertanto essere inviati automaticamente a tutti i nodi. Se l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. Per altre informazioni, vedere [Concetti di base relativi ai file eseguibili dell’agente di replica](../concepts/replication-agent-executables-concepts.md) o [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md). Andare al passaggio c.  
  
    3.  Eseguire [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql), specificando il valore **@request_id** recuperato nel passaggio b. Attendere finché tutti i nodi indicano di avere ricevuto la richiesta peer. Andare al passaggio d.  
  
    4.  Utilizzare [DBCC CHECKIDENT](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql) per reinizializzare ciascuna tabella nel database **B** , in modo da garantire l'utilizzo di un intervallo appropriato. Andare al passaggio 10.  
  
     Per altre informazioni sulla gestione di intervalli di valori Identity, vedere la sezione "Assegnazione di intervalli per la gestione manuale degli intervalli di valori Identity" in [Replicare colonne Identity](../publish/replicate-identity-columns.md).  
  
10. A questo punto, il database **B** e il database **C** non sono direttamente connessi, ma riceveranno le modifiche tramite il database **A**. Se la topologia contiene nodi in cui è eseguito [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], andare al passaggio 11. Altrimenti, andare al passaggio 12.  
  
11. Mettere in stato di inattività il sistema e ricreare la sottoscrizione tra i database **B** e **C**. Mettere in stato di inattività un sistema significa arrestare le attività sulle tabelle pubblicate in tutti i nodi e verificare che ogni nodo abbia ricevuto tutte le modifiche dagli altri nodi:  
  
    1.  Arrestare qualsiasi attività sulle tabelle pubblicate nella topologia peer-to-peer. Andare al passaggio b.  
  
    2.  Eseguire [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) nel database **B** e recuperare il parametro di output **@request_id**. Andare al passaggio c.  
  
    3.  Per impostazione predefinita, l'agente di distribuzione è impostato per l'esecuzione continua. I token dovrebbero pertanto essere inviati automaticamente a tutti i nodi. Se l'agente di distribuzione non viene eseguito in modalità continua, eseguire l'agente. Andare al passaggio d.  
  
    4.  Eseguire [sp_helppeerresponses](/sql/relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql), specificando il valore **@request_id** recuperato nel passaggio b. Attendere finché tutti i nodi indicano di avere ricevuto la richiesta peer. Andare al passaggio e.  
  
    5.  Ricreare la sottoscrizione nel database **B** della pubblicazione nel database **C**, specificando che nel Sottoscrittore i dati sono già disponibili. Andare al passaggio b.  
  
    6.  Ricreare la sottoscrizione nel database **C** della pubblicazione nel database **B**, specificando che nel Sottoscrittore i dati sono già disponibili. Andare al passaggio 13.  
  
12. Ricreare la sottoscrizione tra i database **B** e **C**:  
  
    1.  Nel database **B**eseguire una query sulla tabella [MSpeer_lsns](/sql/relational-databases/system-tables/mspeer-lsns-transact-sql) per recuperare il numero di sequenza del file di log (LSN) della transazione più recente che il database **B** ha ricevuto dal database **C**.  
  
    2.  Ricreare la sottoscrizione nel database **B** della pubblicazione nel database **C**, specificando che è necessario inizializzare la sottoscrizione in base al numero LSN, ovvero impostando il valore **initialize from lsn** per il parametro **@sync_type** di [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Andare al passaggio b.  
  
    3.  Ricreare la sottoscrizione nel database **C** della pubblicazione nel database **B**, specificando che nel Sottoscrittore i dati sono già disponibili. Andare al passaggio 13.  
  
13. Eseguire gli agenti di distribuzione per sincronizzare le sottoscrizioni nei database **B** e **C**. Il ripristino viene completato.  
  
#### <a name="msdb-database-publisher"></a>Database msdb (server di pubblicazione)  
  
1.  Ripristinare il backup più recente del database **msdb** .  
  
2.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, il recupero viene completato. In caso contrario, andare al passaggio 3.  
  
3.  Ricreare il processo di pulizia dei riferimenti alle sottoscrizioni dagli script di replica. Il recupero viene completato.  
  
#### <a name="master-database-publisher"></a>Database master (server di pubblicazione)  
  
1.  Ripristinare il backup più recente del database **master** .  
  
2.  Assicurarsi che il database sia consistente con il database di pubblicazione in termini di impostazioni e configurazione della replica.  
  
### <a name="databases-at-the-distributor"></a>Database nel database di distribuzione  
  
#### <a name="distribution-database"></a>Database di distribuzione  
  
1.  Ripristinare il backup più recente del database di distribuzione.  
  
2.  L'opzione **sync with backup** era abilitata nel database di distribuzione prima dell'errore? In caso affermativo, andare al passaggio 3. In caso contrario, andare al passaggio 4.  
  
     Se l'opzione è abilitata, la query `SELECT DATABASEPROPERTYEX('<DistributionDatabaseName>', 'IsSyncWithBackup')` restituisce "1".  
  
3.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, il recupero viene completato. In caso contrario, andare al passaggio 4.  
  
4.  Le informazioni di configurazione nel database di distribuzione ripristinato non sono aggiornate o l'opzione **sync with backup** non è stata impostata nel database di distribuzione. Dopo il ripristino, è possibile che nel database di distribuzione manchino le transazioni di cui è stato eseguito il commit nel server di pubblicazione, ma che non sono state ancora recapitate ai Sottoscrittori. Eliminare e ricreare la replica, quindi eseguire la convalida.  
  
    1.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Andare al passaggio b.  
  
         Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
         Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
    2.  Contrassegnare tutte le pubblicazioni per la convalida. Reinizializzare eventuali sottoscrizioni che non superano la convalida. Il recupero viene completato.  
  
         Per ulteriori informazioni sulla convalida, vedere [Validate Replicated Data](../validate-replicated-data.md). Per altre informazioni sulla reinizializzazione, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
#### <a name="msdb-database-distributor"></a>Database msdb (database di distribuzione)  
  
1.  Ripristinare il backup più recente del database **msdb** .  
  
2.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le pubblicazioni e le sottoscrizioni? In caso affermativo, il recupero viene completato. In caso contrario, andare al passaggio 3.  
  
3.  Rimuovere la configurazione della replica dal server di pubblicazione, dal database di distribuzione e dai Sottoscrittori, quindi ricreare la configurazione. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Andare al passaggio 4.  
  
     Per altre informazioni su come rimuovere la replica, vedere [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
     Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
4.  Contrassegnare tutte le pubblicazioni per la convalida. Reinizializzare eventuali sottoscrizioni che non superano la convalida. Il recupero viene completato.  
  
     Per ulteriori informazioni sulla convalida, vedere [Validate Replicated Data](../validate-replicated-data.md). Per altre informazioni sulla reinizializzazione, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
#### <a name="master-database-distributor"></a>Database master (database di distribuzione)  
  
1.  Ripristinare il backup più recente del database **master** .  
  
2.  Assicurarsi che il database sia consistente con il database di pubblicazione in termini di impostazioni e configurazione della replica.  
  
### <a name="databases-at-the-subscriber"></a>Database nel Sottoscrittore  
  
#### <a name="subscription-database"></a>Database di sottoscrizione  
  
1.  L'ultimo backup del database di sottoscrizione è più recente dell'impostazione minima relativa alla memorizzazione per la distribuzione nel database di distribuzione? Questo aspetto determina se il database di distribuzione disponga ancora di tutti i comandi necessari per aggiornare il Sottoscrittore. In caso affermativo, andare al passaggio 2. In caso contrario, reinizializzare la sottoscrizione. Il recupero viene completato.  
  
     Per determinare l'impostazione massima relativa alla memorizzazione per la distribuzione, eseguire [sp_helpdistributiondb](/sql/relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql) e recuperare il valore dalla colonna **max_distretention** . Questo valore è espresso in ore.  
  
     Per ulteriori informazioni sulla reinizializzazione di una sottoscrizione, vedere [Reinitialize a Subscription](../reinitialize-a-subscription.md).  
  
2.  Ripristinare il backup del database di sottoscrizione più recente. Andare al passaggio 3.  
  
3.  Se il database di sottoscrizione contiene solo sottoscrizioni push, andare al passaggio 4. Se il database di sottoscrizione contiene sottoscrizioni pull, porsi le domande seguenti: Sia le informazioni sulla sottoscrizione corrente? Nel database sono incluse tutte le tabelle e le opzioni impostate al momento dell'errore? In caso affermativo, andare al passaggio 4. In caso contrario, reinizializzare la sottoscrizione. Il recupero viene completato.  
  
4.  Per sincronizzare il Sottoscrittore, eseguire l'agente di distribuzione. Il recupero viene completato.  
  
     Per altre informazioni su come eseguire l'agente di distribuzione, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
#### <a name="msdb-database-subscriber"></a>Database msdb (Sottoscrittore)  
  
1.  Ripristinare il backup più recente del database **msdb** . Nel Sottoscrittore vengono utilizzate sottoscrizioni pull? In caso di risposta negativa, il ripristino viene completato. In caso affermativo, andare al passaggio 2.  
  
2.  Il backup ripristinato è completo e aggiornato? Contiene la configurazione più recente per tutte le sottoscrizioni pull? In caso affermativo, il recupero viene completato. In caso contrario, andare al passaggio 3.  
  
3.  Eliminare e ricreare le sottoscrizioni pull. Quando si ricreano le sottoscrizioni, specificare che i dati sono già disponibili nel Sottoscrittore. Il ripristino viene completato.  
  
     Per ulteriori informazioni sull'eliminazione delle sottoscrizioni, vedere [Subscribe to Publications](../subscribe-to-publications.md).  
  
     Per ulteriori informazioni su come specificare che i dati sono già disponibili nel Sottoscrittore, vedere [Initialize a Subscription Manually](../initialize-a-subscription-manually.md).  
  
#### <a name="master-database-subscriber"></a>Database master (Sottoscrittore)  
  
1.  Ripristinare il backup più recente del database **master** .  
  
2.  Assicurarsi che il database sia consistente con il database di pubblicazione in termini di impostazioni e configurazione della replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database SQL Server](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backup e ripristino di database replicati](back-up-and-restore-replicated-databases.md)   
 [Configura distribuzione](../configure-distribution.md)   
 [Pubblicare dati e oggetti di database](../publish/publish-data-and-database-objects.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)   
 [Inizializzare una sottoscrizione](../initialize-a-subscription.md)   
 [Sincronizzare i dati](../synchronize-data.md)  
  
  
