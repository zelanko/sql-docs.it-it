---
title: SQL_VARIANT_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: caadacbe6ad9eb1841a2646f39cdedea17ac58aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907031"
---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce il tipo di dati di base e altre informazioni su un valore di tipo **sql_variant**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Espressione di tipo **sql_variant**.  
  
 *property*  
 Contiene il nome della proprietà **sql_variant** per la quale è necessario specificare informazioni. *property* è **varchar(** 128 **)** . I valori possibili sono i seguenti:  
  
|valore|Descrizione|Tipo di base di sql_variant restituito|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|Tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio:<br /><br /> **bigint**<br /><br /> **binary**<br /><br /> **char**<br /><br /> **data**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = Input non valido.|  
|**Precisione**|Numero di cifre del tipo di dati numerici di base:<br /><br /> **datetime** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** (p,s) e **numeric** (p,s) = p<br /><br /> **money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> Tutti gli altri tipi = 0|**int**<br /><br /> NULL = Input non valido.|  
|**Scala**|Numero di cifre a destra del separatore decimale con tipo di base numerico:<br /><br /> **decimal** (p,s) e **numeric** (p,s) = s<br /><br /> **money** e **smallmoney** = 4<br /><br /> **datetime** = 3<br /><br /> Tutti gli altri tipi = 0|**int**<br /><br /> NULL = Input non valido.|  
|**TotalBytes**|Numero di byte necessari per l'archiviazione sia dei metadati che dei dati del valore. Questo valore risulta utile per verificare le dimensioni massime dei dati in una colonna **sql_variant**. Se il valore è maggiore di 900, la creazione dell'indice genera un errore.|**int**<br /><br /> NULL = Input non valido.|  
|**Regole di confronto**|Regole di confronto del valore di tipo **sql_variant** specifico.|**sysname**<br /><br /> NULL = Input non valido.|  
|**MaxLength**|Lunghezza massima del tipo di dati espressa in byte. Ad esempio, **MaxLength** di **nvarchar(** 50 **)** è 100, **MaxLength** di **int** è 4.|**int**<br /><br /> NULL = Input non valido.|  
  
## <a name="return-types"></a>Tipi restituiti  
 **sql_variant**  
  
## <a name="examples"></a>Esempi  
### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Uso di un tipo sql_variant in una tabella  
 Nell'esempio seguente vengono recuperate le informazioni di `SQL_VARIANT_PROPERTY` relative al valore `colA` `46279.1`, dove `colB` =`1689`, dato che `tableA` include `colA` di tipo `sql_variant` e `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Si noti che tutti e tre i valori sono di tipo **sql_variant**.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. Uso di un tipo sql_variant come variabile   
 Nell'esempio seguente vengono recuperate informazioni `SQL_VARIANT_PROPERTY` su una variabile con nome @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  

