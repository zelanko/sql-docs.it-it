---
title: Governance delle risorse per l'esecuzione di script R e Python
description: Allocare memoria RAM, CPU e i/o per i carichi di lavoro R e Python in SQL Server istanza del motore di database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1a665fd92f630b46351ef96cc203c9bbf71f54a2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345141"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Governance delle risorse per Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Gli algoritmi di Data Science e di Machine Learning sono a elevato utilizzo di calcolo. A seconda delle priorità del carico di lavoro, potrebbe essere necessario aumentare le risorse disponibili per data science o ridurre la capacità di riapprovvigionamento se l'esecuzione di script R e Python compromette le prestazioni di altri servizi in esecuzione simultanea. 

Quando è necessario ribilanciare la distribuzione delle risorse di sistema tra più carichi di lavoro, è possibile usare [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) per allocare CPU, i/o fisico e risorse di memoria utilizzate dai runtime esterni per R e Python. Se si spostano le allocazioni delle risorse, tenere presente che potrebbe essere necessario ridurre anche la quantità di memoria riservata ad altri carichi di lavoro e servizi. 

> [!NOTE] 
> Resource Governor è una funzionalità di Enterprise Edition.

## <a name="default-allocations"></a>Allocazioni predefinite

Per impostazione predefinita, i runtime di script esterni per Machine Learning sono limitati a non più del 20% della memoria totale del computer. Dipende dal sistema in uso, ma in generale è possibile che questo limite non sia adeguato per attività di apprendimento automatico gravi, ad esempio per il training di un modello o per la stima di molte righe di dati. 

## <a name="use-resource-governor-to-control-resourcing"></a>Usare Resource Governor per controllare la Resourcing
 
Per impostazione predefinita, i processi esterni utilizzano fino al 20% della memoria totale dell'host nel server locale. È possibile modificare il pool di risorse predefinito per apportare modifiche a livello di server, con processi R e Python che usano la capacità disponibile per i processi esterni.

In alternativa, è possibile creare *pool di risorse esterne*personalizzati, con i gruppi di carico di lavoro e i classificatori associati, per determinare l'allocazione delle risorse per le richieste provenienti da programmi specifici, da host o da altri criteri forniti. Un pool di risorse esterne è un tipo di pool di risorse [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] introdotto in per semplificare la gestione dei processi R e Python esterni al motore di database.

1. [Abilita governance delle risorse](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (è disattivato per impostazione predefinita).

2. Eseguire [Crea pool di risorse esterne](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) per creare e configurare il pool di risorse, seguito da [ALTER Resource Governor](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) per implementarlo.

3. Creare un gruppo di carico di lavoro per le allocazioni granulari, ad esempio tra il training e il punteggio.

4. Creare un classificatore per intercettare le chiamate per l'elaborazione esterna.

5. Eseguire query e procedure usando gli oggetti creati.

Per una procedura dettagliata, vedere [come creare un pool di risorse per gli script R e Python esterni](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) per istruzioni dettagliate.

Per un'introduzione alla terminologia e ai concetti generali, vedere [Resource Governor pool di risorse](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processi con governance delle risorse
  
 È possibile utilizzare un *pool di risorse esterno* per gestire le risorse utilizzate dai seguenti file eseguibili in un'istanza del motore di database:

+ Rterm. exe quando viene chiamato localmente da SQL Server o chiamato in remoto con SQL Server come contesto di calcolo remoto
+ Python. exe quando viene chiamato localmente da SQL Server o chiamato in remoto con SQL Server come contesto di calcolo remoto
+ BxlServer.exe e processi satellite
+ Processi satellite avviati da Launchpad, ad esempio PythonLauncher. dll
  
> [!NOTE]
> La gestione diretta del servizio Launchpad usando Resource Governor non è supportata. Launchpad è un servizio attendibile che può ospitare solo i lanci forniti da Microsoft. I lanci attendibili sono configurati in modo esplicito per evitare l'utilizzo di risorse eccessive.
  
## <a name="see-also"></a>Vedere anche

+ [Gestire l'integrazione di Machine Learning](../r/managing-and-monitoring-r-solutions.md)
+ [Creare un pool di risorse per Machine Learning](../r/how-to-create-a-resource-pool-for-r.md)
+ [Pool di risorse Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
