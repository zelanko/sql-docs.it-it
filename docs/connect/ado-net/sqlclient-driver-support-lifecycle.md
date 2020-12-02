---
title: Ciclo di vita del supporto per il driver SqlClient
description: Pagina che contiene informazioni sul ciclo di vita del supporto tecnico.
ms.date: 11/19/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 30155a584de4e22692601a1dcf9551a67d4f580f
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2020
ms.locfileid: "95011793"
---
# <a name="sqlclient-driver-support-lifecycle"></a>Ciclo di vita del supporto per il driver SqlClient

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La libreria Microsoft.Data.SqlClient segue i criteri di supporto di .NET Core più recenti per tutte le versioni.

[Visualizzare i criteri di supporto di .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

## <a name="microsoftdatasqlclient-release-cadence"></a>Cadenza delle versioni di Microsoft.Data.SqlClient

Le nuove versioni stabili (GA) verranno pubblicate ogni sei mesi con cadenza regolare a partire dalla versione 1.2, oltre a 2-3 versioni di anteprima nel frattempo. Le versioni con supporto a lungo termine (LTS) verranno scelte dagli stakeholder e dai responsabili della manutenzione in base a un numero ridotto di qualifiche e alle risposte dei clienti.

### <a name="release-life-cycles"></a>Cicli di vita delle versioni

| Versione | Data di rilascio ufficiale | Ultima versione patch | Data di rilascio patch | Livello di supporto  | Fine del supporto |
| -- | -- | -- | -- | -- | -- |
| 2.1 | 19 novembre 2020 | 2.1.0 | 19 novembre 2020 | Corrente | |
| 2.0 | 16 giugno 2020 | 2.0.1 | 25 agosto 2020 | Corrente | |
| 1.1 | 20 novembre 2019 | 1.1.3 | 15 maggio 2020 | LTS | 21 novembre 2022 |
| 1,0 | 28 agosto 2019 | 1.0.19269.1 | 26 settembre 2019 | Corrente | 20 febbraio 2020 |

### <a name="long-term-support-lts-releases"></a>Versioni con supporto a lungo termine (LTS)

Le versioni LTS sono supportate per tre anni dopo la versione iniziale.

### <a name="current-releases"></a>Versioni correnti

Le versioni correnti sono supportate per tre mesi dopo una versione corrente o LTS successiva.

## <a name="sql-version-compatibility-with-microsoftdatasqlclient"></a>Compatibilità delle versioni di SQL con Microsoft.Data.SqlClient

|Versione database&nbsp;&#8594;<br />&#8595; Versione del driver|database SQL di Azure|Azure Synapse Analytics|Istanza gestita di SQL di Azure|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|
|---|---|---|---|---|---|---|---|---|
|2.1|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|
|2.0|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|
|1.1|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|
|1.0|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|
