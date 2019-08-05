---
title: Replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e158860b786a7612a31acd629a7b5d5deff203f3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769482"
---
# <a name="sql-server-replication"></a>Replica di SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La replica è costituita da un set di tecnologie per la copia e la distribuzione di dati e oggetti di database da un database a un altro e la successiva sincronizzazione dei database in modo che risultino consistenti. Usare la replica per distribuire dati a diverse posizioni e a utenti remoti o mobili tramite reti locali e WAN, connessioni remote, connessioni wireless e Internet.  
  
 La replica transazionale viene in genere utilizzata negli scenari server-server con esigenze di elevata velocità effettiva, inclusi il miglioramento delle caratteristiche di scalabilità e disponibilità, funzionalità di data warehouse e di creazione di report, integrazione di dati da più siti, integrazione di dati eterogenei e ripartizione del carico di lavoro dell'elaborazione batch. La replica di tipo merge è principalmente progettata per le applicazioni mobili o server distribuite con possibili conflitti di dati. Tra gli scenari comuni sono inclusi lo scambio di dati con utenti mobili, applicazioni POS e integrazione di dati da più siti. La replica snapshot viene utilizzata per fornire il set di dati iniziale per la replica di tipo merge o transazionale, nonché nel caso sia necessario un aggiornamento completo dei dati. Con questi tre tipi di replica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] costituisce un sistema potente e flessibile per la sincronizzazione dei dati aziendali. La replica in SQLCE 3.5 e SQLCE 4.0 è supportata sia in [!INCLUDE[win8srv](../../includes/win8srv-md.md)] sia in [!INCLUDE[win8](../../includes/win8-md.md)].  

 In alternativa alla replica, è possibile sincronizzare i database utilizzando Microsoft Sync Framework. Sync Framework include componenti e una API intuitiva e flessibile che facilitano la sincronizzazione fra i database di SQL Server, SQL Server Express, SQL Server Compact e SQL Azure. Sync Framework include anche classi che possono essere adattate per la sincronizzazione tra un database di SQL Server e un qualsiasi altro database compatibile con ADO.NET. Per la documentazione dettagliata dei componenti per la sincronizzazione di Sync Framework, vedere [Sincronizzazione di database](https://go.microsoft.com/fwlink/?LinkId=209079). Per una panoramica su Sync Framework, vedere la pagina relativa al [centro per sviluppatori di Microsoft Sync Framework](https://go.microsoft.com/fwlink/?LinkId=209078). Per un confronto tra Sync Framework e la replica di tipo merge, vedere [Panoramica sulla sincronizzazione di database](https://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  

## <a name="whats-new"></a>Novità 
- In SQL Server 2017 non sono state introdotte funzionalità significative nuove per la replica di SQL Server. 
- In SQL Server 2016 non sono state introdotte funzionalità significative nuove per la replica di SQL Server. 

Per informazioni sulla compatibilità con le versioni precedenti, vedere [Compatibilità con le versioni precedenti della replica](replication-backward-compatibility.md) 


 ## <a name="replication-security"></a>Sicurezza della replica
  
-   [Visualizzare e modificare le impostazioni di sicurezza della replica](security/view-and-modify-replication-security-settings.md)  
-   [Gestire gli account nell'elenco di accesso alla pubblicazione](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>Pubblicazione e distribuzione  
  
-   [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)   
-   [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
-   [Disabilitare la pubblicazione e la distribuzione](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>Pubblicazioni e articoli 
  
-   [Create a Publication](publish/create-a-publication.md)    
-   [Define an Article](publish/define-an-article.md)   
-   [Visualizzare e modificare le proprietà della pubblicazione](publish/view-and-modify-publication-properties.md)   
-   [Visualizzare e modificare le proprietà degli articoli](publish/view-and-modify-article-properties.md)    
-   [Eliminare una pubblicazione](publish/delete-a-publication.md)   
-   [Eliminare un articolo](publish/delete-an-article.md)    
-   [Creare una pubblicazione da un database Oracle](publish/create-a-publication-from-an-oracle-database.md)   
-   [Impostare il periodo di scadenza per le sottoscrizioni](publish/set-the-expiration-period-for-subscriptions.md)  
-   [Specificare le opzioni dello schema](publish/specify-schema-options.md)  
-   [Replicare le modifiche dello schema](publish/replicate-schema-changes.md)    
-   [Gestire le colonne Identity](publish/manage-identity-columns.md)   
-   [Impostare il livello di compatibilità per le pubblicazioni di tipo merge](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opzioni per gli snapshot  
  
-   [Configurare le proprietà dello snapshot](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [Recapitare uno snapshot tramite FTP](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>Filtrare i dati  
  
-   [Definire e modificare un filtro colonne](publish/define-and-modify-a-column-filter.md)    
-   [Definire e modificare un filtro di riga statico](publish/define-and-modify-a-static-row-filter.md)    
-   [Definire e modificare un filtro di riga con parametri per un articolo di merge](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [Ottimizzare i filtri di riga con parametri](publish/optimize-parameterized-row-filters.md)    
-   [Definire e modificare un filtro di join tra articoli di merge](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opzioni per la replica transazionale  
  
-   [Impostare il metodo di propagazione per le modifiche ai dati negli articoli transazionali](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [Abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opzioni per la replica di tipo merge  
  
-   [Definire una relazione tra record logici degli articoli di tabelle di merge](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [Specificare le proprietà della replica di tipo merge](merge/specify-merge-replication-properties.md)    
-   [Specificare un sistema di risoluzione dei conflitti dell'articolo di merge](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>Gestire le sottoscrizioni  
  
-   [Create a Pull Subscription](create-a-pull-subscription.md)    
-   [Visualizzare e modificare le proprietà delle sottoscrizioni pull](view-and-modify-pull-subscription-properties.md)    
-   [Eliminare una sottoscrizione pull](delete-a-pull-subscription.md)    
-   [Creare una sottoscrizione push](create-a-push-subscription.md)   
-   [Visualizzare e modificare le proprietà delle sottoscrizioni push](view-and-modify-push-subscription-properties.md)   
-   [Eliminare una sottoscrizione push](delete-a-push-subscription.md)   
-   [Specificare le pianificazioni della sincronizzazione](specify-synchronization-schedules.md)    
-   [Creare una sottoscrizione aggiornabile di una pubblicazione transazionale](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [Creare una sottoscrizione per un Sottoscrittore non SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>Sincronizzare le sottoscrizioni  
  
-   [Creazione e applicazione dello snapshot iniziale](create-and-apply-the-initial-snapshot.md)   
-   [Creare uno snapshot per una pubblicazione di tipo merge con filtri con parametri](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [Inizializzare una sottoscrizione transazionale da un backup &#40;programmazione Transact-SQL della replica&#41;](initialize-a-transactional-subscription-from-a-backup.md)    
-   [Inizializzare manualmente una sottoscrizione](initialize-a-subscription-manually.md)    
-   [Sincronizzazione di una sottoscrizione pull](synchronize-a-pull-subscription.md)    
-   [Sincronizzazione di una sottoscrizione push](synchronize-a-push-subscription.md)   
-   [Reinizializzare una sottoscrizione](reinitialize-a-subscription.md)    
-   [Eseguire script durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [Implementare un gestore della logica di business per un articolo di merge](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [Eseguire il debug di un gestore della logica di business &#40;programmazione della replica&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [Controllare il comportamento di trigger e vincoli durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administration"></a>Amministrazione 
  
-   [Usare i profili agenti di replica](agents/work-with-replication-agent-profiles.md)   
-   [Convalidare i dati nel sottoscrittore](validate-data-at-the-subscriber.md)    
-   [Gestire le partizioni di una pubblicazione di tipo merge con filtri con parametri](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [Caricamento bulk dei dati nelle tabelle in una pubblicazione di tipo merge &#40;programmazione Transact-SQL della replica&#41;](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [Eseguire la pulizia dei metadati di merge &#40;programmazione Transact-SQL della replica&#41;](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [Eseguire un aggiornamento fittizio per un articolo di merge &#40;programmazione Transact-SQL della replica&#41;](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [Visualizzare comandi replicati e altre informazioni nel database di distribuzione &#40;programmazione Transact-SQL della replica&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Abilitare backup coordinati per la replica transazionale &#40;programmazione Transact-SQL della replica&#41;](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [Amministrare una topologia peer-to-peer &#40;programmazione Transact-SQL della replica&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [Mettere una topologia di replica in stato di inattività &#40;programmazione Transact-SQL della replica&#41;](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [Configurare il processo del set di transazioni per un server di pubblicazione Oracle &#40;programmazione Transact-SQL della replica&#41;](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [Aggiornare gli script di replica &#40;programmazione Transact-SQL della replica&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>Monitoraggio
  
-   [Consentire a utenti non amministratori di usare Monitoraggio replica](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [Monitorare la replica a livello di programmazione](monitor/programmatically-monitor-replication.md)    
-   [Visualizzare comandi replicati e altre informazioni nel database di distribuzione &#40;programmazione Transact-SQL della replica&#41;](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](view-conflict-information-for-merge-publications.md) 
-   [Misurare la latenza e convalidare le connessioni per la replica transazionale](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
