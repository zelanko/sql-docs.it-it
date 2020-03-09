---
title: Operazioni asincrone
description: Viene descritto come eseguire operazioni di database asincrone usando un'API basata sul modello asincrono usato da .NET Framework.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bc2a921e3aec0068c11b2baab45c396d853a1a36
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897057"
---
# <a name="asynchronous-operations"></a>Operazioni asincrone

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Per il completamento di alcune operazioni del database, ad esempio le esecuzioni di comandi, può essere richiesto molto tempo. In questi casi usare le applicazioni a thread singolo per bloccare le altre operazioni e attendere il completamento del comando prima di riprenderle. Invece, la possibilità di assegnare un'operazione con esecuzione prolungata a un thread in background consente di mantenere attivo il thread in primo piano per tutta l'operazione. In un'applicazione Windows, ad esempio, la delega dell'operazione con esecuzione prolungata a un thread in background consente al thread dell'interfaccia utente di rimanere reattivo mentre viene eseguita l'operazione.  
  
.NET offre diversi modelli di progettazione asincrona standard che possono essere usati dagli sviluppatori per sfruttare i vantaggi dei thread in background e liberare l'interfaccia utente o i thread con priorità elevata per completare altre operazioni nella classe <xref:Microsoft.Data.SqlClient.SqlCommand>. In particolare, i metodi <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, abbinati ai metodi <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, offrono il supporto asincrono.  
  
> [!NOTE]
>  La programmazione asincrona è una funzionalità di base di .NET. Per altre informazioni sulle diverse tecniche asincrone disponibili per gli sviluppatori, vedere [Chiamata di metodi sincroni in modalità asincrona](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously).  
  
Benché l'uso di tecniche asincrone con le funzionalità di ADO.NET non richieda particolari considerazioni, è importante sapere quali sono i vantaggi e le insidie della creazione delle applicazioni multithreading. Gli esempi riportati in questa sezione evidenziano diversi aspetti importanti che gli sviluppatori dovranno tenere in considerazione durante la creazione di applicazioni che incorporano funzionalità multithreading.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Applicazioni Windows tramite callback](windows-applications-callbacks.md)  
Include un esempio che illustra come eseguire un comando asincrono in modo sicuro, gestendo correttamente l'interazione con un modulo e il relativo contenuto da un thread separato.  
  
[Applicazioni ASP.NET tramite handle di attesa](aspnet-apps-use-wait-handles.md)  
Questo documento propone un esempio che spiega come eseguire più comandi simultanei da una pagina ASP.NET, usando gli handle di attesa per gestire l'operazione al completamento di tutti i comandi.  
  
[Polling in applicazioni console](poll-console-applications.md)  
Include un esempio che illustra l'uso del polling per attendere il completamento dell'esecuzione di un comando asincrono da un'applicazione console. Questa tecnica è valida anche in una libreria di classi o in un'altra applicazione senza interfaccia utente.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
- [Chiamata di metodi sincroni in modalità asincrona](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
