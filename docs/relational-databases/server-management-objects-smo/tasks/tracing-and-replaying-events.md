---
title: Traccia e riproduzione di eventi | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f441cceed84b873b31c7d4691b08a541a0aee06f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030166"
---
# <a name="tracing-and-replaying-events"></a>Traccia e riproduzione di eventi
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO i **traccia** e **Replay** gli oggetti nel <xref:Microsoft.SqlServer.Management.Trace> dello spazio dei nomi fornisce l'accesso al [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] funzionalità, che viene usata per monitorare un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. È possibile acquisire e salvare i dati di ogni evento in un file o in una tabella per operazioni di analisi successive. È ad esempio possibile monitorare un ambiente di produzione per verificare le stored procedure che influiscono sulle prestazioni a causa di un'esecuzione troppo lenta.  
  
 Il **traccia** e **Replay** oggetti forniscono un set di oggetti che può essere utilizzato per creare tracce in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Questi oggetti possono essere utilizzati all'interno di applicazioni personalizzate per creare tracce in modo manuale per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Inoltre, SMO **traccia** oggetti possono essere utilizzati per leggere i file di traccia SQL e le tabelle che sono state create monitorando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], o la registrazione DTS.  
  
 SMO **traccia** oggetti consentono di eseguire le attività seguenti:  
  
-   Creare una traccia.  
  
-   Impostare i filtri nella traccia.  
  
-   Impostare gli eventi per la traccia.  
  
-   Avviare o arrestare una traccia.  
  
-   Leggere file di traccia e tabelle di traccia.  
  
-   Ottenere informazioni sugli eventi in una traccia.  
  
-   Ottenere informazioni sui filtri in una traccia.  
  
-   Modificare i dati di traccia a livello di programmazione.  
  
-   Scrivere file di traccia e tabelle di traccia.  
  
-   Riprodurre file di traccia o tabelle di traccia.  
  
 Dati di traccia le **traccia** e **Replay** oggetti possono essere utilizzati dall'applicazione SMO o possono essere esaminato manualmente mediante [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). I dati di traccia sono anche compatibili con il [traccia SQL](../../../relational-databases/sql-trace/sql-trace.md) stored procedure che forniscono anche le funzionalità di traccia.  
  
 Gli oggetti di traccia SMO risiedono nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Trace>, che richiede un riferimento al file Microsoft.SQLServer.ConnectionInfo.dll.  
  
 Il **traccia** e **Replay** oggetti richiedono una [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> per stabilire una connessione all'istanza di oggetto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) risiede nell'oggetto il [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common) dello spazio dei nomi, che richiede un riferimento al file ConnectionInfo.  
  
> [!NOTE]  
>  Il **traccia** e **Replay** oggetti non sono supportati su una piattaforma a 64 bit.  
  
  
