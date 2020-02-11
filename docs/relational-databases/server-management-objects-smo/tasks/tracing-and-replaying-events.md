---
title: Traccia e riproduzione di eventi | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d83b716d9919bf322097b8ded8409950982d961c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148356"
---
# <a name="tracing-and-replaying-events"></a>Traccia e riproduzione di eventi
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO gli oggetti **Trace** e **Replay** nello <xref:Microsoft.SqlServer.Management.Trace> spazio dei nomi forniscono l'accesso programmatico [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] alla funzionalità, che viene utilizzata per il monitoraggio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] un' [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]istanza di o di. È possibile acquisire e salvare i dati di ogni evento in un file o in una tabella per operazioni di analisi successive. È ad esempio possibile monitorare un ambiente di produzione per verificare le stored procedure che influiscono sulle prestazioni a causa di un'esecuzione troppo lenta.  
  
 Gli oggetti **Trace** e **Replay** forniscono un set di oggetti che possono essere utilizzati per creare tracce in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Questi oggetti possono essere utilizzati all'interno di applicazioni personalizzate per creare tracce in modo manuale per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Inoltre, è possibile utilizzare gli oggetti **traccia** SMO per leggere i file di traccia SQL e le tabelle create [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]monitorando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]la registrazione DTS, o.  
  
 Gli oggetti **traccia** Smo consentono di eseguire le funzioni seguenti:  
  
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
  
 I dati di traccia degli oggetti **Trace** e **Replay** possono essere utilizzati dall'applicazione SMO oppure possono essere esaminati manualmente tramite [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). I dati di traccia sono inoltre compatibili con le stored procedure di [traccia SQL](../../../relational-databases/sql-trace/sql-trace.md) che forniscono anche le funzionalità di traccia.  
  
 Gli oggetti di traccia SMO risiedono nello spazio dei nomi <xref:Microsoft.SqlServer.Management.Trace>, che richiede un riferimento al file Microsoft.SQLServer.ConnectionInfo.dll.  
  
 Gli oggetti **Trace** e **Replay** richiedono un oggetto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> per stabilire una connessione con l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'oggetto [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) risiede nello spazio dei nomi [Microsoft. SqlServer. Management. Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common) , che richiede un riferimento al file Microsoft. SqlServer. ConnectionInfo. dll.  
  
> [!NOTE]  
>  Gli oggetti **Trace** e **Replay** non sono supportati in una piattaforma a 64 bit.  
  
  
