---
title: Visualizzare le proprietà del listener del gruppo di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdec432699b7d0a6152509ec6a53ddf452376d5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788027"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>Visualizzare le proprietà del listener del gruppo di disponibilità (SQL Server)
  In questo argomento viene illustrato come visualizzare le proprietà di un *listener del gruppo di disponibilità* AlwaysOn tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Per visualizzare le proprietà del listener utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per visualizzare le proprietà del listener**  
  
1.  In Esplora oggetti connettersi a un'istanza del server che ospita una replica di disponibilità del gruppo di disponibilità di cui si desidera visualizzare il listener. Fare clic sul nome del server per espandere il relativo albero.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Espandere il nodo del gruppo di disponibilità ed espandere il nodo **Listener gruppo di disponibilità** .  
  
4.  Fare clic con il pulsante destro del mouse sul listener da visualizzare e scegliere il comando **Proprietà** .  
  
5.  Verrà aperta la finestra di dialogo **Proprietà listener gruppo di disponibilità** . Per altre informazioni, vedere [Proprietà listener gruppo di disponibilità (finestra di dialogo)](#AgListenerPropertiesDialog), più avanti in questo argomento.  
  
###  <a name="AgListenerPropertiesDialog"></a> Proprietà listener gruppo di disponibilità (finestra di dialogo)  
 **Nome DNS del listener**  
 Nome di rete del listener del gruppo di disponibilità.  
  
 **Porta**  
 Porta TCP usata dal listener.  
  
> [!NOTE]  
>  Se la replica primaria è connessa, è possibile utilizzare il campo per modificare il numero di porta del listener. È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
 **Modalità di rete**  
 Indica il protocollo TCP utilizzato dal listener. È possibile scegliere uno dei seguenti valori:  
  
 **DHCP**  
 Il listener utilizza un indirizzo IP dinamico assegnato da un server in cui viene eseguito il protocollo DHCP (Dynamic Host Configuration Protocol).  
  
 **Indirizzo IP statico**  
 Il listener utilizza uno o più indirizzi IP statici. Per accedere ad altre subnet, è necessario che un listener del gruppo di disponibilità utilizzi indirizzi IP statici.  
  
 Nella griglia vengono visualizzate le subnet in cui il listener è in attesa e l'indirizzo IP associato a ciascuna subnet.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per visualizzare le proprietà del listener**  
  
 Per monitorare i listener del gruppo di disponibilità, utilizzare le viste seguenti:  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 Restituisce una riga per ogni indirizzo IP virtuale conforme attualmente online per un listener del gruppo di disponibilità.  
  
 **Nomi delle colonne:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 Per un determinato gruppo di disponibilità, restituisce zero righe, cosa che indica che nessun nome di rete è associato al gruppo di disponibilità, oppure restituisce una riga per ogni configurazione del listener del gruppo di disponibilità nel cluster WSFC (Windows Server Failover Clustering).  
  
 **Nomi delle colonne:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 Restituisce una riga contenente informazioni sullo stato dinamico per ogni listener TCP.  
  
 **Nomi delle colonne:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
> [!NOTE]  
>  Per altre informazioni sull'uso di [!INCLUDE[tsql](../../../includes/tsql-md.md)] per monitorare l'ambiente di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , vedere [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Rimuovere un listener del gruppo di disponibilità &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
