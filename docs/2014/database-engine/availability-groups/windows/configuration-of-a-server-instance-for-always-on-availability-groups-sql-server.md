---
title: Configurazione di un'istanza del Server per gruppi di disponibilità (SQL Server) Always On | Microsoft Docs
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
ms.openlocfilehash: d8c9aa465237010ff48881a2df176de6d067da0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815278"
---
# <a name="configuration-of-a-server-instance-for-always-on-availability-groups-sql-server"></a>Configurazione di un'istanza del server per i gruppi di disponibilità AlwaysOn (SQL Server)
  In questo argomento vengono fornite informazioni sui requisiti per la configurazione di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Per informazioni di base sui prerequisiti e le limitazioni di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] per i nodi Windows Server Failover Clustering (WSFC) e per le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Prerequisiti, restrizioni e consigli per i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
 
  
##  <a name="TermsAndDefinitions"></a> Termini e definizioni  
  
 Soluzione di disponibilità elevata e recupero di emergenza che offre una sostituzione di livello enterprise al mirroring del database. Un *gruppo di disponibilità* supporta un ambiente di failover per un set discreto di database utente, noti come *database di disponibilità*, su cui si verifica il failover.  
  
 replica di disponibilità  
 Creazione di un'istanza di un gruppo di disponibilità ospitata da un'istanza specifica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e che mantiene una copia locale di ogni database di disponibilità che appartiene al gruppo di disponibilità. Sono disponibili due tipi di replica di disponibilità: una *replica primaria* e da una a quattro *repliche secondarie*. Le istanze del server che ospitano le repliche di disponibilità per un determinato gruppo di disponibilità devono risiedere in nodi diversi di un solo cluster WSFC (Windows Server Failover Clustering).  
  
 [endpoint del mirroring del database](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 È un oggetto di SQL Server che consente la comunicazione di SQL Server nella rete. Per fare parte del mirroring del database e/o di un'istanza del server [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è richiesto un endpoint speciale e dedicato. Tutte le connessioni del mirroring e del gruppo di disponibilità in un'istanza del server utilizzano lo stesso endpoint del mirroring del database. Si tratta di un endpoint speciale utilizzato solo per ricevere tali connessioni da altre istanze del server.  
  
##  <a name="ConfigSI"></a> Per configurare un'istanza del Server per supportare i gruppi di disponibilità AlwaysOn  
 Per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], un'istanza del server deve trovarsi in un nodo nel cluster di failover WSFC in cui è ospitato il gruppo di disponibilità, essere abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e in essa deve essere presente un endpoint del mirroring del database.  
  
1.  Abilitare la funzionalità Gruppi di disponibilità AlwaysOn in ogni istanza del server che deve far parte di uno o più gruppi di disponibilità. Una determinata istanza del server può ospitare solo una singola replica di disponibilità per un gruppo di disponibilità specifico.  
  
2.  Verificare che nell'istanza del server sia incluso un endpoint del mirroring del database.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per abilitare gruppi di disponibilità AlwaysOn**  
  
-   [Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Per determinare la presenza di un endpoint del mirroring del database**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **Per creare un endpoint del mirroring del database**  
  
-   [Creare un Endpoint del mirroring per i gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Su AlwaysON - HADRON serie: Uso del pool di lavoro per database abilitati HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn Team blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Video:**  
  
     [Serie Microsoft SQL Server nome in codice "Denali" AlwaysOn, parte 1: Introducing the Next Generation High Availability Solution](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302) (Serie Always On in Microsoft SQL Server nome in codice "Denali", parte 1: Introduzione alla soluzione a disponibilità elevata di nuova generazione)  
  
     [Serie Microsoft SQL Server nome in codice "Denali" AlwaysOn, parte 2: Creazione di una soluzione di disponibilità elevata critica tramite Alwasyon](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper:**  
  
     [Microsoft SQL Server AlwaysOn Solutions Guide for High Availability and Disaster Recovery](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Gruppi di disponibilità AlwaysOn: Interoperabilità (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Clustering di failover e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Istanze del Cluster di Failover AlwaysOn](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
