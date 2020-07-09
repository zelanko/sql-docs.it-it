---
title: Monitorare l'uso del disco | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d1ee155b97823b419623d0296928db5334c71e7f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787472"
---
# <a name="monitor-disk-usage"></a>Monitoraggio dell'utilizzo del disco
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzate le chiamate di input/output (I/O) del sistema operativo Microsoft Windows per eseguire operazioni di lettura e scrittura sul disco. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce i tempi e le modalità di esecuzione delle operazioni di I/O, ma è il sistema operativo Windows a eseguire le operazioni di I/O sottostanti. Il sottosistema di I/O include il bus di sistema, le schede dei controller dei dischi, i dischi, le unità a nastro, l'unità CD-ROM e numerosi altri dispositivi di I/O. L'attività di I/O su disco rappresenta frequentemente la causa di colli di bottiglia in un sistema.  
  
 Il monitoraggio dell'attività del disco si concentra su due aree:  
  
-   Monitoraggio dell'I/O su disco e rilevamento del paging eccessivo  
  
-   Isolamento dell'attività del disco creata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Per altre informazioni, vedere [Monitoraggio dell'utilizzo del disco](https://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx). 
 
 Per altre informazioni su come risolvere i problemi di I/O in SQL Server, vedere [Slow I/O - SQL Server and disk I/O performance](https://techcommunity.microsoft.com/t5/SQL-Server-Support/Slow-I-O-SQL-Server-and-disk-I-O-performance/ba-p/333983) (I/O lento - SQL Server e le prestazioni di I/O del disco).
  
  
