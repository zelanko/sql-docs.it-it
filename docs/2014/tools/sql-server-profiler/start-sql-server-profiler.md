---
title: Avvia SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a3219168a070a9c264d4fb5457f9e5844734844a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68186119"
---
# <a name="start-sql-server-profiler"></a>Avviare SQL Server Profiler
  È possibile avviare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] in diversi modi per supportare la raccolta dell'output di traccia in numerosi scenari. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] può essere avviato dal menu **Start** , dal menu **Strumenti** in Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] e da diverse posizioni all'interno di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Quando si avvia [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per la prima volta e si sceglie **Nuova traccia** dal menu **File **, l'applicazione visualizza la finestra di dialogo** Connetti al server[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è possibile specificare l'istanza di** alla quale si vuole connettersi.  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>Per avviare SQL Server Profiler dal menu Start  
  
1.  Scegliere **Tutti i programmi** dal menu **Start**, selezionare [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], scegliere **Strumenti per le prestazioni**e fare clic su **SQL Server Profiler**.  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>Per avviare SQL Server Profiler in Ottimizzazione guidata motore di database  
  
1.  Selezionare [!INCLUDE[ssDE](../../includes/ssde-md.md)] SQL Server Profiler **dal menu** Tools **di Ottimizzazione guidata**.  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>Avvio di SQL Server Profiler in Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] avvia ogni sessione del profiler nella rispettiva istanza e continua l'esecuzione anche dopo l'arresto di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 È possibile avviare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] da diverse posizioni all'interno di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], come illustrato nelle procedure riportate di seguito. Quando viene avviato [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , vengono caricati il contesto di connessione, il modello di traccia e il contesto del filtro del punto di avvio.  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>Per avviare SQL Server Profiler dal menu Strumenti  
  
1.  Dal menu  **Strumenti** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] scegliere **SQL Server Profiler**.  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>Per avviare SQL Server Profiler dall'editor di query  
  
1.  Sulla barra dei menu di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fare clic su **Nuova query**.  
  
2.  In Editor di query fare clic con il pulsante destro del mouse e scegliere **Traccia query in SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Il contesto di connessione è la connessione dell'editor, il modello di traccia è TSQL_SPs e il filtro applicato è SPID = finestra della query SPID.  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>Per avviare SQL Server Profiler da Monitor attività  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e scegliere **Monitoraggio attività**.  
  
2.  Nel riquadro **Processi** fare clic con il pulsante destro del mouse sul processo di cui si vuole modificare il profilo e scegliere **Processo di traccia in SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Quando viene selezionato un processo, il contesto di connessione è la connessione Esplora oggetti stabilita all'apertura di Monitor attività. Il modello di traccia è l'impostazione predefinita basata sul tipo di server e lo SPID corrisponde a quello del processo selezionato.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Nella modalità di autenticazione di Windows l'account utente utilizzato per l'esecuzione di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] deve disporre dell'autorizzazione per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per eseguire tracce con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], gli utenti devono inoltre possedere l'autorizzazione ALTER TRACE.  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Server Profiler](sql-server-profiler.md)   
 [Utilizzo di SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)  
  
  
