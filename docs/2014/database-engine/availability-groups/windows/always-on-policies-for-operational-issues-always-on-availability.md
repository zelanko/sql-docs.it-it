---
title: Criteri di Always On per problemi operativi con i gruppi di disponibilità Always On (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 090ad6a9651a01532af528f5f78316eeadb9798d
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922009"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>Criteri Always On per problemi operativi con gruppi di disponibilità Always On (SQL Server)
  Il modello di integrità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] consente di valutare un set di criteri di gestione basata su criteri (PBM, Policy Based Management) predefiniti. Questi criteri possono essere utilizzati per la visualizzazione dell'integrità di un gruppo di disponibilità, nonché delle repliche e dei database di disponibilità relativi in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
  
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a>Termini e definizioni  
 Criteri predefiniti AlwaysOn  
 Set di criteri predefiniti che consentono a un amministratore del database di verificare la conformità di un gruppo di disponibilità e delle relative repliche di disponibilità, nonché dei database, con gli stati definiti dai criteri AlwaysOn.  
  
 [Gruppi di disponibilità AlwaysOn](always-on-availability-groups-sql-server.md) Soluzione a disponibilità elevata e ripristino di emergenza che offre un'alternativa di livello Enterprise al mirroring del database.  
  
 gruppo di disponibilità  
 Contenitore per un set discreto di database utente, noti come *database di disponibilità*, su cui si verifica il failover.  
  
 replica di disponibilità  
 Creazione di un'istanza di un gruppo di disponibilità ospitata da un'istanza specifica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e che mantiene una copia locale di ogni database di disponibilità che appartiene al gruppo di disponibilità. Sono disponibili due tipi di replica di disponibilità: una *replica primaria* e da una a quattro *repliche secondarie*. Le istanze del server che ospitano le repliche di disponibilità per un determinato gruppo di disponibilità devono risiedere in nodi diversi di un solo cluster WSFC (Windows Server Failover Clustering).  
  
 database di disponibilità  
 Database che appartiene a un gruppo di disponibilità. Per ogni database di disponibilità, il gruppo di disponibilità gestisce una sola copia di lettura e scrittura (il *database primario*) e da una a quattro copie di sola lettura (*database secondari*).  
  
 Dashboard AlwaysOn  
 Un dashboard [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] fornisce una vista immediata dell'integrità di un gruppo di disponibilità. Per ulteriori informazioni, vedere [Dashboard AlwaysOn](#Dashboard)di seguito in questo argomento.  
  
##  <a name="predefined-policies-and-issues"></a><a name="AlwaysOnPBM"></a> Criteri predefiniti e problemi  
 Nella tabella seguente sono riepilogati i criteri predefiniti.  
  
|Nome criteri|Problema|Categoria**<sup>*</sup>**|Facet|  
|-----------------|-----------|------------------------------|-----------|  
|Stato del cluster WSFC|Il [servizio cluster WSFC è offline](wsfc-cluster-service-is-offline.md).|Critico|Istanza di SQL Server|  
|Stato online del gruppo di disponibilità|Il [gruppo di disponibilità è offline](availability-group-is-offline.md).|Critico|gruppo di disponibilità|  
|Conformità del gruppo di disponibilità al failover automatico|Il [gruppo di disponibilità non è pronto per il failover automatico](availability-group-is-not-ready-for-automatic-failover.md).|Critico|gruppo di disponibilità|  
|Stato di sincronizzazione dei dati delle repliche di disponibilità|[Alcune repliche di disponibilità non eseguono la sincronizzazione dei dati](some-availability-replicas-are-not-synchronizing-data.md).|Avviso|gruppo di disponibilità|  
|Stato di sincronizzazione dei dati delle repliche sincrone|[Alcune repliche sincrone non sono sincronizzate](some-synchronous-replicas-are-not-synchronized.md).|Avviso|gruppo di disponibilità|  
|Stato del ruolo delle repliche di disponibilità|[Alcune repliche di disponibilità non dispongono di un ruolo integro](some-availability-replicas-do-not-have-a-healthy-role.md).|Avviso|gruppo di disponibilità|  
|Stato di connessione delle repliche di disponibilità|[Alcune repliche di disponibilità sono disconnesse](some-availability-replicas-are-disconnected.md).|Avviso|gruppo di disponibilità|  
|Stato del ruolo della replica di disponibilità|[La replica di disponibilità non dispone di un ruolo integro](availability-replica-does-not-have-a-healthy-role.md).|Critico|replica di disponibilità|  
|Stato di connessione della replica di disponibilità|[La replica di disponibilità è disconnessa](availability-replica-is-disconnected.md).|Critico|replica di disponibilità|  
|Stato di join della replica di disponibilità|[Replica di disponibilità non unita in join](availability-replica-is-not-joined.md).|Avviso|replica di disponibilità|  
|Stato di sincronizzazione dei dati delle repliche di disponibilità|[Lo stato di sincronizzazione dei dati di alcuni database di disponibilità non è integro](data-synchronization-state-of-some-availability-database-is-not-healthy.md).|Avviso|replica di disponibilità|  
|Stato di sospensione del database di disponibilità|Il [database di disponibilità è sospeso](availability-database-is-suspended.md).|Avviso|Database di disponibilità|  
|Stato di join del database di disponibilità|Il [database secondario non è unito in join](secondary-database-is-not-joined.md).|Avviso|Database di disponibilità|  
|Stato di sincronizzazione dei dati del database di disponibilità|[Lo stato di sincronizzazione dei dati del database di disponibilità non è integro](data-synchronization-state-of-availability-database-is-not-healthy.md).|Avviso|Database di disponibilità|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>** Per i criteri AlwaysOn, i nomi delle categorie vengono usati come ID. La modifica del nome di una categoria AlwaysOn causa l'interruzione della funzionalità di valutazione dell'integrità. Evitare pertanto di modificare i nomi di categorie AlwaysOn.  
  
##  <a name="alwayson-dashboard"></a><a name="Dashboard"></a>Dashboard AlwaysOn  
 Il dashboard AlwaysOn fornisce una vista immediata dell'integrità di un gruppo di disponibilità. Nel dashboard AlwaysOn sono incluse le nuove funzionalità seguenti:  
  
-   Consente di visualizzare facilmente i dettagli relativi a un gruppo di disponibilità specificato, le repliche di disponibilità e i database corrispondenti.  
  
-   Fornisce indicatori visivi degli stati chiave per velocizzare la scelta di decisioni operative da parte degli amministratori del database.  
  
-   Fornisce punti di avvio per scenari per la risoluzione di problemi.  
  
-   Per un determinato problema operativo popola la finestra di dialogo **Risultato di valutazione criteri** con informazioni relative alle violazioni dei criteri di integrità AlwaysOn specifiche e con collegamenti a informazioni della Guida sulle possibili correzioni.  
  
-   Fornisce un visualizzatore di eventi estesi relativi all'integrità per mostrare gli eventi precedenti per i problemi specifici di AlwaysOn.  
  
-   Se il failover sul gruppo di disponibilità costituisce una possibile risoluzione per un problema, fornisce un punto di avvio per i collegamenti alla[Procedura guidata Failover del gruppo di disponibilità](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md). Questa procedura guida un amministratore del database attraverso il processo di failover manuale.  
  
##  <a name="extending-the-alwayson-health-model"></a><a name="ExtendHealthModel"></a>Estensione del modello di integrità AlwaysOn  
 L'estensione del modello di integrità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] riguarda semplicemente la creazione di propri criteri definiti dall'utente e l'inserimento in determinate categorie in base al tipo di oggetto di cui si sta eseguendo il monitoraggio.  Dopo aver modificato alcune impostazioni, tramite il dashboard AlwaysOn verranno valutati automaticamente i propri criteri definiti dall'utente, nonché i criteri predefiniti AlwaysOn.  
  
 I criteri definiti dall'utente possono usare qualsiasi facet della gestione basata su criteri disponibile, inclusi quelli utilizzati dai criteri predefiniti AlwaysOn (vedere [Criteri predefiniti e problemi](#AlwaysOnPBM), precedentemente in questo argomento). Il facet Server fornisce le proprietà seguenti per il monitoraggio dell'integrità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]: (`IsHadrEnabled` e `HadrManagerStatus`). Fornisce inoltre le proprietà dei seguenti criteri per il monitoraggio della configurazione del cluster WSFC: `ClusterQuorumType` e `ClusterQuorumState`.  
  
 Per altre informazioni, vedere la pagina relativa alla [seconda parte del modelli di integrità AlwaysOn riguardante l’estensione del modello di integrità](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model) (blog del team di SQL Server AlwaysOn).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Utilizzare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Ripristino di emergenza WSFC tramite quorum forzato &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [Forzare l'avvio di un cluster WSFC senza un quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Eseguire un failover manuale forzato di un gruppo di disponibilità &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Risolvere i problemi relativi a un'operazione di aggiunta file non riuscita &#40;Gruppi di disponibilità AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   [Pagina sulla prima parte del modello di integrità AlwaysOn riguardante l'architettura del modello di integrità](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview)  
  
-   [Pagina relativa alla seconda parte del modello di integrità AlwaysOn riguardante l'estensione del modello di integrità](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)  
  
-   [Pagina relativa alla guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di disponibilità AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Amministrazione di un gruppo di disponibilità &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
