---
title: Monitoraggio di Gruppi di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 6f1da20eb1c23176036dad0847d5b420a498e83e
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922006"
---
# <a name="monitoring-of-availability-groups-sql-server"></a>Monitoraggio di Gruppi di disponibilità (SQL Server)
  Per monitorare le proprietà e lo stato di un gruppo di disponibilità AlwaysOn, è possibile usare gli strumenti riportati di seguito.  
  
|Strumento|Breve descrizione|Collegamenti|  
|----------|-----------------------|-----------|  
|Pacchetto System Center Monitoring per SQL Server|Il pacchetto di monitoraggio per SQL Server (SQLMP, Monitoring Pack for SQL Server) è la soluzione consigliata per l'esecuzione del monitoraggio di gruppi, repliche e database di disponibilità per amministratori IT. Nel monitoraggio di funzionalità che sono particolarmente pertinenti a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sono inclusi gli elementi seguenti:<br /><br /> Individuazione automatica di gruppi, repliche e database di disponibilità in centinaia di computer. In questo modo è possibile tenere traccia facilmente dell'inventario di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Supporto completo per la creazione di ticket e la generazione di avvisi per System Center Operations Manager (SCOM). Queste funzionalità forniscono una conoscenza dettagliata che consente una soluzione più rapida a un problema.<br /><br /> Estensione personalizzata al monitoraggio dell'integrità AlwaysOn mediante la gestione basata su criteri (PBM).<br /><br /> Rollup da database di disponibilità in repliche di disponibilità tramite integrità.<br /><br /> Attività personalizzate che consentono di gestire [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] dalla console di System Center Operations Manager.|Per scaricare il pacchetto di monitoraggio (SQLServerMP.msi) e *Guida del Management Pack di SQL Server per System Center Operations Manager* (SQLServerMPGuide.doc), vedere:<br /><br /> [Pacchetto System Center Monitoring per SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] forniscono numerose informazioni sui gruppi di disponibilità e sulle repliche, i database, i listener e l'ambiente con cluster WSFC relativi.|[Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Nel riquadro **Dettagli Esplora oggetti** sono visualizzate informazioni di base sui gruppi di disponibilità ospitati nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui è stata effettuata la connessione.<br /><br /> Suggerimento: usare questo riquadro per selezionare più gruppi, repliche o database di disponibilità e per eseguire attività amministrative di routine sugli oggetti selezionati, ad esempio la rimozione di più repliche o database di disponibilità da un gruppo di disponibilità.|[Usare Dettagli Esplora oggetti per monitorare i gruppi di disponibilità &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|Le finestre di dialogo**Proprietà** consentono di visualizzare le proprietà di gruppi, repliche o listener di disponibilità e, talvolta, di modificarne i valori.|[Visualizzare le proprietà dei gruppi di disponibilità &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)<br /><br /> [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)<br /><br /> [Visualizzare le proprietà del listener del gruppo di disponibilità &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)|  
|Monitor di sistema|Nell'oggetto prestazione **SQLServer:Availability Replica** sono inclusi contatori delle prestazioni con informazioni sulle repliche di disponibilità.|[SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor di sistema|Nell'oggetto prestazione **SQLServer:Database Replica** sono inclusi contatori delle prestazioni con informazioni sui database secondari in una determinata replica secondaria.<br /><br /> Nell'oggetto **SQLServer:Databases** in SQL Server sono inclusi, tra l'altro, i contatori delle prestazioni per il monitoraggio delle attività del log delle transazioni. I contatori seguenti sono particolarmente rilevanti per il monitoraggio dell'attività del log delle transazioni sui database di disponibilità: **Ora di scrittura scaricamento log (ms)**, **Scaricamenti log/sec**, **Mancati riscontri cache del pool di log/sec**, **Letture disco del pool di log/sec**e **Richieste del pool di log/sec**.|[SQL Server, replica di database](../../../relational-databases/performance-monitor/sql-server-database-replica.md) e [SQL Server, oggetto di database](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Pagina sulla prima parte del modello di integrità AlwaysOn riguardante l'architettura del modello di integrità](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-1-health-model-architecture)  
  
     [Pagina relativa alla seconda parte del modello di integrità AlwaysOn riguardante l'estensione del modello di integrità](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)  
  
     [Pagina relativa al monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 1: panoramica sui cmdlet di base](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview)  
  
     [Pagina relativa al monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 2: utilizzo avanzato dei cmdlet](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage)  
  
     [Pagina relativa al monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 3 : una semplice applicazione di monitoraggio](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application)  
  
     [Pagina relativa al monitoraggio dell'integrità AlwaysOn con PowerShell - Parte 4 : integrazione con SQL Server Agent](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent)  
  
     [Blog del team di SQL Server AlwaysOn: Blog ufficiale del team di SQL Server AlwaysOn](https://docs.microsoft.com/archive/blogs/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **White paper:**  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Gruppi di disponibilità AlwaysOn &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql)   
 [Gruppi di disponibilità AlwaysOn funzioni e viste a gestione dinamica &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions)   
 [Criteri di failover flessibili per il failover automatico di un gruppo di disponibilità &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [&#40;di correzione automatica della pagina per i gruppi di disponibilità e il mirroring del database&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
