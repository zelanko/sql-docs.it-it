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
ms.openlocfilehash: 005fe3d14a7314f7339157064b248a81044a1dfb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401209"
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
  
Il polling più frequente è accettabile, ma il polling troppo spesso può ingombrare la DMV [sys. dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) .  Il polling troppo spesso può rendere difficile per gli utenti la diagnosi dei problemi di prestazioni delle query quando ne viene rapidamente eseguito il rollup.  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoraggio Appliance &#40;sistema piattaforma di analisi&#41;](appliance-monitoring.md)  
  
