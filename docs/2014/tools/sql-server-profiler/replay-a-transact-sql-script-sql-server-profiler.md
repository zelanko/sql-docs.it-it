---
title: Riprodurre uno script Transact-SQL (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5abf22a1201ac927f12ef9e4cfdd1f6d3026d00a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011423"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Riprodurre uno script Transact-SQL (SQL Server Profiler)
  Quando si desidera provare possibili soluzioni a un problema di prestazioni, è possibile utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per riprodurre script [!INCLUDE[tsql](../../includes/tsql-md.md)] e confrontare così le prestazioni prima e dopo aver effettuato le modifiche.  
  
### <a name="to-replay-a-transact-sql-script"></a>Per riprodurre uno script Transact-SQL  
  
1.  Scegliere **Apri** dal menu **File**e quindi **File script**.  
  
2.  Selezionare il file script [!INCLUDE[tsql](../../includes/tsql-md.md)] che si desidera aprire. Verificare che lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] contenga gli eventi necessari per la riproduzione. Per altre informazioni, vedere [Requisiti per la riproduzione](replay-requirements.md).  
  
3.  Scegliere **Avvia** dal menu **Riproduci**e connettersi al server in cui si vuole riprodurre lo script.  
  
4.  Nella finestra di dialogo **Configurazione riproduzione** verificare le impostazioni e quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre le tracce](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
