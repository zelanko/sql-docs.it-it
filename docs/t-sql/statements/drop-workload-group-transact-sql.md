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
ms.openlocfilehash: d2bbbee44b7b50e5d25bda3b4d10c6123db6497b
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001159"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Fare clic su un prodotto.

Nella riga seguente fare clic sul nome di prodotto a cui si è interessati. Verrà visualizzato un contenuto diverso in questa pagina Web, appropriato per il prodotto su cui si fa clic.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||
|---|---|---|
|**_\* SQL Server \*_** &nbsp;|[Istanza gestita<br />database SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|**_\* Istanza gestita<br />database SQL \*_** &nbsp;|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

##  <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server e Istanza gestita di database SQL

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|[Istanza gestita<br />database SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)| **_\* Azure Synapse<br />Analytics \*_** &nbsp;|
||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (anteprima)

Consente di eliminare un gruppo di carico di lavoro.  Al termine dell'esecuzione dell'istruzione, le impostazioni sono attive.

![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```syntaxsql
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
