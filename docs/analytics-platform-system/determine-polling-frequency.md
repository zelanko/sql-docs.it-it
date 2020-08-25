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
ms.openlocfilehash: cafd18a7701ed5de5018a3e8dc23bc8d5d9640fa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767040"
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
  
Il polling più frequente è accettabile, ma il polling troppo spesso può ingombrare la DMV [sys. dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) .  Il polling troppo spesso può rendere difficile per gli utenti la diagnosi dei problemi di prestazioni delle query quando ne viene rapidamente eseguito il rollup.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
