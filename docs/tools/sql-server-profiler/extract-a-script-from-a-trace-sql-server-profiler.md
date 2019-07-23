---
title: Estrarre uno script da una traccia (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c2ee53261681cbcebd023bef75b98124a24d383
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223693"
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>Estrarre uno script da una traccia (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento vengono descritti l'estrazione di eventi [!INCLUDE[tsql](../../includes/tsql-md.md)] da un file o da una tabella di traccia e il relativo salvataggio come file script [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>Per estrarre uno script Transact-SQL da un file o una tabella di traccia  
  
1.  Aprire il file o la tabella di traccia contenente gli eventi [!INCLUDE[tsql](../../includes/tsql-md.md)] che si desidera salvare in un file script [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per altre informazioni, vedere [Aprire un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) o Ottimizzazione guidata [Aprire una tabella di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
2.  Nel menu **File** scegliere **Esporta**, **Estrai eventi di SQL Server** e quindi **Estrai eventi Transact-SQL**.  
  
3.  Nella finestra di dialogo **Salva con nome** digitare un nome per il file [!INCLUDE[tsql](../../includes/tsql-md.md)] e quindi fare clic su **Salva**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
