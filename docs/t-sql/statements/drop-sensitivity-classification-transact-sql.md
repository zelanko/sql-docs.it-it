---
title: DROP SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
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
ms.openlocfilehash: d70e4a10601ab7c9171ddccf41a9ab9e5b2395c7
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544319"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Elimina i metadati di classificazione della riservatezza da una o più colonne di database.

## <a name="syntax"></a>Sintassi

```syntaxsql
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
    - *table_name*: si tratta del nome della tabella a cui appartiene la colonna classificata.
    - *column_name*: si tratta del nome della colonna da cui eliminare la classificazione.

## <a name="remarks"></a>Osservazioni  

- È possibile eliminare più classificazioni di oggetti usando una sola istruzione 'DROP SENSITIVITY CLASSIFICATION'.

## <a name="permissions"></a>Autorizzazioni  

È necessaria l'autorizzazione ALTER ANY SENSITIVITY CLASSIFICATION. L'autorizzazione ALTER ANY SENSITIVITY CLASSIFICATION è implicita nell'autorizzazione del database ALTER o nell'autorizzazione del server CONTROL SERVER.


## <a name="examples"></a>Esempi  


### <a name="a-dropping-classification-from-a-single-column"></a>R. Eliminazione della classificazione da una singola colonna

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
