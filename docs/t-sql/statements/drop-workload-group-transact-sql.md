---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 6e75e84884bca1fef4d42a64056e2ef38111e6db
ms.sourcegitcommit: 0a9058c7da0da9587089a37debcec4fbd5e2e53a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2020
ms.locfileid: "75952335"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Fare clic su un prodotto.

Nella riga seguente fare clic sul nome di prodotto a cui si è interessati. Verrà visualizzato un contenuto diverso in questa pagina Web, appropriato per il prodotto su cui si fa clic.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[Istanza gestita<br />database SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

Elimina un gruppo del carico di lavoro esistente di Resource Governor definito dall'utente.

![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>Argomenti

*group_name* è il nome di un gruppo di carico di lavoro esistente definito dall'utente.

## <a name="remarks"></a>Osservazioni

L'istruzione DROP WORKLOAD GROUP non è consentita per i gruppi interni o predefiniti di Resource Governor.

Per l'esecuzione di istruzioni DDL, è consigliabile avere familiarità con gli stati di Resource Governor. Per altre informazioni, vedere [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

Se un gruppo del carico di lavoro contiene sessioni attive, non sarà possibile eliminare o spostare il gruppo del carico di lavoro a un pool di risorse diverso quando l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE dovrà applicare la modifica. Per evitare il problema, eseguire una delle azioni seguenti:

- Attendere la disconnessione di tutte le sessioni relative al gruppo interessato, quindi eseguire nuovamente l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

- Arrestare in modo esplicito le sessioni del gruppo interessato utilizzando il comando KILL, quindi eseguire nuovamente l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

- Riavviare il server. Una volta completato il processo di riavvio, il gruppo eliminato non verrà creato e in un gruppo spostato verrà utilizzata la nuova assegnazione del pool di risorse.

- Una volta generata l'istruzione DROP WORKLOAD GROUP, se si decide di non arrestare in modo esplicito le sessioni per applicare la modifica, è possibile ricreare il gruppo utilizzando lo stesso nome presente prima della generazione dell'istruzione DROP, quindi spostando il gruppo al pool di risorse originale. Per applicare le modifiche, eseguire l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL SERVER.

## <a name="examples"></a>Esempi

L'esempio seguente illustra come eliminare il gruppo del carico di lavoro denominato `adhoc`.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Vedere anche

- [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[Istanza gestita<br />database SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (anteprima)

Consente di eliminare un gruppo di carico di lavoro.  Al termine dell'esecuzione dell'istruzione, le impostazioni sono attive.

![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>Argomenti

*group_name*  
Il nome di un gruppo del carico di lavoro esistente definito dall'utente.

## <a name="remarks"></a>Osservazioni

Non è possibile eliminare un gruppo di carico di lavoro se esistono classificatori per quest'ultimo.  Eliminare i classificatori prima di eliminare il gruppo di carico di lavoro.  Se sono presenti richieste attive che usano risorse del gruppo di carico di lavoro in corso di eliminazione, l'istruzione di eliminazione del carico di lavoro viene bloccata in corrispondenza di queste.

## <a name="examples"></a>Esempi

Usare l'esempio di codice seguente per determinare quali classificatori devono essere eliminati prima che sia possibile eliminare il gruppo di carico di lavoro.

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione CONTROL DATABASE

## <a name="see-also"></a>Vedere anche

[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

::: moniker-end
