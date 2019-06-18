---
title: Riprodurre uno script Transact-SQL (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
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
manager: craigg
ms.openlocfilehash: 6b85c31fcaad26d6cc8604764e37d8aa32d58610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712355"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Riprodurre uno script Transact-SQL (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si desidera provare possibili soluzioni a un problema di prestazioni, è possibile utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per riprodurre script [!INCLUDE[tsql](../../includes/tsql-md.md)] e confrontare così le prestazioni prima e dopo aver effettuato le modifiche.  
  
### <a name="to-replay-a-transact-sql-script"></a>Per riprodurre uno script Transact-SQL  
  
1.  Scegliere **Apri** dal menu **File**e quindi **File script**.  
  
2.  Selezionare il file script [!INCLUDE[tsql](../../includes/tsql-md.md)] che si desidera aprire. Verificare che lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] contenga gli eventi necessari per la riproduzione. Per altre informazioni, vedere [Requisiti per la riproduzione](../../tools/sql-server-profiler/replay-requirements.md).  
  
3.  Scegliere **Avvia** dal menu **Riproduci**e connettersi al server in cui si vuole riprodurre lo script.  
  
4.  Nella finestra di dialogo **Configurazione riproduzione** verificare le impostazioni e quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre le tracce](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
