---
title: Filtrare gli eventi in base all'ora di inizio (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event start times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: aa61ce726ce3e0610a3c1db8337c36054dc1b9e7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729954"
---
# <a name="filter-events-based-on-the-event-start-time-sql-server-profiler"></a>Filtrare gli eventi in base all'ora di inizio (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritta la procedura per filtrare gli eventi di traccia in base all'ora di inizio mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-an-event-based-on-the-event-start-time"></a>Per filtrare un evento in base all'ora di inizio  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia**.  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione**è selezionata, la finestra di dialogo **Proprietà traccia**non viene visualizzata e viene invece avviata la traccia. Per disabilitare questa impostazione, scegliere **Opzioni**dal menu **Strumenti**e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione** .  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Nell'elenco dei nomi di **modello**selezionare un modello di traccia.  
  
4.  Facoltativamente, specificare una destinazione per i risultati della traccia.  
  
5.  Nella scheda **Selezione eventi**fare clic sull'intestazione di colonna **StartTime** . È inoltre possibile fare clic con il pulsante destro del mouse sull'intestazione di colonna e quindi scegliere **Modifica filtro colonne** per avviare la finestra di dialogo **Modifica filtro** .  
  
6.  Espandere **Maggiore di** o **Minore di**e quindi immettere un valore **datetime** nel campo visualizzato sotto l'operatore di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
