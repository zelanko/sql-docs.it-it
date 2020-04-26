---
title: Monitorare la replica a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 949c8585b3886d0d3f422e76d031b390d248e9a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62667247"
---
# <a name="programmatically-monitor-replication"></a>Monitoraggio della replica a livello di programmazione
  Monitoraggio replica è uno strumento grafico che consente di monitorare una topologia di replica. È possibile accedere agli stessi dati di monitoraggio a livello di programmazione utilizzando le stored procedure di replica [!INCLUDE[tsql](../../../includes/tsql-md.md)] o gli oggetti RMO (Replication Management Objects). Tali oggetti consentono di programmare le attività seguenti:  
  
-   Monitoraggio dello stato dei server di pubblicazione, delle pubblicazioni e delle sottoscrizioni.  
  
-   Monitoraggio delle sessioni dell'agente di merge in uno o più Sottoscrittori.  
  
-   Monitoraggio dei comandi transazionali in attesa di essere applicati a uno o più Sottoscrittori.  
  
-   Definizione delle metriche di soglia che determinano la necessità di un intervento per una pubblicazione.  
  
-   Monitoraggio dello stato dei token di traccia.  
  
 **Contenuto dell'argomento:**  
  
 [Transact-SQL](#Tsql)  
  
 [Oggetti RMO (Replication Management Objects)](#RMO)  
  
##  <a name="transact-sql"></a><a name="Tsql"></a> Transact-SQL  
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>Per monitorare i server di pubblicazione, le pubblicazioni e le sottoscrizioni dal database di distribuzione  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelppublisher](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql). Vengono restituite le informazioni di monitoraggio per tutti i server di pubblicazione che utilizzano il server di distribuzione. Per limitare il set di risultati a un solo server di **@publisher**pubblicazione, specificare.  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelppublication](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql). Vengono restituite le informazioni di monitoraggio per tutte le pubblicazioni che utilizzano il server di distribuzione. Per limitare il set di risultati a un solo server di pubblicazione, a una sola pubblicazione **@publisher**o **@publication**a un **@publisher_db**solo database pubblicato, specificare rispettivamente, o.  
  
3.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelpsubscription](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql). Vengono restituite le informazioni di monitoraggio per tutte le sottoscrizioni che utilizzano il server di distribuzione. Per limitare il set di risultati alle sottoscrizioni appartenenti a un solo server di pubblicazione, a una **@publisher**sola **@publication**pubblicazione o **@publisher_db**a un solo database pubblicato, specificare rispettivamente, o.  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>Per monitorare i comandi transazionali in attesa di essere applicati al Sottoscrittore  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorsubscriptionpendingcmds](/sql/relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql). Vengono restituite le informazioni di monitoraggio per tutti i comandi in sospeso per tutte le sottoscrizioni che utilizzano il server di distribuzione. Per limitare il set di risultati ai comandi in sospeso per le sottoscrizioni appartenenti a un solo server di pubblicazione, a un Sottoscrittore **@publication**, a **@publisher_db**una pubblicazione o a un database pubblicato, specificare **@publisher**rispettivamente, **@subscriber**, o.  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>Per monitorare le modifiche di tipo merge in attesa di essere caricate o scaricate  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_showpendingchanges](/sql/relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql). Viene restituito un set di risultati in cui sono indicate le informazioni sulle modifiche in attesa di essere replicate nei Sottoscrittori. Per limitare il set di risultati alle modifiche che appartengono a una sola pubblicazione o a un **@publication** solo **@article**articolo, specificare rispettivamente o.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_showpendingchanges](/sql/relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql). Viene restituito un set di risultati in cui sono indicate le informazioni sulle modifiche in attesa di essere replicate nel server di pubblicazione. Per limitare il set di risultati alle modifiche che appartengono a una sola pubblicazione o a un **@publication** solo **@article**articolo, specificare rispettivamente o.  
  
#### <a name="to-monitor-merge-agent-sessions"></a>Per monitorare sessioni dell'agente di merge  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelpmergesession](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql). Vengono restituite le informazioni di monitoraggio, **Session_id**incluso, relative a tutte le sessioni dell'agente di merge per tutte le sottoscrizioni che utilizzano il server di distribuzione. È anche possibile ottenere il valore **Session_id** eseguendo una query sulla tabella di sistema [MSmerge_sessions](/sql/relational-databases/system-tables/msmerge-sessions-transact-sql) .  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelpmergesessiondetail](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql). Specificare il valore **Session_id** indicato al passaggio 1 per **@session_id**. Vengono visualizzate informazioni di monitoraggio dettagliate sulla sessione.  
  
3.  Ripetere il passaggio 2 per ciascuna sessione desiderata.  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>Per monitorare le sessioni dell'agente di merge per le sottoscrizioni pull dal Sottoscrittore  
  
1.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_replmonitorhelpmergesession](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql). Per una determinata sottoscrizione, specificare **@publisher**, **@publication**e il nome del database di pubblicazione per **@publisher_db**. Vengono restituite le informazioni di monitoraggio per le ultime cinque sessioni dell'agente di merge della sottoscrizione. Tenere presente il valore di **Session_id** per le sessioni desiderate nel set di risultati.  
  
2.  Nel database di sottoscrizione del Sottoscrittore eseguire [sp_replmonitorhelpmergesession](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql). Specificare il valore **Session_id** indicato al passaggio 1 per **@session_id**. Vengono visualizzate informazioni di monitoraggio dettagliate sulla sessione.  
  
3.  Ripetere il passaggio 2 per ciascuna sessione desiderata.  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>Per visualizzare e modificare le misurazioni del valore soglia di monitoraggio per una pubblicazione  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorhelppublicationthresholds](/sql/relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql). Vengono restituiti i valore soglia di monitoraggio impostati per tutte le pubblicazioni che utilizzano il server di distribuzione. Per limitare il set di risultati al monitoraggio delle soglie per le pubblicazioni appartenenti a un singolo server di pubblicazione o a un solo **@publisher**database **@publisher_db**pubblicato o **@publication**a una sola pubblicazione, specificare rispettivamente, o. Tenere presente il valore di **Metric_id** per i valore soglia da modificare. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql). Specificare i parametri seguenti, in base alle esigenze:  
  
    -   Il valore **Metric_id** ottenuto nel passaggio 1 per **@metric_id**.  
  
    -   Nuovo valore per la metrica di soglia di monitoraggio **@value**per.  
  
    -   Un valore pari a **1** per **@shouldalert** se è necessaria la registrazione di un avviso al raggiungimento del valore soglia specificato o un valore pari a **0** se la registrazione dell'avviso non è necessaria.  
  
    -   Un valore pari a **1** per **@mode** per abilitare la metrica di soglia di monitoraggio o un valore pari a **2** per disabilitarla.  
  
##  <a name="replication-management-objects-rmo"></a><a name="RMO"></a> Oggetti RMO (Replication Management Objects)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>Per monitorare una sottoscrizione di una pubblicazione di tipo merge nel Sottoscrittore  
  
1.  Creare una connessione al Sottoscrittore tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> e impostare le proprietà <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>e <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> per la sottoscrizione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1.  
  
3.  Chiamare uno dei metodi indicati di seguito per ottenere informazioni sulle sessioni dell'agente di merge per la sottoscrizione.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> : restituisce una matrice di oggetti <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con informazioni sulle ultime cinque sessioni dell'agente di merge al massimo. Tenere presente il valore della proprietà <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> per le sessioni desiderate.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> : restituisce una matrice di oggetti <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con informazioni sulle sessioni dell'agente di merge che hanno avuto luogo durante il numero passato di ore specificato come parametro *hours* (ultime cinque sessioni al massimo). Tenere presente il valore della proprietà <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> per le sessioni desiderate.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> : restituisce un oggetto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con informazioni sull'ultima sessione dell'agente di merge. Tenere presente il valore della proprietà <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> per questa sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> : restituisce un oggetto <xref:System.Data.DataSet> con informazioni sulle ultime cinque sessioni dell'agente di merge al massimo, una in ciascuna riga. Tenere presente il valore della colonna **Session_id** per le sessioni desiderate.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> : restituisce un oggetto <xref:System.Data.DataRow> con informazioni sull'ultima sessione dell'agente di merge. Tenere presente il valore della colonna **Session_id** per questa sessione.  
  
4.  (Facoltativo) Chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> per aggiornare i dati per l'oggetto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> passato come *mss,* o chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> per aggiornare i dati nell'oggetto <xref:System.Data.DataRow> passato come *drRefresh*.  
  
5.  Utilizzando l'ID sessione ottenuto nel passaggio 3, chiamare uno dei metodi indicati di seguito per ottenere informazioni sui dettagli di una determinata sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A>: restituisce una matrice di <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> oggetti per l'oggetto *SessionID*fornito.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A>: restituisce un <xref:System.Data.DataSet> oggetto con le informazioni per l'oggetto *SessionID*specificato.  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>Per monitorare le proprietà di replica per tutte le pubblicazioni in un server di distribuzione  
  
1.  Creare una connessione al server di distribuzione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.ReplicationMonitor>.  
  
3.  Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1.  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto.  
  
5.  Eseguire uno o più metodi riportati di seguito per ottenere le informazioni di replica per tutti i server di pubblicazione che utilizzano il server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli agenti di distribuzione nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sugli errori archiviati nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli agenti di lettura log nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli agenti di merge nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli altri agenti di replica nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti i server di pubblicazione nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> : restituisce un oggetto <xref:System.Data.DataSet> che restituisce i server di pubblicazione che utilizzano il server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli agenti di lettura coda nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene dettagli sull'agente di lettura coda specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni di sessione relative all'agente di lettura coda specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti gli agenti snapshot nel server di distribuzione.  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>Per monitorare le proprietà della pubblicazione per un server di pubblicazione specifico nel server di distribuzione  
  
1.  Creare una connessione al server di distribuzione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Recuperare un oggetto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> mediante uno dei modi indicati di seguito.  
  
    -   Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.PublisherMonitor>. Impostare la proprietà <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> per il server di pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1. Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, il nome del server di pubblicazione è definito in modo non corretto o la pubblicazione non esiste.  
  
    -   Utilizzare l'oggetto <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> a cui si accede mediante la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> di un oggetto <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> esistente.  
  
3.  Eseguire uno o più metodi riportati di seguito per ottenere le informazioni di replica per tutte le pubblicazioni appartenenti al server di pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene dettagli sull'agente di distribuzione specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni di sessione relative all'agente di distribuzione specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni del record di errori relative all'errore specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene dettagli sull'agente di lettura log specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni di sessione relative all'agente di lettura log specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene dettagli sull'agente di merge specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene ulteriori dettagli sull'agente di merge specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni di sessione relative all'agente di merge specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene ulteriori informazioni di sessione relative all'agente di merge specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutte le pubblicazioni nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene ulteriori informazioni su tutte le pubblicazioni nel server di distribuzione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene dettagli sull'agente snapshot specificato e sulla sessione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni di sessione relative all'agente snapshot specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutte le sottoscrizioni delle pubblicazioni nel server di distribuzione.  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>Per monitorare le proprietà di una pubblicazione specifica nel server di distribuzione  
  
1.  Creare una connessione al server di distribuzione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Recuperare un oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> mediante uno dei modi indicati di seguito.  
  
    -   Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1. Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono definite in modo non corretto o la pubblicazione non esiste.  
  
    -   Utilizzare l'oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> a cui si accede mediante la proprietà <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> di un oggetto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> esistente.  
  
3.  Eseguire uno o più metodi riportati di seguito per ottenere informazioni su questa pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene record di errori relativi all'errore specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sull'agente di lettura log della pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sui valore soglia degli avvisi di monitoraggio impostati per la pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sull'agente di lettura coda utilizzato dalla pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sull'agente snapshot della pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sulle sottoscrizioni della pubblicazione.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> - restituisce un oggetto <xref:System.Data.DataSet> che contiene ulteriori informazioni sulle sottoscrizioni della pubblicazione in base all'oggetto <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni sulla latenza per il token di traccia specificato.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> : restituisce un oggetto <xref:System.Data.DataSet> che contiene informazioni su tutti i token di traccia inseriti nella pubblicazione.  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>Per monitorare i comandi transazionali in attesa di essere applicati al Sottoscrittore  
  
1.  Creare una connessione al server di distribuzione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Recuperare un oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> mediante uno dei modi indicati di seguito.  
  
    -   Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1. Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono definite in modo non corretto o la pubblicazione non esiste.  
  
    -   Utilizzare l'oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> a cui si accede mediante la proprietà <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> di un oggetto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> esistente.  
  
3.  Eseguire il metodo <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> che restituisce un oggetto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> .  
  
4.  Utilizzare le proprietà dell'oggetto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> per determinare il numero stimato di comandi in sospeso e il tempo necessario per completare il recapito di tali comandi.  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>Per impostare i valore soglia degli avvisi di monitoraggio per una pubblicazione  
  
1.  Creare una connessione al server di distribuzione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Recuperare un oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> mediante uno dei modi indicati di seguito.  
  
    -   Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Impostare le proprietà <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> per la pubblicazione, quindi impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creato nel passaggio 1. Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono definite in modo non corretto o la pubblicazione non esiste.  
  
    -   Utilizzare l'oggetto <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> a cui si accede mediante la proprietà <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> di un oggetto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> esistente.  
  
3.  Eseguire il metodo <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> . Tenere presenti le impostazioni dei valore soglia correnti nell'oggetto <xref:System.Collections.ArrayList> restituito degli oggetti <xref:Microsoft.SqlServer.Replication.MonitorThreshold> .  
  
4.  Eseguire il metodo <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> . Passare i parametri indicati di seguito.  
  
    -   *metricID* : un valore <xref:System.Int32> che rappresenta la misurazione del valore soglia di monitoraggio nella tabella riportata di seguito.  
  
        |valore|Descrizione|  
        |-----------|-----------------|  
        |1|`expiration`: esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni di pubblicazioni transazionali.|  
        |2|`latency`: esegue il monitoraggio delle prestazioni delle sottoscrizioni di pubblicazioni transazionali.|  
        |4|`mergeexpiration`: esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni di pubblicazioni di tipo merge.|  
        |5|`mergeslowrunduration`: esegue il monitoraggio della durata delle sincronizzazioni di tipo merge attraverso connessioni remote a larghezza di banda ridotta.|  
        |6|`mergefastrunduration`: esegue il monitoraggio della durata delle sincronizzazioni di tipo merge attraverso connessioni LAN ad alta larghezza di banda.|  
        |7|`mergefastrunspeed` - esegue il monitoraggio della frequenza delle sincronizzazioni di tipo merge su connessioni tramite rete locale (LAN) a larghezza di banda elevata.|  
        |8|`mergeslowrunspeed`: esegue il monitoraggio della velocità delle sincronizzazioni di tipo merge attraverso connessioni remote a larghezza di banda ridotta.|  
  
    -   *enable* - <xref:System.Boolean> che indica se la misurazione è attivata per la pubblicazione.  
  
    -   *thresholdValue* : valore integer che imposta il valore soglia.  
  
    -   *shouldAlert* - Integer che indica se il valore soglia deve generare un avviso.  
  
  
