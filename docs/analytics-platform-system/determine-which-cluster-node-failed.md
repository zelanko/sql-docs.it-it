---
title: Determinare il nodo di cluster non riuscita - sistema di piattaforma Analitica | Microsoft Docs
description: Questo articolo descrive come determinare il nome del nodo Analitica Platform System (APS) che non è riuscita dopo un failover del cluster si è verificato e ha generato un avviso di failover cluster. Come parte della risoluzione dei problemi relativi a un cluster di failover, è necessario determinare il nome del nodo che non è riuscito prima di contattare Microsoft per contribuire a risolvere il problema.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4fd739e55725a3138a22539ef837088f86c8d8b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283150"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>Determinare quale cluster nodo non è riuscita per il sistema di piattaforma Analitica
Questo argomento descrive come determinare il nome del nodo Analitica Platform System (APS) che non è riuscita dopo un failover del cluster si è verificato e ha generato un avviso di failover cluster. Come parte della risoluzione dei problemi relativi a un cluster di failover, è necessario determinare il nome del nodo che non è riuscito prima di contattare Microsoft per contribuire a risolvere il problema.  
  
## <a name="Background"></a>In background  
Per la disponibilità elevata in SQL Server PDW il nodo di controllo e i nodi di calcolo vengono configurati come attivi o passivi componenti del cluster di failover di Windows. Quando un server attivo non riesce a rispondere alle richieste di sistema critiche, il server passivo viene eseguito il failover ed esegue le funzioni del server che non è riuscita.  
  
Dopo il failover del cluster, quando SQL Server PDW segnala lo stato del nodo, nel server passivo è un'operazione tramite lo stato. Tuttavia, non è ovvio quale server o un nodo non è riuscita, soprattutto se il server non è ancora online. Per risolvere l'errore del cluster, è necessario determinare il nome del nodo in cui è stato eseguito il failover.  
  
## <a name="AdminConsoleSolution"></a>Soluzione di Console di amministrazione  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Per trovare il nome del nodo che non è riuscita  
  
1.  Aprire la Console di amministrazione. Per altre informazioni sulla Console di amministrazione, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md). Dopo il failover, l'evento di failover è incluso nel numero di avvisi sul **integrità** pagina. È presente un' **integrità** pagina per l'area PDW e per l'area di fabric dell'appliance. Ogni pagina di integrità contiene un **avvisi** scheda. Per altre informazioni su un avviso, fare clic sulla pagina di integrità, scheda Avvisi e quindi fare clic su un avviso.  
  
## <a name="SystemView"></a>Soluzione di vista di sistema  
L'istruzione SQL seguente viene illustrato come utilizzare il [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) vista di sistema per trovare il nome del server che non è riuscita.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
