---
title: Riprodurre un solo evento alla volta (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c36aafe3a01a48f7623fa1d2871428ee3bea390
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63240464"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>Riprodurre un solo evento alla volta (SQL Server Profiler)
  In questo argomento viene illustrato come riprodurre un evento alla volta in un file o tabella di traccia di riproduzione utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-replay-a-single-event-at-a-time"></a>Per riprodurre un solo evento alla volta  
  
1.  Aprire il file o la tabella di traccia che si desidera riprodurre. Per altre informazioni, vedere [Aprire un file di traccia &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) o Ottimizzazione guidata [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Verificare che il file o la tabella di traccia aperta contenga le classi di evento necessarie per la riproduzione. Per altre informazioni, vedere [Requisiti per la riproduzione](replay-requirements.md).  
  
2.  Scegliere **Passaggio** dal menu **Riproduci**e quindi connettersi all'istanza del server in cui si vuole riprodurre la traccia.  
  
3.  Nella finestra di dialogo **Configurazione riproduzione** verificare le impostazioni e quindi fare clic su **OK**. Per altre informazioni sulla specifica delle impostazioni nella finestra di dialogo **Configurazione riproduzione**, vedere [Riprodurre un file di traccia &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md) o [Riprodurre una tabella di traccia &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md).  
  
4.  Per riprodurre il primo evento, fare clic su **OK** nella finestra di dialogo **Configurazione riproduzione** .  
  
5.  Per riprodurre gli eventi successivi, scegliere **Passaggio** dal menu **Riproduci**oppure premere F10. Fare di nuovo clic su **Passaggio** oppure premere di nuovo F10 per ogni evento.  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre le tracce](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
