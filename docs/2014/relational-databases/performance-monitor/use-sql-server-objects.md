---
title: Usare oggetti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67edebf9b4adcf40c12190446997dbd7c4b6e57b
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100726"
---
# <a name="use-sql-server-objects"></a>Utilizzare oggetti di SQL Server
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rende disponibili oggetti e contatori utilizzabili in Monitoraggio di sistema per il monitoraggio dell'attività nei computer che eseguono un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per oggetto si intende qualsiasi risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio un blocco di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un processo di Windows. Ogni oggetto contiene uno o più contatori che determinano diversi aspetti degli oggetti da monitorare. Ad esempio, l'oggetto **SQL Server Locks** contiene i contatori **Numero di blocchi critici deadlock/sec** e **Timeout blocchi/sec**.  
  
 Se un computer include più risorse dello stesso tipo, saranno presenti più istanze dello stesso tipo di oggetto. Ad esempio, nei sistemi con più processori saranno presenti più istanze dell'oggetto di tipo **Processor** . Per ogni database di **sarà presente un'istanza dell'oggetto di tipo** Databases [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per alcuni tipi di oggetti, ad esempio **Memory Manager** , è prevista una sola istanza. Se sono presenti più istanze di un tipo di oggetto, è possibile aggiungere i contatori per tenere traccia delle statistiche di ogni singola istanza o in molti casi di tutte le istanze contemporaneamente. I contatori per l'istanza predefinita sono visualizzati nel formato **SQLServer:**_\<nome oggetto>_. I contatori per le istanze denominate sono visualizzati nel formato **MSSQL$**_\<nome istanza>_**:**_\<nome contatore>_ o **SQLAgent$**_\<nome istanza>_**:**_\<nome contatore>_.  
  
 Per specificare gli oggetti e i contatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da monitorare all'avvio di Monitoraggio di sistema, aggiungere o rimuovere i contatori nel grafico e salvare le impostazioni.  
  
 È possibile configurare Monitoraggio di sistema in modo da visualizzare le statistiche di qualsiasi contatore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È anche possibile impostare un valore soglia per i contatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e generare un avviso quando viene superato il valore specificato. Per altre informazioni sull'impostazione di un avviso, vedere [Creare un avviso del database di SQL Server](create-a-sql-server-database-alert.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le statistiche sono visualizzate solo quando viene installata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]viene arrestata e riavviata, la visualizzazione delle statistiche viene interrotta e ripresa automaticamente. Si noti inoltre che i contatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno visualizzati nello snap-in di Monitoraggio di sistema anche se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in esecuzione. Su un'istanza di cluster, i contatori delle prestazioni funzionano solo sul nodo in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Oggetti prestazione di SQL Server Agent](#SQLServerAgentPOs)  
  
-   [Oggetti prestazione di Service Broker](#ServiceBrokerPOs)  
  
-   [Oggetti prestazione di SQL Server](#SQLServerPOs)  
  
-   [Oggetti prestazione della replica di SQL Server](#SQLServerReplicationPOs)  
  
-   [Contatori delle pipeline SSIS](#SsisPipelineCounters)  
  
-   [Autorizzazioni necessarie](#RequiredPermissions)  
  
##  <a name="SQLServerAgentPOs"></a> Oggetti prestazione di SQL Server Agent  
 Nella tabella seguente sono indicati gli oggetti prestazione disponibili per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|[SQLAgent:Avvisi](sql-server-agent-alerts-object.md)|Offre informazioni relative agli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Processi](sql-server-agent-jobs-object.md)|Offre informazioni relative ai processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:JobSteps](sql-server-agent-jobsteps-object.md)|Offre informazioni relative ai passaggi di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Statistiche](sql-server-agent-statistics-object.md)|Offre informazioni generali relative a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
  
##  <a name="ServiceBrokerPOs"></a> Oggetti prestazione di Service Broker  
 Nella tabella seguente sono indicati gli oggetti prestazione disponibili per [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|[SQLServer:Attivazione Broker](sql-server-broker-activation-object.md)|Offe informazioni sulle attività attivate da [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|[SQLServer:Statistiche Broker](sql-server-broker-statistics-object.md)|Offre informazioni generali relative a [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
|[SQLServer:Broker Transport](sql-server-broker-dbm-transport-object.md)|Offre informazioni relative alle funzioni di rete di [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
  
##  <a name="SQLServerPOs"></a> Oggetti prestazione di SQL Server  
 Nella seguente tabella vengono descritti gli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|[SQLServer:Access Methods](sql-server-access-methods-object.md)|Ricerca e misura l'allocazione degli oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ad esempio, il numero di ricerche eseguite negli indici o il numero di pagine allocate per gli indici e i dati).|  
|[SQLServer:Backup Device](sql-server-backup-device-object.md)|Offre informazioni sui dispositivi di backup utilizzati nelle operazioni di backup e ripristino, ad esempio la velocità effettiva del dispositivo di backup.|  
|[SQLServer:Buffer Manager](sql-server-buffer-manager-object.md)|Offre informazioni sui buffer di memoria utilizzati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio **freememory** e **buffer cache hit ratio**.|  
|[Nodo SQLServer:Buffer](sql-server-buffer-node.md)|Offre informazioni sulla frequenza con cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede le pagine disponibili e vi accede.|  
|[SQLServer:CLR](sql-server-clr-object.md)|Offre informazioni su Common Language Runtime (CLR).|  
|[SQLServer:Gestione cursori per tipo](sql-server-cursor-manager-by-type-object.md)|Offre informazioni relative ai cursori.|  
|[SQLServer:Cursor Manager Total](sql-server-cursor-manager-total-object.md)|Offre informazioni relative ai cursori.|  
|[SQLServer:Database Mirroring](sql-server-database-mirroring-object.md)|Offre informazioni relative al mirroring del database.|  
|[SQLServer:Databases](sql-server-databases-object.md)|Offre informazioni su un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio la quantità di spazio di log libero o il numero di transazioni attive nel database. Possono essere presenti più istanze di questo oggetto.|  
|[SQL Server:Deprecated Features](sql-server-deprecated-features-object.md)|Conta il numero di volte in cui vengono utilizzate le caratteristiche deprecate.|  
|[SQLServer:Exec Statistics](sql-server-execstatistics-object.md)|Offre informazioni relative alle statistiche di esecuzione.|  
|[SQLServer:General Statistics](sql-server-general-statistics-object.md)|Offre informazioni sull'attività dell'intero server, ad esempio il numero di utenti connessi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server:HADR Availability Replica](sql-server-availability-replica.md)|Offre informazioni sulle repliche di disponibilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQL Server:HADR Database Replica](sql-server-database-replica.md)|Offre informazioni sulle repliche di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQLServer:Latch](sql-server-latches-object.md)|Offre informazioni sui latch sulle risorse interne, ad esempio le pagine di database, utilizzati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Locks](sql-server-locks-object.md)|Offre informazioni sulle singole richieste di blocco eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio i timeout dei blocchi e i deadlock. Possono essere presenti più istanze di questo oggetto.|  
|[SQLServer:Gestione memoria](sql-server-memory-manager-object.md)|Offre informazioni sull'utilizzo della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio il numero totale delle strutture di blocco attualmente allocate.|  
|[SQLServer:Plan Cache](sql-server-plan-cache-object.md)|Offre informazioni sulla cache di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzata per archiviare oggetti, ad esempio stored procedure, trigger e piani delle query.|  
|[SQLServer: Statistiche del Pool di risorse](sql-server-resource-pool-stats-object.md)|Fornisce informazioni sulle statistiche del pool di risorse di Resource Governor.|  
|[SQLServer:SQL Errors](sql-server-sql-errors-object.md)|Offre informazioni relative agli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLServer:Statistiche SQL](sql-server-sql-statistics-object.md)|Offre informazioni su aspetti delle query [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio il numero dei batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ricevuti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Transactions](sql-server-transactions-object.md)|Offre informazioni sulle transazioni attive in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio il numero totale di transazioni e il numero di transazioni snapshot.|  
|[SQLServer:User Settable](sql-server-user-settable-object.md)|Esegue un monitoraggio personalizzato. Ogni contatore può essere rappresentato da una stored procedure personalizzata o da qualsiasi istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che restituisce un valore da monitorare.|  
|[SQLServer: Le statistiche di attesa](sql-server-wait-statistics-object.md)|Offre informazioni relative alle attese.|  
|[SQLServer: : Statistiche gruppi del carico di lavoro](sql-server-workload-group-stats-object.md)|Offre informazioni sulle statistiche dei gruppi del carico di lavoro di Resource Governor.|  
  
##  <a name="SQLServerReplicationPOs"></a> Oggetti prestazione della replica di SQL Server  
 Nella tabella seguente sono indicati gli oggetti prestazione disponibili per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|**SQLServer:Agenti di replica**<br /><br /> **SQLServer:Replication Snapshot**<br /><br /> **SQLServer:Replication Logreader**<br /><br /> **SQLServer:Replication Dist.**<br /><br /> **SQLServer:Replication Merge**<br /><br /> Per altre informazioni, vedere [Monitoraggio della replica con Monitor di sistema](../replication/monitor/monitoring-replication-with-system-monitor.md).|Offre informazioni relative all'attività dell'agente di replica.|  
  
##  <a name="SsisPipelineCounters"></a> Contatori delle pipeline SSIS  
 Per il contatore **SSIS Pipeline** , vedere [Contatori delle prestazioni](../../integration-services/performance/performance-counters.md).  
  
##  <a name="RequiredPermissions"></a> Autorizzazioni necessarie  
 L'utilizzo degli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende dalle autorizzazioni di Windows, con l'eccezione di **SQLAgent:Alerts**. Per usare **SQLAgent:Alerts** è necessario che gli utenti siano membri del ruolo predefinito del server **sysadmin**.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo degli oggetti prestazioni](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
