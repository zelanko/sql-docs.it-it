---
title: Determinare il nodo del cluster non riuscito
description: Questo articolo descrive come determinare il nome del nodo del sistema di piattaforma di analisi (APS) che ha avuto esito negativo dopo un failover del cluster ed è stato generato un avviso di failover del cluster. Come parte della risoluzione dei problemi relativi a un failover del cluster, è necessario determinare il nome del nodo che ha avuto esito negativo prima di contattare Microsoft per risolvere il problema.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401202"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>Determinare quale nodo del cluster non è riuscito per il sistema di piattaforma di analisi
Questo argomento descrive come determinare il nome del nodo Analytics Platform System (APS) che ha avuto esito negativo dopo il failover di un cluster ed è stato generato un avviso di failover del cluster. Come parte della risoluzione dei problemi relativi a un failover del cluster, è necessario determinare il nome del nodo che ha avuto esito negativo prima di contattare Microsoft per risolvere il problema.  
  
## <a name="Background"></a>Background  
Per la disponibilità elevata in SQL Server PDW, il nodo di controllo e i nodi di calcolo vengono configurati come componenti attivi o passivi dei cluster di failover di Windows. Quando un server attivo non riesce a rispondere alle richieste di sistema critiche, il server passivo esegue il failover ed esegue le funzioni del server non riuscite.  
  
Dopo un failover del cluster, quando SQL Server PDW segnala lo stato del nodo, il server passivo presenta uno stato di failover. Tuttavia, non è ovvio quale server o nodo ha avuto esito negativo, soprattutto se il server che ha avuto esito negativo è ancora in linea. Per risolvere il problema del cluster, è necessario determinare il nome del nodo di cui è stato eseguito il failover.  
  
## <a name="AdminConsoleSolution"></a>Soluzione console di amministrazione  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Per trovare il nome del nodo che ha avuto esito negativo  
  
1.  Aprire la console di amministrazione. Per altre informazioni sulla console di amministrazione, vedere [monitorare l'appliance usando la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md). Al termine del failover, l'evento di failover viene incluso nel numero di avvisi nella pagina di **integrità** . È disponibile una pagina di **integrità** per l'area PDW e per l'area dell'infrastruttura del dispositivo. Ogni pagina di integrità dispone di una scheda **avvisi** . Per ulteriori informazioni su un avviso, fare clic sulla pagina stato, sulla scheda avvisi, quindi fare clic su un avviso.  
  
## <a name="SystemView"></a>Soluzione visualizzazione sistema  
Nell'istruzione SQL seguente viene illustrato come utilizzare la vista di sistema [sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) per individuare il nome del server che ha avuto esito negativo.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
