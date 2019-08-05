---
title: Procedure consigliate per l'amministrazione della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 04cfff3e2772f945d01093bab15246924a104b2b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768842"
---
# <a name="best-practices-for-replication-administration"></a>Procedure consigliate per l'amministrazione della replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Dopo aver configurato la replica, è importante comprendere in che modo amministrare una topologia di replica. In questo argomento sono contenute procedure consigliate di base relative a diverse aree, con collegamenti ad altre informazioni per ogni area. Oltre ad attenersi a tali procedure, provare a familiarizzare con domande e problemi comuni leggendo: [Domande frequenti per gli amministratori di replica](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md).  
  
 È preferibile suddividere le procedure consigliate in due aree:  
  
-   Nelle informazioni seguenti sono descritte le procedure consigliate da implementare per tutte le topologie di replica:  
  
    -   Sviluppare e testare una strategia di backup e ripristino.  
  
    -   Creare lo script della topologia di replica.  
  
    -   Creare soglie e avvisi.  
  
    -   Monitorare la topologia di replica.  
  
    -   Stabilire dati di riferimento per le prestazioni e regolare la replica, se necessario.  
  
-   Negli argomenti seguenti sono riportate le procedure consigliate che è opportuno prendere in considerazione, sebbene potrebbero non essere richieste per la topologia in uso:  
  
    -   Convalidare i dati periodicamente.  
  
    -   Regolare i parametri dell'agente mediante i profili.  
  
    -   Regolare i periodi di memorizzazione della pubblicazione e della distribuzione.  
  
    -   Comprendere in che modo modificare le proprietà degli articoli e della pubblicazione se i requisiti dell'applicazione cambiano.  
  
    -   Comprendere in che modo apportare modifiche allo schema se i requisiti dell'applicazione cambiano.  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>Sviluppare e testare una strategia di backup e ripristino.  
 È consigliabile eseguire regolarmente il backup di tutti i database nonché testare periodicamente la capacità di ripristino di tali backup. Le stesse procedure sono consigliate anche per i database replicati. Di seguito sono elencati i database da sottoporre a backup regolarmente:  
  
-   Database di pubblicazione  
  
-   Database di distribuzione  
  
-   Database di sottoscrizione  
  
-   Database**msdb** e **master** nel server di pubblicazione, nel server di distribuzione e in tutti i Sottoscrittori  
  
 Il backup e il ripristino dei dati dei database replicati richiedono un'attenzione particolare. Per altre informazioni, vedere [Eseguire il backup e ripristino di database replicati](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
## <a name="script-the-replication-topology"></a>Creare lo script della topologia di replica  
 Gli script di tutti i componenti di replica inclusi in una topologia devono essere creati come parte di un piano di ripristino di emergenza. Gli script possono inoltre essere utilizzati per automatizzare attività ripetitive. Essi contengono le stored procedure di sistema [!INCLUDE[tsql](../../../includes/tsql-md.md)] necessarie per implementare i componenti di replica inseriti in uno script, ad esempio una pubblicazione o una sottoscrizione, Gli script possono essere creati mediante una procedura guidata, quale Creazione guidata nuova pubblicazione, o in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] dopo aver creato un componente. È possibile visualizzare, modificare ed eseguire lo script utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o **sqlcmd**. Gli script possono essere memorizzati con file di backup da utilizzare nel caso in cui sia necessario riconfigurare una topologia di replica. Per altre informazioni, vedere [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
 In caso di modifiche a una proprietà, è necessario riscrivere lo script di un componente. Se si utilizzano stored procedure personalizzate con la replica transazionale, è consigliabile archiviare una copia di ogni procedura con gli script, aggiornando la copia in caso di modifica della procedura. Le procedure vengono in genere aggiornate in seguito a modifiche dello schema o a nuove esigenze applicative. Per altre informazioni sulle procedure personalizzate, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>Stabilire dati di riferimento per le prestazioni e regolare la replica, se necessario  
 Prima di configurare la replica, è consigliabile acquisire familiarità con i fattori che influiscono sulle relative prestazioni:  
  
-   Hardware del server e della rete  
  
-   Progettazione del database  
  
-   Configurazione del server di distribuzione  
  
-   Progettazione e opzioni della pubblicazione  
  
-   Progettazione e utilizzo dei filtri  
  
-   Opzioni di sottoscrizione  
  
-   Opzioni per gli snapshot  
  
-   Parametri degli agenti  
  
-   Manutenzione  
  
 Dopo aver configurato la replica, è consigliabile sviluppare dati di riferimento per le prestazioni in modo da poter stabilire il comportamento della replica in presenza del carico di lavoro tipico delle applicazioni e della topologia in uso. Utilizzare Monitoraggio replica e Monitor di sistema per stabilire i valori tipici per le cinque dimensioni seguenti delle prestazioni della replica:  
  
-   Latenza: la quantità di tempo impiegato per la propagazione di una modifica dei dati tra i nodi di una topologia di replica.  
  
-   Velocità effettiva: quantità di attività di replica, espressa in comandi recapitati in un periodo di tempo specifico, che un sistema è in grado di sostenere nel tempo.  
  
-   Concorrenza: numero di processi di replica che possono essere eseguiti simultaneamente in un sistema.  
  
-   Durata della sincronizzazione: tempo necessario per il completamento di una sincronizzazione specifica.  
  
-   Utilizzo delle risorse: risorse hardware e di rete utilizzate per l'elaborazione della replica.  
  
 La latenza e la velocità effettiva interessano in particolare la replica transazionale, in quanto i sistemi basati su questo tipo di replica richiedono in genere una bassa latenza e una velocità effettiva elevata. La concorrenza e la durata della sincronizzazione sono più rilevanti per la replica di tipo merge in quanto i sistemi che si basano su questo tipo di replica sono spesso caratterizzati da un numero elevato di Sottoscrittori e un server di pubblicazione può stabilire un numero significativo di sincronizzazioni simultanee con tali Sottoscrittori.  
  
 Dopo aver stabilito i numeri di riferimento, impostare le soglie in Monitoraggio replica. Per altre informazioni, vedere [Impostare valori di soglia e avvisi in Monitoraggio replica](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md). In caso di problemi di prestazioni, è consigliabile leggere i suggerimenti riportati negli argomenti relativi al miglioramento delle prestazioni elencati sopra e apportare modifiche nelle aree che hanno determinato tali problemi.  
  
## <a name="create-thresholds-and-alerts"></a>Creare soglie e avvisi  
 Monitoraggio replica consente di impostare diverse soglie relative allo stato e alle prestazioni. È consigliabile impostare soglie appropriate per la topologia. Se si raggiunge una soglia, viene visualizzato un messaggio e, facoltativamente, è possibile inviare un avviso a un account di posta elettronica, un cercapersone o un altro dispositivo. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 Oltre agli avvisi che possono essere associati alle soglie di monitoraggio, la replica offre diversi avvisi predefiniti che rispondono alle azioni dell'agente di replica. Tali avvisi possono essere utilizzati da un amministratore per rimanere aggiornato sullo stato della topologia di replica. È consigliabile leggere l'argomento in cui sono descritti gli avvisi e utilizzare quelli che soddisfano le proprie esigenze amministrative. Se necessario, è inoltre possibile creare avvisi aggiuntivi. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
## <a name="monitor-the-replication-topology"></a>Monitorare la topologia di replica  
 Dopo aver impostato la topologia di replica e aver configurato soglie e avvisi, è consigliabile monitorare regolarmente la replica. Il monitoraggio di una topologia di replica rappresenta un aspetto essenziale della distribuzione di una replica. Dato che l'attività di replica viene distribuita, è fondamentale monitorarne l'attività e lo stato su tutti i computer interessati. Per monitorare la replica è possibile utilizzare gli strumenti seguenti:  
  
-   Monitoraggio replica è lo strumento più importante per il monitoraggio di una replica in quanto consente di controllare lo stato generale di una topologia di replica. Per altre informazioni, vedere [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] e gli oggetti RMO (Replication Management Objects) includono interfacce per il monitoraggio della replica. Per altre informazioni, vedere [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication.md).  
  
-   Il monitoraggio delle prestazioni della replica può essere effettuato anche mediante Monitor di sistema. Per altre informazioni, vedere [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="validate-data-periodically"></a>Convalidare i dati periodicamente  
 La procedura di convalida non è richiesta per la replica, ma è consigliabile eseguirla periodicamente per quella transazionale e di tipo merge. Tale procedura consente di verificare che i dati nel Sottoscrittore corrispondano ai dati nel server di pubblicazione. Una convalida riuscita indica che in quel particolare momento tutte le modifiche del server di pubblicazione sono state replicate nel Sottoscrittore (e dal Sottoscrittore nel server di pubblicazione se il Sottoscrittore supporta gli aggiornamenti) e che i due database sono sincronizzati.  
  
 È consigliabile eseguire la convalida in base alla pianificazione del backup del database di pubblicazione. Se, ad esempio, per il database di pubblicazione è stato impostato un backup completo ogni settimana, è possibile eseguire una convalida ogni settimana al termine del backup. Per altre informazioni, vedere [Convalidare i dati replicati](../../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>Utilizzare i profili agenti per modificare i parametri dell'agente, se necessario  
 I profili agenti consentono di impostare facilmente i parametri dell'agente di replica. È inoltre possibile specificare tali parametri dalla riga di comando dell'agente, sebbene sia generalmente più corretto utilizzare un profilo agente predefinito oppure creare un nuovo profilo se è necessario modificare il valore di un parametro. Se, ad esempio, si utilizza la replica di tipo merge e un Sottoscrittore passa da una connessione a banda larga a una connessione remota, provare a utilizzare il profilo a **collegamento lento** per l'agente di merge. Tale profilo utilizza un set di parametri che sono più adatti per il collegamento di comunicazione più lento. Per altre informazioni, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>Regolare i periodi di memorizzazione della pubblicazione e della distribuzione  
 La replica transazionale e la replica di tipo merge utilizzano periodi di memorizzazione per stabilire, rispettivamente, l'intervallo di tempo durante il quale le transazioni vengono memorizzate nel database di distribuzione e la frequenza con cui è necessario sincronizzare una sottoscrizione. Inizialmente è consigliabile utilizzare le impostazioni predefinite, monitorando la topologia per stabilire se è necessario modificarle. Nel caso ad esempio della replica di tipo merge, il periodo di memorizzazione della pubblicazione (pari a 14 giorni per impostazione predefinita) determina l'intervallo di tempo durante il quale i metadati vengono memorizzati in tabelle di sistema. Se le sottoscrizioni vengono sincronizzate entro cinque giorni, provare a regolare l'impostazione su un numero inferiore, in modo da ridurre i metadati ed eventualmente ottenere prestazioni migliori. Per altre informazioni, vedere [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>Comprendere in che modo modificare le pubblicazioni se i requisiti dell'applicazione cambiano  
 Dopo la creazione di una pubblicazione, potrebbe essere necessario aggiungere o eliminare articoli oppure modificare le proprietà della pubblicazione e degli articoli. Dopo la creazione di una pubblicazione è consentita la maggiore parte delle modifiche. In alcuni casi, tuttavia, è necessario generare un nuovo snapshot per una pubblicazione e/o reinizializzare le relative sottoscrizioni. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) e [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>Comprendere in che modo apportare modifiche allo schema se i requisiti dell'applicazione cambiano  
 In molti casi le modifiche apportate allo schema sono richieste quando un'applicazione viene messa in produzione. In una topologia di replica tali modifiche devono spesso essere propagate a tutti i Sottoscrittori. La replica supporta una vasta gamma di modifiche dello schema negli oggetti pubblicati. Quando si apporta una delle modifiche di schema seguenti nell'oggetto pubblicato appropriato in un server di pubblicazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la modifica viene propagata per impostazione predefinita a tutti i Sottoscrittori [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Domande frequenti sull'amministrazione della replica](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
  
