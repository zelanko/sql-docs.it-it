---
title: Tenere traccia degli avvisi dell'appliance
description: Rilevare gli avvisi del dispositivo nel sistema della piattaforma Analytics.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399947"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Rilevare gli avvisi del dispositivo nel sistema della piattaforma Analytics
Questo argomento illustra come usare la console di amministrazione e le viste di sistema per tenere traccia degli avvisi in un'appliance SQL Server PDW.  
  
## <a name="to-track-appliance-alerts"></a>Per tenere traccia degli avvisi dell'appliance  
SQL Server PDW crea avvisi per problemi hardware e software che richiedono attenzione. Ogni avviso contiene un titolo e una descrizione del problema.  
  
SQL Server PDW registra gli avvisi nella DMV [sys. dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) . Il sistema mantiene un limite di 10.000 avvisi ed Elimina prima di tutto l'avviso meno recente quando viene superato il limite.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Visualizzare gli avvisi tramite la console di amministrazione  
È disponibile una scheda **avvisi** per l'area PDW e per l'area dell'infrastruttura del dispositivo. Quando si verifica il failover, l'evento di failover viene incluso nel numero di avvisi nella pagina. È disponibile una pagina per l'area PDW e per l'area dell'infrastruttura del dispositivo. Ogni pagina di integrità contiene una scheda. Per ulteriori informazioni su un avviso, fare clic sulla pagina **stato** , sulla scheda **avvisi** , quindi fare clic su un avviso.  
  
![Avvisi della console di amministrazione di PDW](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
Nella pagina **avvisi** :  
  
-   Per visualizzare la cronologia degli avvisi, fare clic sul collegamento **esaminare la cronologia degli avvisi** .  
  
-   Per visualizzare il componente avviso e i relativi valori di proprietà correnti, fare clic sulla riga di avviso.  
  
-   Per visualizzare i dettagli relativi al nodo che ha generato l'avviso, fare clic sul nome del nodo.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Visualizzare gli avvisi tramite le viste di sistema  
Per visualizzare gli avvisi tramite le viste di sistema, eseguire una query su [sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Questa DMV Mostra gli avvisi che non sono stati corretti. Per informazioni sugli avvisi e gli errori di Triaging, utilizzare la DMV [sys. dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) .  
  
L'esempio seguente è una query comune per la visualizzazione degli avvisi correnti.  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
  
