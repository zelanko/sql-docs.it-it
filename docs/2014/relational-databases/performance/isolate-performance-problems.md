---
title: Isolare i problemi relativi alle prestazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e700f5178a3520fe83f4d896662a8741aa166b9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150912"
---
# <a name="isolate-performance-problems"></a>Isolare i problemi relativi alle prestazioni
  Per isolare i problemi relativi alle prestazioni del database, è in genere preferibile utilizzare più strumenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o di Microsoft Windows in combinazione, anziché uno per volta. La caratteristica grafica Piano di esecuzione, detta anche Showplan, consente, ad esempio, di individuare in modo semplice deadlock in una singola query. È tuttavia possibile rilevare in modo più semplice altri problemi relativi alle prestazioni utilizzando le caratteristiche di monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows in combinazione.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] può essere utilizzato per monitorare e risolvere i problemi correlati a Transact-SQL e alle applicazioni. Per controllare l'hardware e altri problemi relativi al sistema è possibile utilizzare Monitoraggio di sistema.  
  
 Per risolvere i problemi, è possibile eseguire il monitoraggio degli elementi seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stored procedure o batch di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate da applicazioni utente.  
  
-   Attività degli utenti, ad esempio blocchi o deadlock.  
  
-   Attività hardware, ad esempio utilizzo del disco.  
  
 Tra i problemi che possono verificarsi, sono inclusi i seguenti:  
  
-   Errori di sviluppo delle applicazioni correlati a istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non corrette.  
  
-   Errori hardware, ad esempio errori correlati al disco o alla rete.  
  
-   Un numero eccessivo di blocchi causato da un database progettato in modo non appropriato.  
  
## <a name="tools-for-common-performance-problems"></a>Strumenti per la risoluzione dei problemi comuni relativi alle prestazioni  
 È inoltre importante scegliere con attenzione lo strumento per il monitoraggio o l'ottimizzazione dei problemi relativi alle prestazioni. Lo strumento e l'utilità dipendono dal tipo di problema che si desidera risolvere.  
  
 Negli argomenti seguenti vengono descritti numerosi strumenti di monitoraggio e ottimizzazione e i problemi che tali strumenti consentono di rilevare.  
  
 [Individuare i colli di bottiglia](identify-bottlenecks.md)  
  
 [Monitoraggio dell'utilizzo della memoria](../performance-monitor/monitor-memory-usage.md)  
  
  
