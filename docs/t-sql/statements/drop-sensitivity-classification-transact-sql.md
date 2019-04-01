---
title: DROP SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 871822e57e9109455614e1391a28d87a6d9e6b90
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493093"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Elimina i metadati di classificazione della riservatezza da una o più colonne di database.

## <a name="syntax"></a>Sintassi

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>Argomenti  

*object_name* ([schema_name.]table_name.column_name)

Si tratta del nome della colonna del database da cui rimuovere la classificazione. Attualmente è supportata solo la classificazione delle colonne.
    - *schema_name* (facoltativo): si tratta del nome dello schema a cui appartiene la colonna classificata.
    - *Table_name*: si tratta del nome della tabella a cui appartiene la colonna classificata.
    - *column_name*: si tratta del nome della colonna da cui eliminare la classificazione.

## <a name="remarks"></a>Remarks  

- È possibile eliminare più classificazioni di oggetti usando una sola istruzione 'DROP SENSITIVITY CLASSIFICATION'.

## <a name="permissions"></a>Autorizzazioni  

È necessaria l'autorizzazione ALTER ANY SENSITIVITY CLASSIFICATION. L'autorizzazione ALTER ANY SENSITIVITY CLASSIFICATION è implicita nell'autorizzazione del database ALTER o nell'autorizzazione del server CONTROL SERVER.


## <a name="examples"></a>Esempi  


### <a name="a-dropping-classification-from-a-single-column"></a>A. Eliminazione della classificazione da una singola colonna

Nell'esempio seguente la classificazione viene rimossa dalla colonna `dbo.sales.price`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. Eliminazione della classificazione da più colonne

Nell'esempio seguente la classificazione viene rimossa dalle colonne `dbo.sales.price`, `dbo.sales.discount` e `SalesLT.Customer.Phone`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>Vedere anche  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[Introduzione a SQL Information Protection](https://aka.ms/sqlip)
