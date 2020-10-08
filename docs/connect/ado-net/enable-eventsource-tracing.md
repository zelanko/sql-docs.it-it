---
title: Abilitazione della traccia eventi in SqlClient
description: Descrive come abilitare la traccia eventi in SqlClient implementando un listener di eventi e come accedere ai dati dell'evento.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725742"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>Abilitazione della traccia eventi in SqlClient

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[Event Tracing for Windows (ETW)](/windows/win32/etw/event-tracing-portal) è un'efficiente funzionalità di traccia a livello di kernel che consente di registrare gli eventi definiti dal driver per scopi di debug e test. SqlClient supporta l'acquisizione di eventi ETW a diversi livelli informativi. Per iniziare ad acquisire questi eventi, le applicazioni client devono restare in ascolto degli eventi dall'implementazione EventSource di SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

L'implementazione corrente supporta le parole chiave degli eventi seguenti:

| Nome parola chiave | Valore | Description |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | Attiva l'acquisizione di eventi di avvio/arresto prima e dopo l'esecuzione del comando. |
| Trace | 2 | Attiva l'acquisizione di eventi di traccia del flusso applicazione di base. |
| Scope | 4 | Attiva l'acquisizione di eventi di ingresso e uscita |
| NotificationTrace | 8 | Attiva l'acquisizione di eventi di traccia di `SqlNotification` |
| NotificationScope | 16 | Attiva l'acquisizione di eventi di ingresso e uscita dell'ambito di `SqlNotification` |
| PoolerTrace | 32 | Attiva l'acquisizione di eventi di traccia del flusso del pool di connessioni |
| PoolerScope | 64 | Attiva l'acquisizione di eventi di traccia dell'ambito del pool di connessioni |
| AdvancedTrace | 128 | Attiva l'acquisizione di eventi di traccia del flusso avanzati |
| AdvancedTraceBin  | 256 | Attiva l'acquisizione di eventi di traccia del flusso avanzati con informazioni aggiuntive |
| CorrelationTrace | 512 | Attiva l'acquisizione di eventi di traccia del flusso di correlazione. |
| StateDump | 1024 | Attiva l'acquisizione del backup dello stato completo di `SqlConnection` |
| SNITrace | 2048 | Attiva l'acquisizione di eventi di traccia del flusso dall'implementazione di rete gestita (applicabile solo in .NET Core) |
| SNIScope | 4096 | Attiva l'acquisizione di eventi dell'ambito dall'implementazione di rete gestita (applicabile solo in .NET Core) |
|||

## <a name="example"></a>Esempio
L'esempio seguente abilita la traccia eventi per un'operazione sui dati nel database di esempio **AdventureWorks** e visualizza gli eventi nella finestra della console.

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="external-resources"></a>Risorse esterne  
Per ulteriori informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[classe EventSource](/dotnet/api/system.diagnostics.tracing.eventsource)|Consente di creare eventi ETW.| 
|[Classe EventListener](/dotnet/api/system.diagnostics.tracing.eventlistener)|Fornisce metodi per abilitare e disabilitare eventi da origini evento.|