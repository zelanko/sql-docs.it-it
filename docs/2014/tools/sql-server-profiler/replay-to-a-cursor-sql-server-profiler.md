---
title: Riproduzione di un cursore (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c4c4b9d2e2e07c53f850fe545d803fa411dbbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267484"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Riprodurre fino a un cursore (SQL Server Profiler)
  In questo argomento viene descritto come sospendere la riproduzione di tabelle o file di traccia in corrispondenza di un cursore utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. La sospensione della riproduzione delle tracce in corrispondenza dei cursori supporta il debug in quanto è possibile interrompere la riproduzione di script di traccia lunghi in segmenti più brevi per eseguirne l'analisi incrementale.  
  
### <a name="to-replay-to-the-cursor"></a>Per eseguire la riproduzione fino al cursore  
  
1.  Aprire il file o la tabella di traccia che si desidera riprodurre. Per altre informazioni, vedere [Aprire un file di traccia &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) o Ottimizzazione guidata [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Verificare che il file o la tabella di traccia aperta contenga le classi di evento necessarie per la riproduzione. Per altre informazioni, vedere [Requisiti per la riproduzione](replay-requirements.md).  
  
2.  Nella finestra di traccia fare clic su un evento.  
  
3.  Scegliere **Esegui fino al cursore** dal menu **Riproduci**e quindi connettersi al server di cui si vuole riprodurre la traccia.  
  
4.  Nella finestra di dialogo **Configurazione riproduzione** verificare le impostazioni e quindi fare clic su **OK**.  
  
     La riproduzione viene avviata e quindi sospesa in corrispondenza del primo cursore.  
  
5.  Premere F5 per riprendere la riproduzione della traccia.  
  
6.  Ripetere l'operazione descritta al passaggio 5 fino alla fine della traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre fino a un punto di interruzione &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [Riprodurre le tracce](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
