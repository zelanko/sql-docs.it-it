---
title: Creazione e configurazione di gruppi di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14dea0c618f754024a18ca24d64b98b08aa99f64
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368923"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>Creazione e configurazione di gruppi di disponibilità (SQL Server)
  Negli argomenti di questa sezione si illustra come distribuire un'implementazione di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in istanze di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] che si trovano in nodi WSFC (Windows Server Failover Clustering) diversi all'interno di un singolo cluster di failover WSFC.  
  
 Prima di creare il primo gruppo di disponibilità, è consigliabile avere familiarità con le informazioni contenute negli argomenti seguenti:  
  
 [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 In questo argomento si descrivono i prerequisiti, le restrizioni e i consigli per i computer, cioè i nodi WSFC, le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], i gruppi di disponibilità, le repliche e i database. In questo argomento sono inoltre contenute informazioni relative alle considerazioni sulla sicurezza.  
  
 [Introduzione ai gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 Sono contenute informazioni sulle procedure per configurare un'istanza del server, creare un gruppo di disponibilità, configurare il gruppo di disponibilità per le connessioni client, gestire i gruppi di disponibilità, nonché per monitorare i gruppi di disponibilità  
  
 
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per configurare un'istanza del server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Creare un Endpoint del mirroring per i gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **Per iniziare a usare la configurazione di gruppi di disponibilità AlwaysOn**  
  
-   [Introduzione ai gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **Per creare e configurare un nuovo gruppo di disponibilità**  
  
-   [Usare la Creazione guidata gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Creare un gruppo di disponibilità &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Creare un gruppo di disponibilità &#40;PowerShell SQL Server&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Usare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Specifica dell'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurare i criteri di Failover flessibili per controllare le condizioni per il Failover automatico (gruppi di disponibilità AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Configurare il backup su repliche di disponibilità &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Avviare lo spostamento dati su un Database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Gestione di account di accesso e processi per i database di un gruppo di disponibilità &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **Per risolvere i problemi**  
  
-   [Risolvere i problemi di configurazione di gruppi di disponibilità di AlwaysOn (SQL Server) eliminato](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Risolvere i problemi di un'operazione di aggiunta File non riuscita &#40;gruppi di disponibilità AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   **Blog:**  
  
     [Su AlwaysON - HADRON serie: Utilizzo del Pool di lavoro per HADRON database abilitati](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn Team blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Pagina relativa ai blog del Servizio Supporto Tecnico Clienti per gli ingegneri di SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Video:**  
  
     [Serie Microsoft SQL Server nome in codice "Denali" AlwaysOn, parte 1: Introduzione della soluzione di disponibilità elevata di prossima generazione](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Serie Microsoft SQL Server nome in codice "Denali" AlwaysOn, parte 2: Creazione di una soluzione di disponibilità elevata critica tramite Alwasyon](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper:**  
  
     [Microsoft SQL Server AlwaysOn Solutions Guide for High Availability and Disaster Recovery](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Pagina relativa ai white paper Microsoft per SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Pagina relativa ai white paper del team di consulenza clienti di SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Amministrazione di un gruppo di disponibilità &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Criteri AlwaysOn per problemi operativi con gruppi di disponibilità AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Gruppi di disponibilità AlwaysOn: Interoperabilità (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
  
