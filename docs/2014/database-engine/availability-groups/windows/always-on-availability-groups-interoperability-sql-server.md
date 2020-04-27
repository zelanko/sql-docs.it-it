---
title: 'Gruppi di disponibilità AlwaysOn: interoperabilità (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f6123f66d687327ba56601419328e44fd920a2a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815747"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Gruppi di disponibilità AlwaysOn: interoperabilità (SQL Server)
  In questo argomento viene descritta l'interoperabilità di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] con altre funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  

  
##  <a name="features-that-interoperate-with-alwayson-availability-groups"></a><a name="Interop"></a>Funzionalità che interagiscono con Gruppi di disponibilità AlwaysOn  
 Nella tabella seguente vengono elencate le funzionalità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di interoperabilità con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Un collegamento nella colonna **Ulteriori informazioni** indica che per una determinata funzionalità esistono le considerazioni di interoperabilità.  
  
|Funzionalità|Altre informazioni|  
|-------------|----------------------|  
|Change Data Capture|[Replica, Rilevamento modifiche, Change Data Capture e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|Rilevamento modifiche|[Replica, Rilevamento modifiche, Change Data Capture e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|Database indipendenti|[Database indipendenti con Gruppi di disponibilità AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)|  
|Crittografia del database|[Database crittografati con Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|Snapshot del database|[Snapshot del database con Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM e tabelle FileTable|[FILESTREAM e FileTable con Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|Ricerca full-text|Nota: gli indici full-text sono sincronizzati con i database secondari AlwaysOn.|  
|Log shipping|[Prerequisiti per la migrazione dal log shipping a Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|Archivio BLOB remoto (RBS)|[Archivio BLOB remoti &#40;RBS&#41; e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|[Configurazione della replica per gruppi di disponibilità AlwaysOn (SQL Server)](configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Gestione di un database di pubblicazione AlwaysOn &#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Replica, Rilevamento modifiche, Change Data Capture e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Sottoscrittori della replica e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services con i gruppi di disponibilità AlwaysOn](analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|Utilizzare solo repliche secondarie come origine dei dati di Reporting Services e ridurre il carico nella replica primaria di lettura e scrittura.<br /><br /> [Reporting Services con Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Broker di servizio|[Service Broker con Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server Agent||  
  
##  <a name="features-that-do-not-interoperate-with-alwayson-availability-groups"></a><a name="NoInterop"></a>Funzionalità che non interagiscono con Gruppi di disponibilità AlwaysOn  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] non è in grado di interagire con le funzionalità:  
  
-   Transazioni tra database e transazioni distribuite  
  
     Per altre informazioni sui motivi per cui queste transazioni non sono supportate, vedere [Transazioni tra database non supportate per il mirroring del database o i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
-   Mirroring del database  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Pagina relativa alla guida alla migrazione in cui viene illustrata la migrazione al clustering di failover e ai gruppi di disponibilità di SQL Server 2012 dal clustering e dalle distribuzioni del mirroring precedenti](https://blogs.msdn.com/b/sqlalwayson/archive/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments.aspx)  
  
     [Blog del team di SQL Server AlwaysOn: Blog ufficiale del team di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **White paper:**  
  
     [Pagina relativa alla guida alla migrazione in cui viene illustrata la migrazione in gruppi di disponibilità AlwaysOn da distribuzioni precedenti in cui vengono combinati il mirroring del database e il log shipping](https://msdn.microsoft.com/library/jj635217)  
  
     [Pagina relativa alla guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
