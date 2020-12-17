---
title: Determinare la frequenza di polling
description: Questo articolo illustra come determinare la frequenza di polling per gli avvisi dell'appliance del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee5c83fee1028b7e165db6dfb8015129c29e4eca
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/17/2020
ms.locfileid: "97641478"
---
# <a name="determine-polling-frequency"></a>Determinare la frequenza di polling
Questo articolo illustra come determinare la frequenza di polling per gli avvisi dell'appliance del sistema della piattaforma di analisi.  
  
## <a name="to-determine-the-polling-frequency"></a>Per determinare la frequenza di polling  
Poiché PDW non supporta attualmente le notifiche proattive quando si verificano gli avvisi, la soluzione di monitoraggio deve eseguire continuamente il polling delle dll del dispositivo.  Internamente, PDW esegue il polling dei componenti a intervalli diversi:  
  
-   Cluster-60 secondi  
  
-   Heartbeat-60 secondi  
  
-   Tutti gli altri componenti-cinque minuti  
  
-   Contatori delle prestazioni-tre secondi  
  
Un intervallo comune per eseguire il polling degli avvisi, che viene usato anche da System Center, è **ogni 15 minuti**.  Ovviamente, è possibile eseguire query in modo più o meno frequente, ma non è consigliabile eseguire il polling meno di ogni sei ore.  
  
Il polling più frequente è accettabile, ma il polling troppo spesso può ingombrare il [sys.dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) DMV.  Il polling troppo spesso può rendere difficile per gli utenti la diagnosi dei problemi di prestazioni delle query quando ne viene rapidamente eseguito il rollup.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
