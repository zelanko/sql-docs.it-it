---
title: Operazioni asincrone
description: Viene descritto come eseguire operazioni di database asincrone usando un'API basata sul modello asincrono usato da .NET Framework.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452328"
---
# <a name="asynchronous-operations"></a>Operazioni asincrone

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Alcune operazioni del database, ad esempio le esecuzioni dei comandi, possono richiedere molto tempo per essere completate. In tal caso, le applicazioni a thread singolo devono bloccare altre operazioni e attendere il completamento del comando prima di poter continuare le proprie operazioni. Invece, la possibilità di assegnare un'operazione con esecuzione prolungata a un thread in background consente di mantenere attivo il thread in primo piano per tutta l'operazione. In un'applicazione Windows, ad esempio, la delega dell'operazione a esecuzione prolungata a un thread in background consente al thread dell'interfaccia utente di rimanere attivo mentre l'operazione è in esecuzione.  
  
.NET offre diversi modelli di progettazione asincrona standard che possono essere utilizzati dagli sviluppatori per sfruttare i vantaggi dei thread in background e liberare l'interfaccia utente o i thread con priorità alta per completare altre operazioni nella classe <xref:Microsoft.Data.SqlClient.SqlCommand>. In particolare, i metodi <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, abbinati ai metodi <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, forniscono il supporto asincrono.  
  
> [!NOTE]
>  La programmazione asincrona è una funzionalità di base di .NET. Per ulteriori informazioni sulle diverse tecniche asincrone disponibili per gli sviluppatori, vedere [chiamata asincrona dei metodi sincroni](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously).  
  
Sebbene l'utilizzo di tecniche asincrone con le funzionalità di ADO.NET non aggiunga particolari considerazioni, è importante conoscere i vantaggi e le insidie della creazione di applicazioni multithreading. Gli esempi riportati in questa sezione indicano diversi aspetti importanti che gli sviluppatori dovranno tenere in considerazione durante la creazione di applicazioni che incorporano funzionalità multithread.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Applicazioni Windows tramite callback](windows-applications-callbacks.md)  
Viene fornito un esempio che illustra come eseguire un comando asincrono in modo sicuro, gestendo correttamente l'interazione con un modulo e il relativo contenuto da un thread separato.  
  
[Applicazioni ASP.NET tramite handle di attesa](aspnet-apps-use-wait-handles.md)  
Viene fornito un esempio che illustra come eseguire più comandi simultanei da una pagina ASP.NET, usando gli handle di attesa per gestire l'operazione al completamento di tutti i comandi.  
  
[Polling in applicazioni console](poll-console-applications.md)  
Viene fornito un esempio che illustra l'uso del polling per attendere il completamento dell'esecuzione di un comando asincrono da un'applicazione console. Questa tecnica è valida anche in una libreria di classi o in un'altra applicazione senza interfaccia utente.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
- [Chiamata asincrona di metodi sincroni](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
