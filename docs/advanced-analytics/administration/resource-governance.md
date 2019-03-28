---
title: Governance delle risorse per l'esecuzione di script R e Python, SQL Server Machine Learning
description: Allocare memoria RAM, CPU e i/o per i carichi di lavoro R e Python nell'istanza di motore di database SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e8b3122f4083d419797abeef5ff96944bac3e6a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512988"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Governance delle risorse per machine learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Analisi scientifica dei dati e algoritmi di machine learning sono notevoli. In base alla priorità del carico di lavoro, potrebbe essere necessario aumentare le risorse disponibili per l'analisi scientifica dei dati o diminuzione precise se l'esecuzione dello script R e Python compromette le prestazioni di altri servizi in esecuzione contemporaneamente. 

Quando è necessario bilanciare nuovamente la distribuzione delle risorse di sistema tra più carichi di lavoro, è possibile usare [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) allocare risorse di CPU, i/o fisico e memoria utilizzate da runtime esterni per R e Python. Se si passa le allocazioni di risorse, tenere presente che potrebbe essere necessario ridurre anche la quantità di memoria riservata per altri carichi di lavoro e i servizi. 

> [!NOTE] 
> Resource Governor è una funzionalità di Enterprise Edition.

## <a name="default-allocations"></a>Allocazioni predefinite

Per impostazione predefinita, i runtime dello script esterno per machine learning sono limitati a non più di 20% della memoria totale del computer. Dipende dal sistema, ma in generale, si potrà trovare questo limite inadeguata per attività di apprendimento automatico gravi, ad esempio un modello di training o la stima su molte righe di dati. 

## <a name="use-resource-governor-to-control-resourcing"></a>Utilizzo di Resource Governor per controllare la ricerca di risorse
 
Per impostazione predefinita, i processi esterni usano fino a 20% della memoria totale host nel server locale. È possibile modificare il pool di risorse predefinito per apportare modifiche a livello di server, con R e i processi Python che usano qualsiasi capacità sarà disponibile per i processi esterni.

In alternativa, è possibile costruire custom *pool di risorse esterne*, con i gruppi di carico di lavoro associato e i classificatori, per determinare l'allocazione delle risorse per le richieste provenienti da programmi specifici, gli host o ad altri criteri che forniscono. Un pool di risorse esterne è un tipo di pool di risorse introdotto in [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] per gestire i processi R e Python esterni al motore di database.

1. [Abilita governance delle risorse](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (è disattivato per impostazione predefinita).

2. Eseguire [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) per creare e configurare il pool di risorse, seguito da [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) implementarla.

3. Creare un gruppo di carico di lavoro per le allocazioni granulare, ad esempio tra il set di training e assegnazione dei punteggi.

4. Creare un classificatore per intercettare le chiamate per l'elaborazione esterna.

5. Eseguire query e procedure utilizzando gli oggetti creati.

Per informazioni dettagliate, vedere [come creare un pool di risorse per gli script R e Python esterni](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) per istruzioni dettagliate.

Per un'introduzione ai concetti generali e la terminologia, vedere [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processi con governance delle risorse
  
 È possibile usare un *pool di risorse esterne* per gestire le risorse usate per i seguenti file eseguibili in un'istanza del motore di database:

+ Rterm.exe quando la chiamata in locale da SQL Server o chiamati in remoto con SQL Server come contesto di calcolo remoto
+ Python.exe quando la chiamata in locale da SQL Server o chiamati in remoto con SQL Server come contesto di calcolo remoto
+ BxlServer.exe e processi satellite
+ Processi satellite avviati da Launchpad, ad esempio PythonLauncher.dll
  
> [!NOTE]
> Gestione diretta del servizio Launchpad con Resource Governor non è supportata. Finestra di avvio è un servizio attendibile che può essere solo host utilità di avvio fornite da Microsoft. Utilità di avvio attendibili sono configurati in modo esplicito per evitare un utilizzo eccessivo di risorse.
  
## <a name="see-also"></a>Vedere anche

+ [Gestire l'integrazione di machine learning](../r/managing-and-monitoring-r-solutions.md)
+ [Creare un pool di risorse per Machine Learning](../r/how-to-create-a-resource-pool-for-r.md)
+ [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
