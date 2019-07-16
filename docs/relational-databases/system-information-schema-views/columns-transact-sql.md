---
title: Le colonne (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 021e9e66b281a8bbca6d5c9e21e78ffa4069c5c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950793"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni colonna accessibile dall'utente corrente nel database corrente.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA** _.view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|Qualificatore della tabella.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|Nome dello schema che contiene la tabella.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|Nome della tabella.|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|Nome colonna.|  
|**ORDINAL_POSITION**|**int**|Numero di identificazione della colonna.|  
|**COLUMN_DEFAULT**|**nvarchar(** 4000 **)**|Valore predefinito della colonna.|  
|**IS_NULLABLE**|**varchar(** 3 **)**|Impostazione relativa al supporto di valori Null nella colonna. Se nella colonna sono consentiti valori NULL, in questa colonna viene restituito YES. In caso contrario, viene restituito NO.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|Tipo di dati di sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Lunghezza massima espressa in caratteri per i dati di tipo binario, carattere, text o image.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. Per gli altri tipi di dati viene restituito NULL. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Lunghezza massima espressa in byte per i dati di tipo binario, carattere, text o image.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base di precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**NUMERIC_SCALE**|**int**|Scala dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. Per gli altri tipi di dati viene restituito NULL.|  
|**DATETIME_PRECISION**|**smallint**|Codice di sottotipo per **data/ora** e ISO **intervallo** i tipi di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|Restituisce **master**. Indica il database in cui è disponibile, il set di caratteri se la colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|Viene restituito sempre NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|Restituisce il nome univoco per il set di caratteri se questa colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|Viene restituito sempre NULL.|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|Viene restituito sempre NULL.|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|Restituisce il nome univoco per le regole di confronto se la colonna è di tipo carattere o **testo** tipo di dati. Per gli altri tipi di dati viene restituito NULL.|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|Restituisce il nome del database in cui è stato creato il tipo di dati definito dall'utente se la colonna contiene un tipo di dati alias. Per gli altri tipi di dati viene restituito NULL.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|Restituisce il nome dello schema del tipo di dati definito dall'utente se la colonna contiene un tipo di dati definito dall'utente. Per gli altri tipi di dati viene restituito NULL.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un tipo di dati. L'unica modalità affidabile per cercare lo schema di un tipo consiste nell'utilizzare la funzione TYPEPROPERTY.|  
|**DOMAIN_NAME**|**nvarchar(** 128 **)**|Restituisce il nome del tipo di dati definito dall'utente se la colonna contiene un tipo di dati definito dall'utente. Per gli altri tipi di dati viene restituito NULL.|  
  
## <a name="remarks"></a>Note  
 Il **ORDINAL_POSITION** colonna il **INFORMATION_SCHEMA. COLONNE** vista non è compatibile con lo schema di bit delle colonne restituite dalla funzione COLUMNS_UPDATED. Per ottenere uno schema di bit compatibile con COLUMNS_UPDATED, è necessario fare riferimento il **ColumnID** proprietà di funzione di sistema COLUMNPROPERTY quando esegue una query di **INFORMATION_SCHEMA. COLONNE** visualizzazione. Ad esempio:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
