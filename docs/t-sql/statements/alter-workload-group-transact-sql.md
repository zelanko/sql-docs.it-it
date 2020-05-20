---
title: ALTER WORKLOAD GROUP (Transact-SQL)
ms.custom: ''
ms.date: 05/05/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: d4b70d64da9d87a8bab61f1881473dd7daaefb28
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606794"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Fare clic su un prodotto.

Nella riga seguente fare clic sul nome di prodotto a cui si è interessati. Verrà visualizzato un contenuto diverso in questa pagina Web, appropriato per il prodotto su cui si fa clic.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

|||||
|---|---|---|---|
|**_\* SQL Server \*_** &nbsp;||[Istanza gestita<br />database SQL](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)||[Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)|**_\* Istanza gestita<br />database SQL \*_** &nbsp;|[Azure Synapse<br />Analytics](alter-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

[!INCLUDE [ALTER WORKLOAD GROUP](../../includes/alter-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](alter-workload-group-transact-sql.md?view=sql-server-2017)|[Istanza gestita<br />database SQL](alter-workload-group-transact-sql.md?view=azuresqldb-mi-current)|**_\* Azure Synapse<br />Analytics \*_** &nbsp;|
||||

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

Modifica un gruppo di carico di lavoro esistente.

Per altri dettagli sul comportamento di `ALTER WORKLOAD GROUP` in un sistema con richieste in esecuzione e in coda, vedere la sezione relativa al comportamento di `ALTER WORKLOAD GROUP` di seguito. 

Le restrizioni esistenti per [CREATE WORKLOAD GROUP](create-workload-group-transact-sql.md) si applicano anche a `ALTER WORKLOAD GROUP`.  Prima di modificare i parametri, eseguire una query in [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) per assicurarsi che i valori siano compresi negli intervalli accettabili.

## <a name="syntax"></a>Sintassi

```syntaxsql
ALTER WORKLOAD GROUP group_name
 WITH
 ([       MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ] 
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
  ```

## <a name="arguments"></a>Argomenti

group_name  
Nome del gruppo di carico di lavoro esistente definito dall'utente in corso di modifica.  group_name non è modificabile. 

MIN_PERCENTAGE_RESOURCE = valore  
Il valore è un numero intero compreso tra 0 e 100.  Quando si modifica min_percentage_resource, la somma di min_percentage_resource in tutti i gruppi di carico di lavoro non può essere maggiore di 100.  La modifica di min_percentage_resource richiede il completamento di tutte le query in esecuzione nel gruppo di carico di lavoro prima del completamento del comando.  Per altri dettagli, vedere la sezione Comportamento di ALTER WORKLOAD GROUP in questo documento.

CAP_PERCENTAGE_RESOURCE = valore  
Il valore è un numero intero compreso tra 1 e 100.  Il valore di cap_percentage_resource deve essere maggiore di min_percentage_resource.  La modifica di cap_percentage_resource richiede il completamento di tutte le query in esecuzione nel gruppo di carico di lavoro prima del completamento del comando.  Per altri dettagli, vedere la sezione Comportamento di ALTER WORKLOAD GROUP in questo documento. 

REQUEST_MIN_RESOURCE_GRANT_PERCENT = valore  
Il valore è un numero decimale compreso nell'intervallo da 0,75 a 100,00.  Il valore di request_min_resource_grant_percent deve essere un fattore di min_percentage_resource ed essere minore di cap_percentage_resource. 
  
REQUEST_MAX_RESOURCE_GRANT_PERCENT = valore  
Il valore è un numero decimale e deve essere maggiore di request_min_resource_grant_percent.

IMPORTANCE = { LOW |  BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }  
Modifica l'importanza predefinita di una richiesta per il gruppo di carico di lavoro.

QUERY_EXECUTION_TIMEOUT_SEC = valore  
Modifica il tempo massimo di esecuzione di una query, in secondi, prima che venga annullata. Il valore deve essere 0 o un numero intero positivo. L'impostazione predefinita per il valore è 0, ovvero un valore illimitato.   

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL DATABASE

## <a name="example"></a>Esempio

Nell'esempio seguente vengono controllati i valori nella vista del catalogo per wgDataLoads e i valori vengono modificati.

```sql
SELECT *
FROM sys.workload_management_workload_groups  
WHERE [name] = 'wgDataLoads'

ALTER WORKLOAD GROUP wgDataLoads WITH
( MIN_PERCENTAGE_RESOURCE            = 40
 ,CAP_PERCENTAGE_RESOURCE            = 80
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 10 )
 ```

## <a name="alter-workload-group-behavior"></a>Comportamento di ALTER WORKLOAD GROUP

In un qualsiasi momento esistono 3 tipi di richieste nel sistema:
- Richieste che non sono state ancora classificate.
- Richieste classificate e in attesa di blocchi di oggetti o risorse di sistema.
- Richieste classificate e in esecuzione.

In base alle proprietà del gruppo di carico di lavoro da modificare, la tempistica con cui le impostazioni diventano effettive varia.

**Importance o query_execution_timeout** Per le proprietà importance e query_execution_timeout, le richieste non classificate prelevano i nuovi valori di configurazione.  Le richieste in attesa e in esecuzione vengono eseguite con la configurazione precedente.  La richiesta `ALTER WORKLOAD GROUP` viene eseguita immediatamente indipendentemente dalla presenza di query in esecuzione nel gruppo di carico di lavoro.

**Request_min_resource_grant_percent o request_max_resource_grant_percent** Per request_min_resource_grant_percent e request_max_resource_grant_percent, le richieste in esecuzione vengono eseguite con la configurazione precedente.  Le richieste in attesa e non classificate prelevano i valori della nuova configurazione.  La richiesta `ALTER WORKLOAD GROUP` viene eseguita immediatamente indipendentemente dalla presenza di query in esecuzione nel gruppo di carico di lavoro.

**Min_percentage_resource o cap_percentage_resource** Per min_percentage_resource e cap_percentage_resource, le richieste in esecuzione vengono eseguite con la configurazione precedente.  Le richieste in attesa e non classificate prelevano i valori della nuova configurazione. 

Per modificare min_percentage_resource e cap_percentage_resource, è necessario scaricare le richieste in esecuzione nel gruppo di carico di lavoro in corso di modifica.  Quando si diminuisce min_percentage_resource, le risorse liberate vengono restituite al pool di condivisione consentendone l'uso per le richieste provenienti da altri gruppi di carico di lavoro.  Viceversa, se si aumenta min_percentage_resource sarà necessario attendere fino al completamento delle richieste che utilizzano solo le risorse necessarie dal pool condiviso.  L'operazione ALTER WORKLOAD GROUP avrà accesso prioritario alle risorse condivise rispetto alle altre richieste in attesa di essere eseguite nel pool condiviso.  Se la somma di min_percentage_resource supera il 100%, la richiesta ALTER WORKLOAD GROUP ha esito negativo immediatamente. 

**Comportamento di blocco** La modifica di un gruppo di carico di lavoro richiede un blocco globale su tutti i gruppi di carico di lavoro.  Una richiesta di modifica di un gruppo di carico di lavoro viene accodata alle richieste già inviate di creazione o eliminazione di gruppi di carico di lavoro.  Se viene inviato in contemporanea un batch di istruzioni ALTER, le istruzioni vengono elaborate in ordine di invio.  

## <a name="see-also"></a>Vedere anche

- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](create-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [Avvio rapido: Configurare l'isolamento del carico di lavoro tramite T-SQL](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
