---
title: sys. sensitivity_classifications (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: mibar
author: barmichal
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- rank
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b95dec6d4d867e54c3ccf0d1108a7f6b1cfa8f3c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73757468"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys. sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Restituisce una riga per ogni elemento classificato nel database.

|Nome colonna|Tipo di dati|Descrizione|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica la classe dell'elemento in cui esiste la classificazione|  
|**class_desc**|**varchar (16)**|Descrizione della classe dell'elemento in cui esiste la classificazione|  
|**major_id**|**int**|ID dell'elemento in cui esiste la classificazione.<br><br>Se la classe è 0, major_id è sempre 0.<br>Se la classe è 1, 2 o 7, major_id è object_id.|  
|**minor_id**|**int**|ID secondario dell'elemento in cui esiste la classificazione, interpretato in base alla relativa classe.<br><br>Se Class = 1, minor_id è la column_id (Se Column), altrimenti 0 (If Object).<br>Se la classe è 2, minor_id è parameter_id.<br>Se class = 7, minor_id è l'index_id. |  
|**label**|**sysname**|Etichetta (leggibile) assegnata per la classificazione di riservatezza|  
|**label_id**|**sysname**|ID associato all'etichetta, che può essere usato da un sistema di protezione delle informazioni, ad esempio Azure Information Protection (AIP)|  
|**information_type**|**sysname**|Tipo di informazioni (leggibile) assegnato per la classificazione di riservatezza|  
|**information_type_id**|**sysname**|ID associato al tipo di informazioni, che può essere usato da un sistema di protezione delle informazioni, ad esempio Azure Information Protection (AIP)|  
|**Rank**|**int**|Valore numerico del rango: <br><br>0 per nessuno<br>10 per basso<br>20 per media<br>30 per alta<br>40 per CRITICAL| 
|**rank_desc**|**sysname**|Rappresentazione testuale del rango:  <br><br>NONE, LOW, MEDIUM, HIGH, CRITICAL|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Osservazioni  

- Questa visualizzazione fornisce visibilità sullo stato di classificazione del database. Può essere utilizzato per la gestione delle classificazioni dei database, nonché per la generazione di report.
- Attualmente è supportata solo la classificazione delle colonne del database. Conseguenza
    - **classe** : avrà sempre il valore 1 (che rappresenta una colonna)
    - **class_desc** : il valore sarà sempre *OBJECT_OR_COLUMN*
    - **major_id** : rappresenta l'ID della tabella contenente la colonna classificata, corrispondente a sys. all_objects. object_id
    - **minor_id** : rappresenta l'ID della colonna in cui esiste la classificazione, corrispondente a sys. all_columns. column_id

## <a name="examples"></a>Esempi

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. Elenco di tutte le colonne classificate e della classificazione corrispondente

Nell'esempio seguente viene restituita una tabella in cui sono elencati il nome della tabella, il nome della colonna, l'etichetta, l'ID dell'etichetta, il tipo di informazioni e l'ID del tipo di informazioni per ogni colonna classificata

> [!NOTE]
> Label è una parola chiave per Azure SQL Data Warehouse.

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID], [Rank], [Rank_Desc]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="see-also"></a>Vedere anche  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[Introduzione a SQL Information Protection](https://aka.ms/sqlip)
