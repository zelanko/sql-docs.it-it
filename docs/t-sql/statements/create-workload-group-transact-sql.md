---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2019
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
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bac286dc1151c6a0b127a928206505fa047c9ad8
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718286"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Crea un gruppo del carico di lavoro di Resource Governor e lo associa al pool di risorse di Resource Governor. Resource Governor non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).

![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

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

*group_name* Nome definito dall'utente per il gruppo di carico di lavoro. *group_name* è un valore alfanumerico, può essere composto da un massimo di 128 caratteri, deve essere univoco all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve essere conforme alle regole relative agli [identificatori](../../relational-databases/databases/database-identifiers.md).

IMPORTANCE = { LOW | **MEDIUM** | HIGH } Specifica l'importanza relativa di una richiesta nel gruppo del carico di lavoro. L'importanza è compresa fra le seguenti, MEDIUM è l'impostazione predefinita:

- LOW
- MEDIUM (valore predefinito)
- HIGH

> [!NOTE]
> Internamente, ogni impostazione dell'importanza viene memorizzata come un numero utilizzato per i calcoli.

IMPORTANCE è locale al pool di risorse. I gruppi di carico di lavoro con diversa importanza e interni allo stesso pool di risorse influiscono l'uno sull'altro, ma non sui gruppi di carico di lavoro in un altro pool di risorse.

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value* Specifica la quantità massima di memoria che una singola richiesta può accettare dal pool. *value* è una percentuale relativa alla dimensione del pool di risorse specificata da MAX_MEMORY_PERCENT. *value* è un valore Integer fino a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e float a partire da [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], con un'impostazione predefinita di 25. L'intervallo consentito per *value* è compreso tra 1 e 100.

> [!NOTE]
> La quantità specificata si riferisce solo alla memoria di concessione per l'esecuzione della query.
>
> - Impostando *value* su 0 si impedisce l'esecuzione delle query con operazioni SORT e HASH MATCH nei gruppi di carico di lavoro definiti dall'utente. > - Non è consigliabile impostare *value* su un valore maggiore di 70 perché è possibile che il server non possa riservare una quantità sufficiente di memoria se sono in esecuzione altre query simultaneamente. È possibile che venga restituito l'errore di timeout query 8645.
> - Se i requisiti di memoria della query superano il limite specificato da questo parametro, il server effettua le operazioni seguenti:
>
> Per i gruppi di carico di lavoro definiti dall'utente, il server tenta di ridurre il grado di parallelismo delle query fino a quando i requisiti di memoria non rientrano nel limite o fino a quando il grado di parallelismo non è uguale a 1. Se i requisiti di memoria delle query sono ancora superiori al limite, si verifica l'errore 8657.
>
> Per i gruppi di carico di lavoro interni e predefiniti, il server permette alla query di ottenere la memoria necessaria.
>
> In entrambi i casi, è possibile che si verifichi l'errore di timeout 8645 se il server non dispone di memoria fisica sufficiente.

REQUEST_MAX_CPU_TIME_SEC = *value* Specifica il tempo massimo della CPU, in secondi, utilizzabile da una richiesta. *value* deve essere 0 o un valore intero positivo. L'impostazione predefinita per *value* è 0, ovvero un valore illimitato.

> [!NOTE]
> Per impostazione predefinita, Resource Governor non impedirà la continuazione di una richiesta se viene superato il tempo massimo, ma verrà generato un evento. Per altre informazioni, vedere [Classe di evento CPU Threshold Exceeded](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).
> [!IMPORTANT]
> A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 e usando il [flag di traccia 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), Resource Governor interrompe una richiesta se viene superato il tempo massimo.

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value* Specifica il tempo massimo, in secondi, che una query può attendere prima che diventi disponibile una concessione di memoria (memoria buffer di lavoro). *value* deve essere 0 o un valore intero positivo. L'impostazione predefinita per *value*, 0, usa un calcolo interno basato sul costo della query per determinare il tempo massimo.

> [!NOTE]
> L'esecuzione della query può riuscire anche in caso di timeout relativo alla concessione di memoria. L'esito negativo di una query si verifica solo se sono in esecuzione più query simultaneamente. In caso contrario, la query può ottenere solo la minima concessione di memoria, con una conseguente riduzione delle prestazioni.

MAX_DOP = *value* Specifica il grado massimo di parallelismo (DOP) per le richieste parallele. *value* deve essere 0 o un valore intero positivo. L'intervallo consentito per *value* è compreso tra 0 e 64. L'impostazione predefinita per *value*, 0, usa l'impostazione globale. MAX_DOP viene gestito nel modo seguente:

- MAX_DOP, inteso come hint per la query, è efficace fintanto che non supera il valore MAX_DOP del gruppo del carico di lavoro. Se l'hint per la query MAXDOP supera il valore configurato con Resource Governor, nel motore di database viene utilizzato il valore MAXDOP di Resource Governor.
- MAX_DOP, inteso come hint per la query, ha sempre la precedenza sull'opzione "max degree of parallelism" di sp_configure.
- Il valore MAX_DOP del gruppo di carico di lavoro ha sempre la precedenza sull'opzione "max degree of parallelism" di sp_configure.
- Se la query viene contrassegnata come seriale in fase di compilazione, durante l'esecuzione non potrà ritornare a parallela, indipendentemente dal gruppo del carico di lavoro o dall'impostazione sp_configure.
- Dopo la configurazione di DOP, è possibile diminuire solo la richiesta di memoria concessa. La riconfigurazione del gruppo di carico di lavoro non è visibile durante l'attesa nella coda della memoria concessa.

GROUP_MAX_REQUESTS = *value* Specifica il numero massimo di richieste simultanee eseguibili nel gruppo del carico di lavoro. *value* deve essere 0 o un numero intero positivo. L'impostazione predefinita per *value* è 0 e consente un numero illimitato di richieste. Quando viene raggiunto il numero massimo di richieste simultanee, un utente in quel gruppo può effettuare l'accesso, ma viene posizionato in uno stato di attesa fino a quando le richieste simultanee non sono inferiori al valore specificato.

USING { *pool_name* |  **"default"** } Associa il gruppo del carico di lavoro al pool di risorse definito dall'utente identificato da *pool_name*. In questo modo, il gruppo del carico di lavoro viene inserito nel pool di risorse. Se *pool_name* non viene specificato o non si usa l'argomento USING, il gruppo del carico di lavoro viene inserito nel pool predefinito di Resource Governor.

"default" è una parola riservata e, se utilizzata con USING, deve essere delimitata da virgolette ("") o parentesi quadre ([]).

> [!NOTE]
> Per i gruppi di carico di lavoro e i pool di risorse predefiniti vengono utilizzati sempre nomi scritti in lettere minuscole, ad esempio "default". Questo aspetto deve essere preso in considerazione per i server in cui vengono utilizzate regole di confronto con distinzione tra maiuscole e minuscole. In server con regole di confronto senza distinzione tra maiuscole e minuscole, ad esempio SQL_Latin1_General_CP1_CI_AS, le parole "default" e "Default" vengono considerate uguali.

EXTERNAL external_pool_name | "default" **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).

Il gruppo del carico di lavoro può specificare un pool di risorse esterne. È possibile definire un gruppo del carico di lavoro e associarlo a 2 pool:

- Un pool di risorse per i carichi di lavoro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le query
- Un pool di risorse esterne per i processi esterni. Per altre informazioni, vedere [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="remarks"></a>Remarks

Quando si usa `REQUEST_MEMORY_GRANT_PERCENT`, per la creazione dell'indice è possibile usare più memoria dell'area di lavoro di quella concessa inizialmente, al fine di migliorare le prestazioni. Tale gestione particolare è supportata da Resource Governor in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La concessione iniziale, così come qualsiasi concessione supplementare, è tuttavia limitata dalle impostazioni del pool di risorse e del gruppo di carico di lavoro.

### <a name="index-creation-on-a-partitioned-table"></a>Creazione dell'indice in una tabella partizionata

La quantità di memoria utilizzata per la creazione dell'indice in una tabella partizionata non allineata è proporzionale al numero di partizioni coinvolte. Se la memoria totale necessaria supera il limite per query `REQUEST_MAX_MEMORY_GRANT_PERCENT` imposto dal gruppo di carico di lavoro di Resource Governor, la creazione dell'indice potrebbe non riuscire. Poiché il gruppo di carico di lavoro *"default"* consente a una query di superare il limite per query con la memoria minima necessaria, l'utente potrebbe essere in grado di eseguire la stessa creazione dell'indice nel gruppo di carico di lavoro *"default"* , se nel pool di risorse *"default"* è configurata una quantità di memoria totale sufficiente per eseguire la query.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione `CONTROL SERVER`.

## <a name="example"></a>Esempio

- Creare un gruppo di carico di lavoro denominato newReports

Utilizza le impostazioni predefinite di Resource Governor ed è contenuto nel pool predefinito di Resource Governor. Nell'esempio viene specificato il pool `default`, ma questo non è necessario.

```sql
CREATE WORKLOAD GROUP newReports
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
