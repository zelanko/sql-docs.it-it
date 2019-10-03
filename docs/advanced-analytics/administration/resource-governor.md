---
title: Gestire i carichi di lavoro Python e R con Resource Governor
description: Informazioni su come usare Resource Governor per gestire l'allocazione di CPU, i/o fisico e risorse di memoria per carichi di lavoro Python e R in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9000ab8bb15e8f9910b8b780aa38d134fa984032
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823540"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>Gestire i carichi di lavoro Python e R con Resource Governor in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Informazioni su come usare [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) per gestire l'allocazione di CPU, i/o fisico e risorse di memoria per carichi di lavoro Python e R in SQL Server Machine Learning Services.

Gli algoritmi di Machine Learning in Python e R sono in genere a elevato utilizzo di calcolo. A seconda delle priorità del carico di lavoro, potrebbe essere necessario aumentare o ridurre le risorse disponibili per Machine Learning Services.

Per informazioni più generali, vedere [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

> [!NOTE] 
> Resource Governor è una funzionalità di Enterprise Edition.

## <a name="default-allocations"></a>Allocazioni predefinite

Per impostazione predefinita, i runtime di script esterni per Machine Learning sono limitati a non più del 20% della memoria totale del computer. Dipende dal sistema in uso, ma in generale è possibile che questo limite non sia adeguato per attività di apprendimento automatico gravi, ad esempio per il training di un modello o per la stima di molte righe di dati. 

## <a name="manage-resources-with-resource-governor"></a>Gestire le risorse con Resource Governor
 
Per impostazione predefinita, i processi esterni utilizzano fino al 20% della memoria totale dell'host nel server locale. È possibile modificare il pool di risorse predefinito per apportare modifiche a livello di server, con processi R e Python che usano la capacità disponibile per i processi esterni.

In alternativa, è possibile creare **pool di risorse esterne**personalizzati, con i gruppi di carico di lavoro e i classificatori associati, per determinare l'allocazione delle risorse per le richieste provenienti da programmi specifici, da host o da altri criteri forniti. Un pool di risorse esterne è un tipo di pool di risorse [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] introdotto in per semplificare la gestione dei processi R e Python esterni al motore di database.

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
  
## <a name="next-steps"></a>Passaggi successivi

+ [Creare un pool di risorse per Machine Learning](create-external-resource-pool.md)
+ [Pool di risorse Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
