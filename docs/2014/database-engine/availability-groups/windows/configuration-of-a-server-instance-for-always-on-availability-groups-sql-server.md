---
title: Configurazione di un'istanza del server per i gruppi di disponibilità Always On (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3dcd239c782f53ec11970e94f89e5acfac982785
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75228807"
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>Configurazione di un'istanza del server per i gruppi di disponibilità AlwaysOn (SQL Server)
  In questo argomento vengono fornite informazioni sui requisiti per la configurazione di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Per informazioni di base sui prerequisiti e le limitazioni di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] per i nodi Windows Server Failover Clustering (WSFC) e per le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
 
  
##  <a name="TermsAndDefinitions"></a>Termini e definizioni  
  
 Soluzione di disponibilità elevata e recupero di emergenza che offre una sostituzione di livello enterprise al mirroring del database. Un *gruppo di disponibilità* supporta un ambiente di failover per un set discreto di database utente, noti come *database di disponibilità*, il cui failover viene eseguito contemporaneamente.  
  
 replica di disponibilità  
 Creazione di un'istanza di un gruppo di disponibilità ospitata da un'istanza specifica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e che mantiene una copia locale di ogni database di disponibilità che appartiene al gruppo di disponibilità. Sono disponibili due tipi di replica di disponibilità: una *replica primaria* e da una a quattro *repliche secondarie*. Le istanze del server che ospitano le repliche di disponibilità per un determinato gruppo di disponibilità devono risiedere in nodi diversi di un solo cluster WSFC (Windows Server Failover Clustering).  
  
 [endpoint del mirroring del database](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 È un oggetto di SQL Server che consente la comunicazione di SQL Server nella rete. Per fare parte del mirroring del database e/o di un'istanza del server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è richiesto un endpoint speciale e dedicato. Tutte le connessioni del mirroring e del gruppo di disponibilità in un'istanza del server utilizzano lo stesso endpoint del mirroring del database. Si tratta di un endpoint speciale utilizzato solo per ricevere tali connessioni da altre istanze del server.  
  
##  <a name="ConfigSI"></a>Per configurare un'istanza del server per il supporto di Gruppi di disponibilità AlwaysOn  
 Per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], un'istanza del server deve trovarsi in un nodo nel cluster di failover WSFC in cui è ospitato il gruppo di disponibilità, essere abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e in essa deve essere presente un endpoint del mirroring del database.  
  
1.  Abilitare la funzionalità Gruppi di disponibilità AlwaysOn in ogni istanza del server che deve far parte di uno o più gruppi di disponibilità. Una determinata istanza del server può ospitare solo una singola replica di disponibilità per un gruppo di disponibilità specifico.  
  
2.  Verificare che nell'istanza del server sia incluso un endpoint del mirroring del database.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per abilitare Gruppi di disponibilità AlwaysOn**  
  
-   [Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Per determinare se esiste un endpoint del mirroring del database**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **Per creare un endpoint del mirroring del database**  
  
-   [Creazione di un endpoint del mirroring del database per Gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Pagina relativa alla serie di informazioni su HADRON riguardanti l'utilizzo del pool di lavoro per database abilitati HADRON in AlwaysOn](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blog del team di SQL Server AlwaysOn: Blog ufficiale del team di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Video:**  
  
     [Pagina relativa alla prima parte riguardante l'introduzione della soluzione a disponibilità elevata di prossima generazione della serie AlwaysOn di Microsoft SQL Server nome in codice "Denali"](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Pagina relativa alla seconda parte riguardante la compilazione di una soluzione a disponibilità elevata critica tramite AlwasyOn della serie AlwaysOn di Microsoft SQL Server nome in codice "Denali"](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper:**  
  
     [Pagina relativa alla guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Gruppi di disponibilità AlwaysOn: interoperabilità (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Clustering di failover e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Windows Server failover clustering &#40;&#41; WSFC con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Istanze del cluster di failover AlwaysOn](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
