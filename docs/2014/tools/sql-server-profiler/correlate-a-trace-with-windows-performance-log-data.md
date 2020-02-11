---
title: Correlare una traccia con i dati del log delle prestazioni di Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3c8a3d7a9888423d312d578784e1f7e1ff75434d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63316305"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Correlare una traccia con i dati del log delle prestazioni di Windows
  
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]consente di aprire un log delle prestazioni di Microsoft Windows, scegliere i contatori da correlare a una traccia e visualizzare i contatori delle prestazioni selezionati insieme alla traccia nell'interfaccia utente grafica di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Quando si seleziona un evento nella finestra della traccia, una barra rossa verticale nel riquadro della finestra dei dati di Monitoraggio di sistema di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica i dati del log delle prestazioni correlati all'evento di traccia selezionato.  
  
 Per correlare una traccia con i contatori delle prestazioni, aprire un file di traccia o una tabella contenente le colonne di dati **StartTime** e **EndTime** data columns, e then click **Importa dati prestazioni** dal menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu. È quindi possibile aprire un log delle prestazioni e selezionare gli oggetti e i contatori di Monitoraggio di sistema da correlare alla traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Correlare una traccia con i dati del log delle prestazioni di Windows &#40;SQL Server Profiler&#41;](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
