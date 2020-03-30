---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: b217787d0cba0a1d62ab8393ef7fac76d7665bb0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "77568064"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Fare clic su un prodotto.

Nella riga seguente fare clic sul nome di prodotto a cui si è interessati. Verrà visualizzato un contenuto diverso in questa pagina Web, appropriato per il prodotto su cui si fa clic.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[Istanza gestita<br />database SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

Crea un gruppo del carico di lavoro di Resource Governor e lo associa al pool di risorse di Resource Governor. Resource Governor non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).

![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>Argomenti

*group_name*</br>
Nome definito dall'utente per il gruppo di carico di lavoro. *group_name* è un valore alfanumerico, può essere composto da un massimo di 128 caratteri, deve essere univoco all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve essere conforme alle regole relative agli [identificatori](../../relational-databases/databases/database-identifiers.md).

IMPORTANCE = { LOW | **MEDIUM** | HIGH }</br>
Specifica l'importanza relativa di una richiesta nel gruppo del carico di lavoro. L'importanza è compresa fra le seguenti, MEDIUM è l'impostazione predefinita:

- LOW
- MEDIUM (valore predefinito)
- HIGH

> [!NOTE]
> Internamente, ogni impostazione dell'importanza viene memorizzata come un numero utilizzato per i calcoli.

IMPORTANCE è locale al pool di risorse. I gruppi di carico di lavoro con diversa importanza e interni allo stesso pool di risorse influiscono l'uno sull'altro, ma non sui gruppi di carico di lavoro in un altro pool di risorse.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*</br>
Specifica la quantità massima di memoria che una singola richiesta può accettare dal pool. *value* è una percentuale relativa alla dimensione del pool di risorse specificata da MAX_MEMORY_PERCENT.

*value* è un intero fino a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e un valore float a partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e in un'istanza gestita di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Il valore predefinito è 25. L'intervallo consentito per *value* è compreso tra 1 e 100.

> [!IMPORTANT]  
> La quantità specificata si riferisce solo alla memoria di concessione per l'esecuzione della query.
>
> Impostando *value* su 0 si impedisce l'esecuzione delle query con operazioni SORT e HASH JOIN nei gruppi del carico di lavoro definiti dall'utente.
>
> Non è consigliabile impostare *value* su un valore maggiore di 70 perché è possibile che il server non possa riservare una quantità sufficiente di memoria se sono in esecuzione altre query simultaneamente. È possibile che venga restituito l'errore di timeout query 8645.
>
> Se i requisiti di memoria della query superano il limite specificato da questo parametro, il server effettua le operazioni seguenti:
>
> - Per i gruppi di carico di lavoro definiti dall'utente, il server tenta di ridurre il grado di parallelismo delle query fino a quando i requisiti di memoria non rientrano nel limite o fino a quando il grado di parallelismo non è uguale a 1. Se i requisiti di memoria delle query sono ancora superiori al limite, si verifica l'errore 8657.
>
> - Per i gruppi di carico di lavoro interni e predefiniti, il server permette alla query di ottenere la memoria necessaria.
>
> In entrambi i casi, è possibile che si verifichi l'errore di timeout 8645 se il server non dispone di memoria fisica sufficiente.

REQUEST_MAX_CPU_TIME_SEC = *value*</br>
Viene specificato il tempo massimo della CPU, in secondi, utilizzabile da una richiesta. *value* deve essere 0 o un valore intero positivo. L'impostazione predefinita per *value* è 0, ovvero un valore illimitato.

> [!NOTE]
> Per impostazione predefinita, Resource Governor non impedirà la continuazione di una richiesta se viene superato il tempo massimo, ma verrà generato un evento. Per altre informazioni, vedere [Classe di evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).
> [!IMPORTANT]
> A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e usando il [flag di traccia 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), Resource Governor interrompe una richiesta se viene superato il tempo massimo.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*</br>
Specifica il tempo massimo, in secondi, che una query può attendere prima che una concessione di memoria (memoria buffer di lavoro) diventi disponibile. *value* deve essere 0 o un valore intero positivo. L'impostazione predefinita per *value*, 0, usa un calcolo interno basato sul costo della query per determinare il tempo massimo.

> [!NOTE]
> L'esecuzione della query può riuscire anche in caso di timeout relativo alla concessione di memoria. L'esito negativo di una query si verifica solo se sono in esecuzione più query simultaneamente. In caso contrario, la query può ottenere solo la minima concessione di memoria, con una conseguente riduzione delle prestazioni.

MAX_DOP = *value*</br>
Specifica il **massimo grado di parallelismo (MAXDOP)** per l'esecuzione di richieste parallele. *value* deve essere 0 o un valore intero positivo. L'intervallo consentito per *value* è compreso tra 0 e 64. L'impostazione predefinita per *value*, 0, usa l'impostazione globale. MAX_DOP viene gestito nel modo seguente:

> [!NOTE]
> MAX_DOP del gruppo di carico di lavoro esegue l'override della [configurazione server del massimo grado di parallelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) e della [configurazione con ambito database](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) di **MAXDOP**.

> [!TIP]
> Per eseguire questa operazione a livello di query, usare l'[hint per la query](../../t-sql/queries/hints-transact-sql-query.md) **MAXDOP**. L'impostazione del massimo grado di parallelismo come hint per la query è efficace finché non supera il valore MAX_DOP del gruppo di carico di lavoro. Se il valore dell'hint per la query MAXDOP supera il valore configurato con Resource Governor, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa il valore `MAX_DOP` di Resource Governor. L'[hint per la query](../../t-sql/queries/hints-transact-sql-query.md) MAXDOP esegue sempre l'override della [configurazione server per il massimo grado di parallelismo ](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
>
> Per eseguire questa operazione a livello di database, usare la [configurazione con ambito database](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) **MAXDOP**.
>
> Per eseguire questa operazione a livello di server, usare l'[opzione di configurazione server](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) relativa al **massimo grado di parallelismo (MAXDOP)** .

GROUP_MAX_REQUESTS = *value*</br>
Viene specificato il numero massimo di richieste simultanee eseguibili nel gruppo del carico di lavoro. *value* deve essere 0 o un numero intero positivo. L'impostazione predefinita per *value* è 0 e consente un numero illimitato di richieste. Quando viene raggiunto il numero massimo di richieste simultanee, un utente in quel gruppo può effettuare l'accesso, ma viene posizionato in uno stato di attesa fino a quando le richieste simultanee non sono inferiori al valore specificato.

USING { *pool_name* |  **"default"** }</br>
Associa il gruppo del carico di lavoro al pool di risorse definito dall'utente identificato da *pool_name*. In questo modo, il gruppo del carico di lavoro viene inserito nel pool di risorse. Se *pool_name* non viene specificato o non si usa l'argomento USING, il gruppo del carico di lavoro viene inserito nel pool predefinito di Resource Governor.

"default" è una parola riservata e, se utilizzata con USING, deve essere delimitata da virgolette ("") o parentesi quadre ([]).

> [!NOTE]
> Per i gruppi di carico di lavoro e i pool di risorse predefiniti vengono utilizzati sempre nomi scritti in lettere minuscole, ad esempio "default". Questo aspetto deve essere preso in considerazione per i server in cui vengono utilizzate regole di confronto con distinzione tra maiuscole e minuscole. In server con regole di confronto senza distinzione tra maiuscole e minuscole, ad esempio SQL_Latin1_General_CP1_CI_AS, le parole "default" e "Default" vengono considerate uguali.

EXTERNAL external_pool_name | "default"</br>
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]).

Il gruppo del carico di lavoro può specificare un pool di risorse esterne. È possibile definire un gruppo di carico del lavoro e associarlo a due pool:

- Un pool di risorse per i carichi di lavoro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le query
- Un pool di risorse esterne per i processi esterni. Per altre informazioni, vedere [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="remarks"></a>Osservazioni

Quando si usa `REQUEST_MEMORY_GRANT_PERCENT`, per la creazione dell'indice è possibile usare più memoria dell'area di lavoro di quella concessa inizialmente, al fine di migliorare le prestazioni. Tale gestione particolare è supportata da Resource Governor in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La concessione iniziale, così come qualsiasi concessione supplementare, è tuttavia limitata dalle impostazioni del pool di risorse e del gruppo di carico di lavoro.

Il limite `MAX_DOP` viene impostato per [attività](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Non è un limite per [richiesta](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) o per query. Ciò significa che durante l'esecuzione di query parallele una singola richiesta può generare più attività che vengono assegnate a un'[utilità di pianificazione](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Per altre informazioni, vedere [Guida sull'architettura dei thread e delle attività](../../relational-databases/thread-and-task-architecture-guide.md).

Se si usa `MAX_DOP` e una query viene contrassegnata come seriale in fase di compilazione, in fase di esecuzione non può tornare parallela, indipendentemente dal gruppo di carico di lavoro o dall'impostazione della configurazione server. Dopo che è stato configurato, il valore `MAX_DOP` può essere diminuito solo in caso di utilizzo elevato della memoria. La riconfigurazione del gruppo di carico di lavoro non è visibile durante l'attesa nella coda della memoria concessa.

### <a name="index-creation-on-a-partitioned-table"></a>Creazione dell'indice in una tabella partizionata

La quantità di memoria utilizzata per la creazione dell'indice in una tabella partizionata non allineata è proporzionale al numero di partizioni coinvolte. Se la memoria totale necessaria supera il limite per query `REQUEST_MAX_MEMORY_GRANT_PERCENT` imposto dal gruppo di carico di lavoro di Resource Governor, la creazione dell'indice potrebbe non riuscire. Poiché il gruppo di carico di lavoro *"default"* consente a una query di superare il limite per query con la memoria minima necessaria, l'utente potrebbe essere in grado di eseguire la stessa creazione dell'indice nel gruppo di carico di lavoro *"default"* , se nel pool di risorse *"default"* è configurata una quantità di memoria totale sufficiente per eseguire la query.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione `CONTROL SERVER`.

## <a name="example"></a>Esempio

Creare un gruppo di carico di lavoro denominato `newReports` che usa le impostazioni predefinite di Resource Governor ed è contenuto nel pool predefinito di Resource Governor. Nell'esempio viene specificato il pool `default`, ma questo non è necessario.

```sql
CREATE WORKLOAD GROUP newReports
WITH
    (REQUEST_MAX_MEMORY_GRANT_PERCENT = 2.5
      , REQUEST_MAX_CPU_TIME_SEC = 100
      , MAX_DOP = 4)    
USING "default" ;
GO
```

## <a name="see-also"></a>Vedere anche

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[Istanza gestita<br />database SQL](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (anteprima)

Crea un gruppo di carico di lavoro. I gruppi di carico di lavoro sono contenitori per un set di richieste e su di essi si basa la configurazione della gestione del carico di lavoro in un sistema. I gruppi di carico di lavoro consentono di riservare risorse per l'isolamento del carico di lavoro, contengono risorse, definiscono le risorse per ogni richiesta e rispettano le regole di esecuzione. Al termine dell'esecuzione dell'istruzione, le impostazioni sono attive.

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

```
CREATE WORKLOAD GROUP group_name
[ WITH
 (  [ MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } ]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
]
```

*group_name*</br>
Specifica il nome con cui viene identificato il gruppo del carico di lavoro. *group_name* è un sysname. Può essere composto da un massimo di 128 caratteri e deve essere univoco all'interno dell'istanza.

*MIN_PERCENTAGE_RESOURCE* = valore</br>
Specifica un'allocazione delle risorse minima garantita per questo gruppo di carico di lavoro non condiviso con altri gruppi di carico di lavoro. Il *valore* è un numero intero compreso tra 0 e 100. La somma di min_percentage_resource in tutti i gruppi di carico di lavoro non può essere superiore a 100. Il valore di min_percentage_resource non può essere maggiore di cap_percentage_resource. Sono consentiti valori minimi effettivi per ogni livello di servizio. Per altre informazioni dettagliate, vedere [Valori effettivi](#effective-values).

*CAP_PERCENTAGE_RESOURCE* = valore</br>
Specifica l'utilizzo massimo delle risorse per tutte le richieste in un gruppo di carico di lavoro. L'intervallo di numeri interi consentito per il valore è compreso tra 1 e 100. Il valore di cap_percentage_resource deve essere maggiore di min_percentage_resource. Il valore effettivo per cap_percentage_resource può essere ridotto se min_percentage_resource è impostato su un valore maggiore di zero in altri gruppi di carico di lavoro.

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = valore</br>
Imposta la quantità minima di risorse allocate per ogni richiesta. Il *valore* è un parametro obbligatorio con un intervallo decimale compreso tra 0,75 e 100,00. Il valore di request_min_resource_grant_percent deve essere un multiplo di 0,25, deve essere un fattore di min_percentage_resource ed essere minore di cap_percentage_resource. Sono consentiti valori minimi effettivi per ogni livello di servizio. Per altre informazioni dettagliate, vedere [Valori effettivi](#effective-values).

Ad esempio:

```sql
CREATE WORKLOAD GROUP wgSample 
WITH
  ( MIN_PERCENTAGE_RESOURCE = 26                -- integer value
    , REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
    , CAP_PERCENTAGE_RESOURCE = 100 )
```

Si considerino i valori usati per le classi di risorse come linee guida per request_min_resource_grant_percent.  La tabella seguente contiene le allocazioni delle risorse per la seconda generazione.

|Classe di risorse|Percentuale di risorse|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = valore</br>         
Imposta la quantità massima di risorse allocate per ogni richiesta. Il *valore* è un parametro decimale facoltativo con un valore predefinito uguale a request_min_resource_grant_percent. Il *valore* deve essere maggiore o uguale a request_min_resource_grant_percent. Quando il valore di request_max_resource_grant_percent è maggiore di request_min_resource_grant_percent e sono disponibili risorse di sistema, vengono allocate risorse aggiuntive a una richiesta.

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>        
Specifica l'importanza predefinita di una richiesta per il gruppo del carico di lavoro. L'importanza è compresa fra le seguenti, NORMAL è l'impostazione predefinita:

- LOW
- BELOW_NORMAL
- NORMAL (valore predefinito)
- ABOVE_NORMAL
- HIGH

L'importanza impostata nel gruppo di carico di lavoro è un'importanza predefinita per tutte le richieste nel gruppo di carico di lavoro. Un utente può anche impostare l'importanza a livello di classificatore, eseguendo in questo modo l'override dell'impostazione dell'importanza del gruppo di carico di lavoro, che consente di differenziare l'importanza permettendo alle richieste di accedere più rapidamente alle risorse non riservate. Quando la somma di min_percentage_resource tra gruppi di carico di lavoro è inferiore a 100, sono presenti risorse non riservate che vengono assegnate in base all'importanza.

*QUERY_EXECUTION_TIMEOUT_SEC* = valore</br>     
Specifica il tempo massimo di esecuzione di una query, in secondi, prima che venga annullata. *value* deve essere 0 o un valore intero positivo. L'impostazione predefinita per il valore è 0, indicante che la query non raggiunge mai il timeout. QUERY_EXECUTION_TIMEOUT_SEC inizia il conteggio una volta che la query è in esecuzione, non quando la query viene accodata.

## <a name="remarks"></a>Osservazioni

I gruppi di carico di lavoro corrispondenti alle classi di risorse vengono creati automaticamente per la compatibilità con le versioni precedenti. Non è possibile eliminare questi gruppi di carico di lavoro definiti dal sistema. È possibile creare altri 8 gruppi di carico di lavoro definiti dall'utente.

Se viene creato un gruppo di carico di lavoro con `min_percentage_resource` maggiore di zero, l'istruzione `CREATE WORKLOAD GROUP` verrà accodata finché non sono disponibili risorse sufficienti per creare il gruppo di carico di lavoro.

## <a name="effective-values"></a>Valori effettivi

I parametri `min_percentage_resource`, `cap_percentage_resource`, `request_min_resource_grant_percent` e `request_max_resource_grant_percent` hanno valori effettivi che vengono modificati nel contesto del livello di servizio corrente e della configurazione di altri gruppi del carico di lavoro.

La concorrenza supportata per ogni livello di servizio rimane invariata quando le classi di risorse sono state usate per definire le concessioni di risorse per ogni query. Di conseguenza i valori supportati per request_min_resource_grant_percent dipendono dal livello di servizio su cui è impostata l'istanza. Al livello di servizio più basso, DW100c, è necessario almeno il 25% di risorse per richiesta. Al livello DW100c, il valore effettivo di request_min_resource_grant_percent per un gruppo di carico di lavoro configurato può essere pari o superiore al 25%. Per altri dettagli su come vengono derivati i valori effettivi, vedere la tabella seguente.

|Livello di servizio|Valore effettivo mio per REQUEST_MIN_RESOURCE_GRANT_PERCENT|Numero massimo di query simultanee|
|---|---|---|
|DW100c|25%|4|
|DW200c|12,5%|8|
|DW300c|8%|12|
|DW400c|6,25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1,5%|64|
|DW5000c|1,5%|64|
|DW6000c|0,75%|128|
|DW7500c|0,75%|128|
|DW10000c|0,75%|128|
|DW15000c|0,75%|128|
|DW30000c|0,75%|128|
||||

Analogamente, request_min_resource_grant_percent, min_percentage_resource devono essere maggiori o uguali al valore effettivo di request_min_resource_grant_percent. Il valore di un gruppo di carico di lavoro con `min_percentage_resource` inferiore al valore effettivo di `min_percentage_resource` viene impostato su zero in fase di esecuzione. In questo caso, le risorse configurate per `min_percentage_resource` sono condivisibili in tutti i gruppi di carico di lavoro. Ad esempio, il gruppo di carico di lavoro `wgAdHoc` con `min_percentage_resource` del 10% in esecuzione in DW1000c avrà un valore `min_percentage_resource` effettivo del 10% (3,25% è il valore minimo supportato in DW1000c). `wgAdhoc` in DW100c avrà un valore min_percentage_resource effettivo dello 0%. Il 10% configurato per `wgAdhoc` verrà condiviso tra tutti i gruppi di carico di lavoro.

Anche `cap_percentage_resource` ha un valore effettivo. Se un gruppo di carico di lavoro `wgAdhoc` è configurato con una `cap_percentage_resource` del 100% e viene creato un altro gruppo di carico di lavoro `wgDashboards` con `min_percentage_resource` del 25%, il valore `cap_percentage_resource` effettivo per `wgAdhoc` diventa 75%.

Il modo più semplice per conoscere i valori di runtime per i gruppi di carico di lavoro consiste nell'eseguire una query sulla vista di sistema [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md).

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione `CONTROL DATABASE`

## <a name="see-also"></a>Vedere anche

- [DROP WORKLOAD GROUP (Transact-SQL)](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- Avvio rapido per creare e usare un [gruppo di carico di lavoro](https://docs.microsoft.com/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
