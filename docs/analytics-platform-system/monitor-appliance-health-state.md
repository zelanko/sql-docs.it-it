---
title: Monitorare lo stato dell'appliance
description: Come monitorare lo stato di un'appliance del sistema della piattaforma di analisi usando la console di amministrazione o eseguendo direttamente una query sulle viste a gestione dinamica data warehouse parallele.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400996"
---
# <a name="monitor-appliance-health-state"></a>Monitorare lo stato di integrità dell'appliance
Questo articolo illustra come monitorare lo stato di un'appliance del sistema della piattaforma Analytics usando la console di amministrazione o eseguendo direttamente una query sulle viste a gestione dinamica data warehouse parallele. 
  
## <a name="to-monitor-the-appliance-state"></a>Per monitorare lo stato dell'appliance  
Un amministratore di sistema può utilizzare la console di amministrazione o la SQL Server PDW DMV (DMV) per recuperare la gerarchia completa di nodi, componenti e software. Nel diagramma seguente viene illustrata una conoscenza di alto livello dei componenti che SQL Server PDW monitoraggi.  
  
![Panoramica del monitoraggio](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Monitorare lo stato dei componenti tramite la console di amministrazione  
Per recuperare lo stato dei componenti tramite la console di amministrazione:  
  
1.  Fare clic sulla scheda **stato Appliance** .  
  
2.  Nella pagina stato dell'appliance fare clic su un nodo specifico per visualizzare i dettagli del nodo.  
  
    ![Stato della console di amministrazione di PDW](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Monitorare lo stato dei componenti utilizzando viste di sistema  
Per recuperare lo stato dei componenti utilizzando le viste di sistema, utilizzare [sys. dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Ad esempio, la query seguente recupera lo stato di tutti i componenti.  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
I valori possibili restituiti per la proprietà Status sono:  
  
-   OK  
  
-   NonCritical  
  
-   Critico  
  
-   Sconosciuto  
  
-   Non supportato  
  
-   Inaccessibile  
  
-   Irreversibile  
  
Per visualizzare tutte le proprietà di tutti i componenti, rimuovere `WHERE  p.property_name = 'Status'` la clausola.  
  
La colonna **[update_time]** Mostra l'ultima volta in cui il componente è stato sottoporre a polling dagli agenti di SQL Server PDW Health.  
  
> [!CAUTION]  
> Assicurarsi di esaminare il problema quando non è stato eseguito il polling di un componente per 5 minuti o più. potrebbe essere presente un avviso che indica un problema con gli heartbeat software.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
  
