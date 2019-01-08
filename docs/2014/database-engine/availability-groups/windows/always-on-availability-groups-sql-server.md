---
title: Gruppi di disponibilità Always On (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f1e86eec76a94a3858ede48fc0fb1b0703de4508
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356248"
---
# <a name="always-on-availability-groups-sql-server"></a>Gruppi di disponibilità Always On (SQL Server)
  La funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è una soluzione di disponibilità elevata e recupero di emergenza che offre un'alternativa di livello enterprise al mirroring del database. Introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aumenta la disponibilità di un set di database utente per un'azienda. Un *gruppo di disponibilità* supporta un ambiente di failover per un set discreto di database utente, noti come *database di disponibilità*, su cui si verifica il failover. Un gruppo di disponibilità supporta un set di database primari di lettura e scrittura e da uno a otto set di database secondari corrispondenti. Facoltativamente, i database secondari possono essere resi disponibili per l'accesso di sola lettura e/o alcune operazioni di backup.  
  
 Per un gruppo di disponibilità il failover si verifica al livello di una replica di disponibilità. I failover non sono dovuti a database ritenuti sospetti in seguito a una perdita di un file di dati, all'eliminazione di un database o al danneggiamento di un log delle transazioni.  
  
  
##  <a name="Benefits"></a> Vantaggi  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è incluso un ampio set di opzioni con cui è possibile migliorare la disponibilità del database e che consentono un uso ottimale delle risorse. I componenti chiave sono i seguenti:  
  
-   Supporta fino a nove repliche di disponibilità. Una *replica di disponibilità* è la creazione di un'istanza di un gruppo di disponibilità ospitata da un'istanza specifica di SQL Server e che mantiene una copia locale di ogni database di disponibilità che appartiene al gruppo di disponibilità. Ogni gruppo di disponibilità supporta una replica primaria e fino a otto repliche secondarie. Per altre informazioni, vedere [Panoramica di Gruppi di disponibilità Always On &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Ogni replica di disponibilità deve risiedere su un nodo diverso di un singolo cluster WSFC (Windows Server Failover Clustering). Per altre informazioni sui prerequisiti, restrizioni e consigli per gruppi di disponibilità, vedere [prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn; SQL Server. ](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Supporta modalità di disponibilità alternative, come segue:  
  
    -   *Modalità commit asincrono*. La modalità di disponibilità è una soluzione di recupero di emergenza che offre risultati ottimali quando le repliche di disponibilità vengono distribuite a distanze considerevoli.  
  
    -   *Modalità commit sincrono*. La modalità di disponibilità privilegia la disponibilità elevata e la protezione dei dati rispetto alle prestazioni, aumentando tuttavia la latenza delle transazioni. Un determinato gruppo di disponibilità è in grado di supportare fino a tre repliche di disponibilità con commit sincrono, inclusa la replica primaria corrente.  
  
     Per altre informazioni, vedere [ modalità di disponibilità; Gruppi di disponibilità; Always On ](availability-modes-always-on-availability-groups.md).  
  
-   Supporta molti formati di failover del gruppo di disponibilità: failover automatico, failover manuale pianificato (in genere definito semplicemente "failover manuale") e failover manuale forzato (in genere definito semplicemente "failover forzato"). Per altre informazioni, vedere [Failover e modalità di Failover; Gruppi di disponibilità; Always On ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Permette di configurare una determinata replica di disponibilità per supportare una o entrambe le seguenti funzionalità delle repliche secondarie attive:  
  
    -   Accesso alla connessione in sola lettura che permette connessioni in sola lettura alla replica per accedere e leggere i relativi database quando viene eseguita come replica secondaria. Per altre informazioni, vedere [repliche secondarie attive: Repliche secondarie leggibili. Gruppi di disponibilità Always On](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
    -   Esecuzione di operazioni di backup sui relativi database quando viene eseguita come replica secondaria. Per altre informazioni, vedere [repliche secondarie attive: Backup su repliche secondarie](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
     L'uso delle funzionalità secondarie attive migliora l'efficienza IT e riduce i costi tramite un migliore uso delle risorse dell'hardware secondario. Inoltre, la ripartizione delle applicazioni con finalità di lettura e dei processi di backup alle repliche secondarie permette di migliorare le prestazioni sulla replica primaria.  
  
-   Supporta un listener del gruppo di disponibilità per ogni gruppo di disponibilità. Un *listener del gruppo di disponibilità* è un nome del server a cui i client possono connettersi per accedere a un database in una replica primaria o secondaria di un gruppo di disponibilità AlwaysOn. I listener del gruppo di disponibilità indirizzano le connessioni in ingresso alla replica primaria o a una replica secondaria in sola lettura. Il listener permette un failover rapido dell'applicazione dopo il failover del gruppo di disponibilità. Per altre informazioni, vedere [listener del gruppo di disponibilità, connettività Client e Failover dell'applicazione; SQL Server. ](../../listeners-client-connectivity-application-failover.md).  
  
-   Supporta criteri di failover flessibili per un maggiore controllo del failover del gruppo di disponibilità. Per altre informazioni, vedere [Failover e modalità di Failover; Gruppi di disponibilità; Always On ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   Supporta il ripristino automatico della pagina per la protezione da danneggiamenti di pagina. Per altre informazioni, vedere [correzione automatica della pagina &#40;per i gruppi di disponibilità e il mirroring del Database;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md).  
  
-   Supporta crittografia e compressione, che forniscono il trasporto sicuro a prestazioni elevate.  
  
-   Fornisce un set integrato di strumenti per semplificare la distribuzione e la gestione dei gruppi di disponibilità, tra cui:  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] per la creazione e la gestione di gruppi di disponibilità. Per altre informazioni, vedere [panoramica delle istruzioni Transact-SQL per gruppo di disponibilità AlwaysOn; SQL Server. ](transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , come segue:  
  
        -   La [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] permette di creare e configurare un gruppo di disponibilità. In alcuni ambienti, questa procedura guidata prepara automaticamente i database secondari e avvia la sincronizzazione dei dati per ognuno di essi. Per altre informazioni, vedere [usare la finestra di dialogo di gruppo di disponibilità nuovo; SQL Server Management Studio. ](use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   La [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] aggiunge uno o più database primari a un gruppo di disponibilità esistente. In alcuni ambienti, questa procedura guidata prepara automaticamente i database secondari e avvia la sincronizzazione dei dati per ognuno di essi. Per altre informazioni, vedere [Usare la procedura guidata Aggiungi database a gruppo di disponibilità (SQL Server)](availability-group-add-database-to-group-wizard.md).  
  
        -   La [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] aggiunge una o più repliche secondarie a un gruppo di disponibilità esistente. In alcuni ambienti, questa procedura guidata prepara automaticamente i database secondari e avvia la sincronizzazione dei dati per ognuno di essi. Per altre informazioni, vedere [usare Aggiungi Replica a Creazione guidata gruppo di disponibilità; SQL Server Management Studio. ](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   La [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)] avvia un failover manuale su un gruppo di disponibilità. A seconda della configurazione e dello stato della replica secondaria specificata come destinazione del failover, la procedura guidata può eseguire un failover pianificato o un failover manuale forzato. Per altre informazioni, vedere [usano l'esito negativo su guidata gruppo di disponibilità; SQL Server Management Studio. ](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] esegue il monitoraggio dei gruppi di disponibilità AlwaysOn, delle repliche di disponibilità e dei database di disponibilità e valuta risultati per i criteri AlwaysOn. Per altre informazioni, vedere [usare il AlwaysOn Dashboard; SQL Server Management Studio. ](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   Nel riquadro Dettagli Esplora oggetti sono visualizzate informazioni di base sui gruppi di disponibilità esistenti. Per altre informazioni, vedere [utilizzare dettagli Esplora oggetti al gruppo di disponibilità di monitoraggio; SQL Server Management Studio. ](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Cmdlet di PowerShell. Per altre informazioni, vedere [panoramica dei cmdlet di PowerShell per gruppi di disponibilità AlwaysOn; SQL Server; ](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="TermsAndDefinitions"></a> Termini e definizioni  
 gruppo di disponibilità  
 Contenitore per un set di database, i *database di disponibilità*, su cui si verifica il failover.  
  
 database di disponibilità  
 Database che appartiene a un gruppo di disponibilità. Per ogni database di disponibilità, il gruppo di disponibilità gestisce una sola copia di lettura e scrittura (il *database primario*) e da una a otto copie di sola lettura (*database secondari*).  
  
 database primario  
 Copia di lettura e scrittura di un database di disponibilità.  
  
 database secondario  
 Copia di sola lettura di un database di disponibilità.  
  
 replica di disponibilità  
 Istanza di un gruppo di disponibilità ospitata da un'istanza specifica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che mantiene una copia locale di ogni database di disponibilità che appartiene al gruppo di disponibilità. Sono disponibili due tipi di replica di disponibilità: una *replica primaria* e da una a otto *repliche secondarie*.  
  
 replica primaria  
 Replica di disponibilità che rende disponibili i database primari per le connessioni in lettura e scrittura dai client e invia i record del log delle transazioni per ogni database primario a ogni replica secondaria.  
  
 replica secondaria  
 Replica di disponibilità che mantiene una copia secondaria di ogni database di disponibilità e che rappresenta la destinazione potenziale del failover per il gruppo di disponibilità. Facoltativamente, una replica secondaria può supportare l'accesso in sola lettura ai database secondari creando backup sui database secondari.  
  
 listener del gruppo di disponibilità  
 Nome del server a cui i client possono connettersi per accedere a un database in una replica primaria o secondaria di un gruppo di disponibilità Always On. I listener del gruppo di disponibilità indirizzano le connessioni in ingresso alla replica primaria o a una replica secondaria in sola lettura.  
  
> [!NOTE]  
>  Per altre informazioni, vedere [Panoramica di gruppi di disponibilità AlwaysOn; SQL Server; ](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="Interoperability"></a> Interoperabilità e coesistenza con altre funzionalità del motore di database  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] può essere usato con le funzionalità o i componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]seguenti:  
  
-   [Informazioni su Change Data Capture; SQL Server.](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [Informazioni sul rilevamento delle modifiche; SQL Server;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [Database indipendenti](../../../relational-databases/databases/contained-databases.md)  
  
-   [Crittografia del database](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [Snapshot di database](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [Log shipping](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [Archivio BLOB remoto (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [Replica](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server Agent](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  Per informazioni sulle restrizioni e limitazioni per l'uso con altre funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [gruppi di disponibilità AlwaysOn: Interoperabilità; SQL Server. ](always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Introduzione a Always nei gruppi di disponibilità. SQL Server.](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [SQL Server Always On Team blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Video:**  
  
     [Microsoft SQL Server nome in codice "Denali" Always On Series, Part 1: Introduzione della soluzione di disponibilità elevata di prossima generazione](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server nome in codice "Denali" Always On Series, Part 2: Creazione di una soluzione di disponibilità elevata critica tramite Alwasyon](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper:**  
  
     [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza)](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità; Always On SQL Server.](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Configurazione di un'istanza del Server per gruppi di disponibilità; Always On SQL Server.](always-on-availability-groups-sql-server.md)   
 [La creazione e la configurazione di gruppi di disponibilità. SQL Server.](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Amministrazione di un gruppo di disponibilità; SQL Server.](administration-of-an-availability-group-sql-server.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Panoramica delle istruzioni Transact-SQL per i gruppi di disponibilità; Always On SQL Server.](transact-sql-statements-for-always-on-availability-groups.md)   
 [Panoramica dei cmdlet di PowerShell per gruppi di disponibilità AlwaysOn. SQL Server.](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
