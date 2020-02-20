---
title: Machine Learning Services (Python, R)
titleSuffix: SQL Server Big Data Clusters
description: Informazioni su come eseguire script Python e R nell'istanza master di cluster Big Data di SQL Server con Machine Learning Services.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75252031"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>Eseguire script Python e R con Machine Learning Services in cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

È possibile eseguire script Python e R nell'istanza master di [cluster Big Data di SQL Server](big-data-cluster-overview.md) con [Machine Learning Services](../advanced-analytics/index.yml).

> [!NOTE]
> Usando le [estensioni del linguaggio di SQL Server](../language-extensions/language-extensions-overview.md) è possibile anche eseguire codice Java sull'istanza master. Con la procedura seguente verranno abilitate anche le estensioni del linguaggio.

## <a name="enable-machine-learning-services"></a>Abilitare Machine Learning Services

Machine Learning Services viene installato nei cluster Big Data per impostazione predefinita e non richiede un'installazione separata.

Per abilitare Machine Learning Services, eseguire questa istruzione sull'istanza master:

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>Abilita gruppi di disponibilità AlwaysOn

Se si usano cluster Big Data di SQL Server con [gruppi di disponibilità Always On](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md), è necessario eseguire alcuni passaggi aggiuntivi per abilitare Machine Learning Services.

1. Connettersi all'istanza master ed eseguire l'istruzione seguente:

    ```sql
    SELECT @@SERVERNAME
    ```

    Annotare il nome del server. In questo esempio, il nome del server relativo all'istanza master è **master-2**.

1. In ogni replica presente nel gruppo di disponibilità Always On del cluster Big data, eseguire questi comandi `kubectl`:

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    L'output dovrebbe essere simile al seguente:
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. Connettersi a ogni endpoint della replica master e abilitare l'esecuzione dello script.

    Eseguire l'istruzione seguente:

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

È ora possibile eseguire script Python e R nell'istanza master di cluster Big Data. Vedere gli argomenti di avvio rapido seguenti per eseguire il primo script.

## <a name="next-steps"></a>Passaggi successivi

+ [Avvio rapido: Creare ed eseguire semplici script Python con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in Python con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [Avvio rapido: Creare ed eseguire semplici script R con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in R con SQL Server Machine Learning Services](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
