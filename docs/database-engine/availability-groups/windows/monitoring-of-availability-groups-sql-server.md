---
title: Strumenti per il monitoraggio dei gruppi di disponibilità
description: "Riferimento per i vari strumenti disponibili per il monitoraggio delle prestazioni e dell'integrità dei gruppi di disponibilità Always On. "
ms.custom: seodec18
ms.date: 06/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0cf0478f63ab98bda9bf13a7cc5bad0f98bd1795
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973120"
---
# <a name="tools-to-monitor-always-on-availability-groups"></a>"Strumenti per il monitoraggio dei gruppi di disponibilità Always On"
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per monitorare le proprietà e lo stato di un gruppo di disponibilità AlwaysOn, è possibile usare gli strumenti descritti di seguito.  
  
|Strumento|Breve descrizione|Collegamenti|  
|----------|-----------------------|-----------|  
|Pacchetto System Center Monitoring per SQL Server|Il pacchetto di monitoraggio per SQL Server (SQLMP, Monitoring Pack for SQL Server) è la soluzione consigliata per l'esecuzione del monitoraggio di gruppi, repliche e database di disponibilità per amministratori IT. Nel monitoraggio di funzionalità che sono particolarmente pertinenti a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sono inclusi gli elementi seguenti:<br /><br /> Individuazione automatica di gruppi, repliche e database di disponibilità in centinaia di computer. In questo modo è possibile tenere traccia facilmente dell'inventario di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Supporto completo per la creazione di ticket e la generazione di avvisi per System Center Operations Manager (SCOM). Queste funzionalità forniscono una conoscenza dettagliata che consente una soluzione più rapida a un problema.<br /><br /> Estensione personalizzata al monitoraggio dell'integrità AlwaysOn tramite la gestione basata su criteri (PBM).<br /><br /> Rollup da database di disponibilità in repliche di disponibilità tramite integrità.<br /><br /> Attività personalizzate che consentono di gestire [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] dalla console di System Center Operations Manager.|Per scaricare il pacchetto di monitoraggio (SQLServerMP.msi) e *Guida del Management Pack di SQL Server per System Center Operations Manager* (SQLServerMPGuide.doc), vedere:<br /><br /> [Pacchetto System Center Monitoring per SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] forniscono numerose informazioni sui gruppi di disponibilità e sulle repliche, i database, i listener e l'ambiente con cluster WSFC relativi.|[Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Nel riquadro **Dettagli Esplora oggetti** sono visualizzate informazioni di base sui gruppi di disponibilità ospitati nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui è stata effettuata la connessione.<br /><br /> **\*\* Suggerimento \*\*** Usare questo riquadro per selezionare più repliche, database o gruppi di disponibilità e per eseguire attività amministrative di routine sugli oggetti selezionati, ad esempio la rimozione di più database o repliche di disponibilità da un gruppo di disponibilità.|[Usare Dettagli Esplora oggetti per monitorare Gruppi di disponibilità &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Le finestre di dialogo**Proprietà** consentono di visualizzare le proprietà di gruppi, repliche o listener di disponibilità e, talvolta, di modificarne i valori.|-   [Visualizzare le proprietà dei gruppi di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)<br />-   [Visualizzare le proprietà della replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)<br />-   [Visualizzare le proprietà del listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)|  
|Monitor di sistema|Nell'oggetto prestazione **SQLServer:Availability Replica** sono inclusi contatori delle prestazioni con informazioni sulle repliche di disponibilità.|[SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor di sistema|Nell'oggetto prestazione **SQLServer:Database Replica** sono inclusi contatori delle prestazioni con informazioni sui database secondari in una determinata replica secondaria.<br /><br /> Nell'oggetto **SQLServer:Databases** in SQL Server sono inclusi, tra l'altro, i contatori delle prestazioni per il monitoraggio delle attività del log delle transazioni. I contatori seguenti sono particolarmente rilevanti per il monitoraggio dell'attività del log delle transazioni sui database di disponibilità: **Ora di scrittura scaricamento log (ms)**, **Scaricamenti log/sec**, **Mancati riscontri cache del pool di log/sec**, **Letture disco del pool di log/sec** e **Richieste del pool di log/sec**.|[SQL Server, replica di database](../../../relational-databases/performance-monitor/sql-server-database-replica.md) e [SQL Server, oggetto di database](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [The Always On Health Model Part 1 -- Health Model Architecture (Pagina sulla prima parte del modello di integrità AlwaysOn riguardante l'architettura del modello di integrità)](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/08/the-alwayson-health-model-part-1-health-model-architecture/)  
  
     [The Always On Health Model Part 2 -- Extending the Health Model](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/the-alwayson-health-model-part-2-extending-the-health-model/)  
  
     [Monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 1: Panoramica dei cmdlet di base](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
     [Monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 2: Utilizzo di cmdlet avanzati](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
     [Monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 3: Semplice applicazione di monitoraggio](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
     [Monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 4: Integrazione con SQL Server Agent](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
     [SQL Server Always On Team Blogs (Blog di SQL Server Always On): blog ufficiale del team di SQL Server Always On](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.microsoft.com/psssql/)  
  
-   **White paper:**  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dei gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Funzioni e DMV di Gruppi di disponibilità AlwaysOn &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Criteri di failover flessibili per failover automatico di un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Correzione automatica della pagina &#40;Gruppi di disponibilità: Mirroring del database&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usare il dashboard Always On &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
