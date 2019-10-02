---
title: Creare un pool di risorse per Python e R
description: Informazioni su come creare e usare un pool di risorse per la gestione dei carichi di lavoro Python e R in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8e8c48665c2928a0c8133892cc0029b4bd82c4cc
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714325"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>Creare un pool di risorse per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Informazioni su come creare e usare un pool di risorse per la gestione dei carichi di lavoro Python e R in SQL Server Machine Learning Services. 

Il processo include più passaggi:

1. Verificare lo stato di tutti i pool di risorse esistenti. È importante comprendere i servizi che usano le risorse esistenti.
2. Modificare i pool di risorse del server.
3. Creare un nuovo pool di risorse per i processi esterni.
4. Creare una funzione di classificazione per identificare le richieste di script esterni.
5. Verificare che il nuovo pool di risorse esterne acquisisca i processi R o Python dai client o dagli account specificati.

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>Esaminare lo stato dei pool di risorse esistenti
  
1.  Utilizzare un'istruzione come la seguente per controllare le risorse allocate al pool predefinito per il server.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Risultati di esempio**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|predefiniti|0|100|0|100|100|0|0|

2.  Controllare le risorse allocate al pool di risorse **esterno** predefinito.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Risultati di esempio**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|predefiniti|100|20|0|2|
 
3.  In queste impostazioni predefinite del server, il runtime esterno probabilmente avrà risorse insufficienti per completare la maggior parte delle attività. Per ovviare a questa situazione, è necessario modificare l'utilizzo delle risorse del server in questo modo:
  
    -   Ridurre la quantità massima di memoria del computer che può essere utilizzata dal motore di database.
  
    -   Aumentare la memoria massima del computer che può essere usata dal processo esterno.

## <a name="modify-server-resource-usage"></a>Modificare l'utilizzo delle risorse del server

1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] eseguire l'istruzione seguente per limitare l'utilizzo della memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al **60%** del valore specificato nell'impostazione 'max server memory'.

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  Analogamente, eseguire l'istruzione seguente per limitare l'uso di memoria da parte dei processi esterni al **40%** delle risorse totali del computer.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  Per applicare queste modifiche, è necessario riconfigurare e riavviare Resource Governor in questo modo:
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  Queste sono solo le impostazioni consigliate per iniziare. è necessario valutare le attività di Machine Learning alla luce di altri processi server per determinare il giusto equilibrio per l'ambiente e il carico di lavoro.

## <a name="create-a-user-defined-external-resource-pool"></a>Creare un pool di risorse esterno definito dall'utente
  
1.  Qualsiasi modifica apportata alla configurazione di Resource Governor viene applicata al server complessivamente e influisce sui carichi di lavoro che usano i pool predefiniti per il server, nonché su quelli che usano i pool esterni.
  
     Di conseguenza, per fornire un controllo con granularità più fine sui carichi di lavoro che devono avere la precedenza, è possibile creare un nuovo pool di risorse esterno definito dall'utente. È anche consigliabile definire una funzione di classificazione e assegnarla al pool di risorse esterno. La parola chiave **External** è nuova.
  
     Per iniziare, creare un nuovo *pool di risorse esterno definito dall'utente*. Nell'esempio seguente il pool si chiama **ds_ep**.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  Creare un gruppo di carico di lavoro denominato `ds_wg` da usare per la gestione delle richieste di sessione. Per le query SQL verrà usato il pool predefinito, mentre per tutti i processi esterni le query useranno il pool `ds_ep`.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     Le richieste vengono assegnate al gruppo predefinito ogni volta che la richiesta non può essere classificata o se si è verificato un altro errore di classificazione.
  
     Per altre informazioni, vedere [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md) e [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).
  
## <a name="create-a-classification-function-for-machine-learning"></a>Creare una funzione di classificazione per Machine Learning
  
Una funzione di classificazione esamina le attività in ingresso e determina se l'attività possa essere eseguita usando il pool di risorse corrente. Le attività che non soddisfano i criteri della funzione di classificazione vengono riassegnate al pool di risorse predefinito del server.
  
1. Per iniziare, specificare che una funzione di classificazione deve essere utilizzata da Resource Governor per determinare i pool di risorse. È possibile assegnare un **valore null** come segnaposto per la funzione di classificazione.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Per altre informazioni, vedere [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  Nella funzione di classificazione per ogni pool di risorse definire il tipo di istruzioni o le richieste in ingresso da assegnare al pool di risorse.
  
     Ad esempio, la funzione seguente restituisce il nome dello schema assegnato al pool di risorse esterno definito dall'utente se l'applicazione che ha inviato la richiesta è 'Microsoft R Host' o 'RStudio'. In caso contrario, restituisce il pool di risorse predefinito.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Dopo la creazione della funzione, riconfigurare il gruppo di risorse in modo da assegnare la nuova funzione di classificazione al gruppo di risorse esterno definito in precedenza.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Verificare i nuovi pool di risorse e l'affinità

Per verificare che le modifiche siano state apportate, controllare la configurazione della memoria e della CPU del server per ognuno dei gruppi di carico di lavoro associati a questi pool di risorse dell'istanza:

+ il pool predefinito per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server
+ pool di risorse predefinito per i processi esterni
+ il pool definito dall'utente per i processi esterni

1. Eseguire l'istruzione seguente per visualizzare tutti i gruppi del carico di lavoro:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Risultati di esempio**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|interno|Medio|25|0|0|0|0|1|2|
    |2|predefiniti|Medio|25|0|0|0|0|2|2|
    |256|ds_wg|Medio|25|0|0|0|0|2|256|
  
2.  Utilizzare la nuova vista del catalogo [sys. resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)per visualizzare tutti i pool di risorse esterni.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Risultati di esempio**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|predefiniti|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Per altre informazioni, vedere [Viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).
  
3.  Eseguire l'istruzione seguente per restituire informazioni sulle risorse del computer creata un'affinità al pool di risorse esterne, se applicabile:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     In questo caso, poiché i pool sono stati creati con affinità AUTO, non viene visualizzata alcuna informazione. Per altre informazioni, vedere [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulla gestione delle risorse del server, vedere:

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 
+ [Transact-SQL delle viste &#40;a gestione dinamica relative a Resource Governor&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Per una panoramica della governance delle risorse per Machine Learning, vedere:

+ [Gestire i carichi di lavoro Python e R con Resource Governor in SQL Server Machine Learning Services](resource-governor.md)
