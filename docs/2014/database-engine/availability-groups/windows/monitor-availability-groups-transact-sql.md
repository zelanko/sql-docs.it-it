---
title: Monitorare Gruppi di disponibilità (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- dynamic management views [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], databases
- catalog views [SQL Server], AlwaysOn Availability Groups
ms.assetid: 881a34de-8461-4811-8c62-322bf7226bed
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b97d62e7dede1cbbe4229f824407946f2fe43ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62789820"
---
# <a name="monitor-availability-groups-transact-sql"></a>Monitorare Gruppi di disponibilità (Transact-SQL)
  Per monitorare le repliche e i gruppi di disponibilità e i database associati tramite [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] offre un set di viste del catalogo, di DMV e di proprietà del server. Tramite le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT, è possibile utilizzare le viste per monitorare i gruppi di disponibilità e i relativi database e repliche. Le informazioni restituite per un gruppo di disponibilità variano a seconda che l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui si è connessi ospiti la replica primaria o una replica secondaria.  
  
> [!TIP]  
>  Molte di queste viste possono essere unite tramite le relative colonne ID in modo che le informazioni vengano restituite da più viste in una singola query.  
  
 
  
##  <a name="Permissions"></a> Autorizzazioni  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] richiedono l'autorizzazione VIEW ANY DEFINITION sull'istanza del server. 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] richiedono l'autorizzazione VIEW SERVER STATE sul server.  
  
##  <a name="AoAgFeatureOnSI"></a>Monitoraggio della funzionalità Gruppi di disponibilità AlwaysOn in un'istanza del server  
 Per monitorare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in un'istanza del server, utilizzare la funzione predefinita seguente:  
  
 [ServerProperty](/sql/t-sql/functions/serverproperty-transact-sql) (funzione)  
 Restituisce informazioni sulle proprietà del server in cui è specificato se [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] è abilitato e, in caso affermativo, se è stato avviato sull'istanza del server.  
  
 **Nomi delle colonne:** IsHadrEnabled, HadrManagerStatus  
  
##  <a name="WSFC"></a>Monitoraggio dei gruppi di disponibilità nel cluster WSFC  
 Per monitorare il cluster WSFC (Windows Server Failover Clustering) che ospita un'istanza del server locale abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], utilizzare le viste seguenti:  
  
 [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
 Se il nodo WSFC (Windows Server Failover Clustering) che ospita un'istanza di SQL Server con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] abilitato ha il quorum WSFC, **sys.dm_hadr_cluster** restituisce una riga che espone il nome del cluster e informazioni sul quorum. Se il nodo WSFC non dispone di quorum, non viene restituita alcuna riga.  
  
 **Nomi delle colonne:** cluster_name, quorum_type, quorum_type_desc, quorum_state quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
 Se il nodo WSFC che ospita l'istanza locale AlwaysOn di SQL Server dispone del quorum WSFC, restituisce una riga per ogni membro che costituisce il quorum e lo stato di ognuno di essi.  
  
 **Nomi delle colonne:** member_name, member_type, member_type_desc, member_state, member_state_desc, number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
 Restituisce una riga per ogni membro che partecipa alla configurazione della subnet di un gruppo di disponibilità. È possibile utilizzare questa DMV per convalidare l'indirizzo IP virtuale di rete configurato per ogni replica di disponibilità.  
  
 **Nomi delle colonne:** member_name, network_subnet_ip, network_subnet_ipv4_mask, network_subnet_prefix_length, is_public, is_ipv4  
  
 **Chiave primaria:** member_name + network_subnet_IP + network_subnet_prefix_length  
  
 [sys.dm_hadr_instance_node_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
 Per ogni istanza di SQL Server che ospita una replica di disponibilità che ha creato un join al gruppo di disponibilità AlwaysOn, restituisce il nome del nodo Windows Server Failover Clustering (WSFC) che ospita l'istanza del server. Questa DMV offre i seguenti utilizzi:  
  
-   Questa DMV è utile per il rilevamento di un gruppo di disponibilità con più repliche di disponibilità ospitate nello stesso nodo WSFC. Si tratta di una configurazione non supportata che si potrebbe verificare dopo un failover dell'istanza del cluster di failover se il gruppo di disponibilità non è stato correttamente configurato.  
  
-   Quando più istanze di SQL Server sono ospitate sullo stesso nodo WSFC, la DLL della risorsa utilizza questa DMV per determinare l'istanza di SQL Server a cui connettersi.  
  
 **Nomi delle colonne:** ag_resource_id, instance_name, node_name  
  
 [sys.dm_hadr_name_id_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
 Mostra il mapping dei gruppi di disponibilità AlwaysOn dove per l'istanza corrente di SQL Server è stato creato un join a tre ID univoci: un ID gruppo di disponibilità, un ID risorsa WSFC e un ID gruppo WSFC. Lo scopo di questo mapping è gestire lo scenario in cui il gruppo/risorsa WSFC viene rinominato.  
  
 **Nomi delle colonne:** ag_name, ag_id, ag_resource_id ag_group_id  
  
> [!NOTE]  
>  Vedere anche **sys.dm_hadr_availability_replica_cluster_nodes** e **sys.dm_hadr_availability_replica_cluster_states** nella sezione [Monitoraggio delle repliche di disponibilità](#AvReplicas) e **sys.availability_databases_cluster** e **sys.dm_hadr_database_replica_cluster_states** nella sezione [Monitoraggio dei database di disponibilità](#AvDbs) più avanti in questo argomento.  
  
 Per informazioni sui cluster WSFC e [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Windows Server Failover Clustering &#40;wsfc&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md) e [clustering di failover e gruppi di disponibilità AlwaysOn ](failover-clustering-and-always-on-availability-groups-sql-server.md)&#40;SQL Server&#41;.  
  
##  <a name="AvGroups"></a>Monitoraggio di gruppi di disponibilità  
 Per monitorare i gruppi di disponibilità per cui l'istanza del server ospita una replica di disponibilità, utilizzare le viste seguenti:  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 Restituisce una riga per ogni gruppo di disponibilità per il quale l'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ospita una replica di disponibilità. Ogni riga contiene una copia memorizzata nella cache dei metadati del gruppo di disponibilità.  
  
 **Nomi delle colonne:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 Restituisce una riga per ogni gruppo di disponibilità nel cluster WSFC. Ogni riga contiene i metadati del gruppo di disponibilità del cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomi delle colonne:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference, automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 Restituisce una riga per ogni gruppo di disponibilità che dispone di una replica di disponibilità sull'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ogni riga visualizza gli stati che definiscono l'integrità di un determinato gruppo di disponibilità.  
  
 **:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health, synchronization_health_desc  
  
##  <a name="AvReplicas"></a>Monitoraggio delle repliche di disponibilità  
 Per monitorare le repliche di disponibilità, utilizzare la funzione di sistema e le viste seguenti:  
  
 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
 Restituisce una riga per ogni replica di disponibilità in ogni gruppo di disponibilità per il quale l'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ospita una replica di disponibilità.  
  
 **Nomi delle colonne:** replica_id, group_id, replica_metadata_id, replica_server_name, owner_sid, ENDPOINT_URL, availability_mode, availability_mode_desc, failover_mode, failover_mode_desc, session_timeout, primary_role_allow_connections, primary_role_allow_connections_desc, secondary_role_allow_connections, secondary_role_allow_connections_desc, create_date, modify_date, backup_priority, READ_ONLY_ROUTING_URL  
  
 [sys.availability_read_only_routing_lists](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
 Viene restituita una riga per l'elenco di routing di sola lettura di ogni replica di disponibilità in un gruppo di disponibilità AlwaysOn nel cluster di failover WSFC.  
  
 **Nomi delle colonne:** replica_id, routing_priority, read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
 Restituisce una riga per ogni replica di disponibilità, indipendentemente dallo stato di join, dei gruppi di disponibilità AlwaysOn nel cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomi delle colonne:** group_name, replica_server_name, node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
 Restituisce una riga per ogni replica, indipendentemente dallo stato del join, di tutti i gruppi di disponibilità AlwaysOn, indipendentemente dal percorso della replica, nel cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomi delle colonne:** replica_id, replica_server_name, group_id, join_state join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
 Restituisce una riga in cui viene mostrato lo stato di ogni replica di disponibilità locale e una riga per ogni replica di disponibilità remota nello stesso gruppo di disponibilità.  
  
 **Nomi delle colonne:** replica_id, group_id, is_local, role, role_desc, operational_state, operational_state_desc, connected_state, connected_state_desc, recovery_health, recovery_health_desc, synchronization_health, synchronization_health_desc, last_connect_error_number, last_connect_error_description e last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
 Determina se la replica corrente è la replica di backup preferita.  
  
> [!NOTE]  
>  Per informazioni sui contatori delle prestazioni per le repliche di disponibilità (oggetto prestazioni **SQLServer:Availability Replica**  ), vedere [SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbs"></a>Monitoraggio dei database di disponibilità  
 Per monitorare i database di disponibilità, utilizzare le viste seguenti:  
  
 [sys.availability_databases_cluster](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
 Contiene una riga per ogni database sull'istanza di SQL Server che fa parte di tutti i gruppi di disponibilità AlwaysOn nel cluster, indipendentemente dal fatto che il database della copia locale sia già stato aggiunto o meno al gruppo di disponibilità.  
  
> [!NOTE]  
>  Quando un database viene aggiunto a un gruppo di disponibilità, viene automaticamente creato un join del database primario con il gruppo. È necessario preparare i database secondari su ogni replica secondaria prima di poterne creare un join al gruppo di disponibilità.  
  
 **Nomi delle colonne:** group_id, group_database_id, database_name  
  
 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
 Contiene una riga per ogni database nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se un database appartiene a una replica di disponibilità, la riga per quel database contiene il GUID della replica e l'identificatore univoco del database all'interno del gruppo di disponibilità.  
  
 nomi delle colonne: replica_id, group_database_id ** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] **  
  
 [sys.dm_hadr_auto_page_repair](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
 Restituisce una riga per ogni tentativo di correzione automatica della pagina in qualsiasi database di disponibilità in una replica di disponibilità ospitata per qualsiasi gruppo di disponibilità dall'istanza del server. Questa vista contiene le righe degli ultimi tentativi automatici di correzione automatica della pagina in un database primario o secondario, con un massimo di 100 righe per database. Non appena un database raggiunge il limite massimo, la riga per il tentativo successivo di correzione automatica della pagina sostituisce una delle voci esistenti.  
  
 **Nomi delle colonne:** database_id, file_id, page_id, error_type, page_status, modification_time  
  
 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
 Restituisce una riga per ogni database che partecipa a un qualsiasi gruppo di disponibilità per il quale l'istanza locale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ospita una replica di disponibilità.  
  
 **Nomi delle colonne:** database_id, group_id, replica_id, group_database_id, is_local, synchronization_state, synchronization_state_desc, is_commit_participant, synchronization_health, synchronization_health_desc, database_state, database_state_desc, is_suspended, suspend_reason, suspend_reason_desc, recovery_lsn, truncation_lsn, last_sent_lsn, last_sent_time, last_received_lsn, last_received_time, last_hardened_lsn, last_hardened_time, last_redone_lsn, last_redone_time, log_send_queue_size, log_send_rate, redo_queue_size, redo_rate, filestream_send_rate, end_of_log_lsn, last_commit_lsn, last_commit_time, low_water_mark_for_ghosts  
  
 [sys.dm_hadr_database_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
 Restituisce una riga contenente informazioni relative all'integrità dei database nei database di disponibilità in ciascun gruppo di disponibilità nel cluster WSFC (Windows Server Failover Clustering). Questa DMV è utile per la pianificazione o la risposta a un failover o per comprendere quale replica secondaria di un gruppo di disponibilità trattiene il troncamento del log su un determinato database primario.  
  
 **Nomi delle colonne:** replica_id, group_database_id, database_name, is_failover_ready, is_pending_secondary_suspend, is_database_joined, recovery_lsn truncation_lsn  
  
> [!NOTE]  
>  Il percorso della replica primaria è l'origine autorevole per un gruppo di disponibilità.  
  
> [!NOTE]  
>  Per informazioni sui contatori delle prestazioni di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] per i database di disponibilità (oggetto prestazioni **SQLServer:Database Replica** ), vedere [SQL Server, replica di database](../../../relational-databases/performance-monitor/sql-server-database-replica.md). Inoltre, per monitorare l'attività del log delle transazioni sui database di disponibilità, utilizzare i contatori seguenti dell'oggetto prestazioni **SqlServer: Databases** : **ora di scrittura scaricamento log (MS)**, **Scaricamenti log/sec**, **mancati riscontri cache del pool di log/sec**, **letture disco del pool di log/sec**e **richieste del pool di log/sec**. Per ulteriori informazioni, vedere [SQL Server, oggetto database](../../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
##  <a name="AGlisteners"></a>Monitoraggio di listener del gruppo di disponibilità  
 Per monitorare i listener del gruppo di disponibilità sulle subnet del cluster WSFC, utilizzare le viste seguenti:  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 Restituisce una riga per ogni indirizzo IP virtuale conforme attualmente online per un listener del gruppo di disponibilità.  
  
 **Nomi delle colonne:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 Per un determinato gruppo di disponibilità, restituisce zero righe, cosa che indica che nessun nome di rete è associato al gruppo di disponibilità, oppure restituisce una riga per ogni configurazione del listener del gruppo di disponibilità nel cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomi delle colonne:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 Restituisce una riga contenente informazioni sullo stato dinamico per ogni listener TCP.  
  
 **Nomi delle colonne:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
 **Chiave primaria:** listener_id  
  
 Per informazioni sui listener dei gruppi di disponibilità, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Attività di monitoraggio dei gruppi di disponibilità AlwaysOn:**  
  
-   [Usare Dettagli Esplora oggetti per monitorare i gruppi di disponibilità &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [Visualizzazione delle Proprietà dei gruppi di disponibilità &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Visualizzare le proprietà del listener del gruppo di disponibilità &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
 **Riferimento relativo al monitoraggio dei gruppi di disponibilità AlwaysOn (Transact-SQL):**  
  
-   [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
-   [sys. availability_group_listener_ip_addresses &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
  
-   [sys. availability_group_listeners &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
  
-   [sys. availability_databases_cluster &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
  
-   [sys. availability_groups &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
  
-   [sys. availability_read_only_routing_lists &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys. availability_replicas &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_nodes &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_states &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
-   [sys. dm_hadr_auto_page_repair &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
  
-   [sys.dm_hadr_availability_group_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_states &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys.dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys. dm_hadr_database_replica_cluster_states &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys. dm_hadr_cluster &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
  
-   [sys. dm_hadr_cluster_members &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
  
-   [sys. dm_hadr_cluster_networks &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
  
-   [sys. dm_hadr_database_replica_cluster_states &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys.dm_hadr_database_replica_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys. dm_hadr_instance_node_map &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
  
-   [sys. dm_hadr_name_id_map &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
  
-   [sys. dm_os_performance_counters &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
-   [sys. dm_tcp_listener_states &#40;&#41;Transact-SQL](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
  
-   [sys. fn_hadr_backup_is_preferred_replica &#40;&#41;Transact-SQL](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **Contatori delle prestazioni AlwaysOn:**  
  
-   [SQL Server, replica di disponibilità](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server, replica di database](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server, oggetto di database](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **Gestione basata su criteri per gruppi di disponibilità AlwaysOn**  
  
-   [Utilizzare i criteri AlwaysOn per visualizzare l'integrità di un gruppo di disponibilità &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usare il dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di disponibilità AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoraggio di Gruppi di disponibilità &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
