---
title: PARAMETRI (Transact-SQL) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14001680cd4cf92086ab797f77e2233222d36b67
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590715"
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni parametro di una funzione definita dall'utente o stored procedure accessibile per l'utente corrente nel database corrente. Per le funzioni, questa vista restituisce inoltre una riga con informazioni sul valore restituito.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar (** 128 **)**|Nome del catalogo della routine per cui questo è un parametro.|  
|**SPECIFIC_SCHEMA**|**nvarchar (** 128 **)**|Nome dello schema della routine per cui questo è un parametro.<br /><br /> <strong>\*\* Importanti \* \*</strong>  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**SPECIFIC_NAME**|**nvarchar (** 128 **)**|Nome della routine per cui questo è un parametro.|  
|**ORDINAL_POSITION**|**int**|Posizione ordinale del parametro a partire da 1. Per il valore restituito da una funzione, corrisponde a 0.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|Restituisce IN se è un parametro di input, OUT se è un parametro di output e INOUT se è un parametro di input/output.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|Restituisce YES se indica il risultato della routine che corrisponde a una funzione. In caso contrario restituisce NO.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|Restituisce YES se dichiarato come indicatore di posizione. In caso contrario restituisce NO.|  
|**PARAMETER_NAME**|**nvarchar (** 128 **)**|Nome del parametro. È NULL se corrisponde al valore restituito da una funzione.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Tipo di dati di sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Lunghezza massima in caratteri per tipi di dati binary o character.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. In caso contrario, viene restituito NULL.|  
|**CHARACTER_OCTET_LENGTH**|**int**|Lunghezza massima in byte per tipi di dati binary o character.<br /><br /> -1 per **xml** e i dati del tipo di valori di grandi dimensioni. In caso contrario, viene restituito NULL.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|Viene restituito sempre NULL.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|Viene restituito sempre NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Nome delle regole di confronto del parametro. Se non si tratta di uno dei tipi di dati character, restituisce NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|Nome del catalogo in cui è definito il set di caratteri del parametro. Se non si tratta di uno dei tipi di dati character, restituisce NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|Viene restituito sempre NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Nome del set di caratteri del parametro. Se non si tratta di uno dei tipi di dati character, restituisce NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. In caso contrario, viene restituito NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base di precisione dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. In caso contrario, viene restituito NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Scala dei dati numerici approssimati, dei dati numerici esatti, dei dati integer o dei dati in valuta. In caso contrario, viene restituito NULL.|  
|**DATETIME_PRECISION**|**smallint**|Precisione in frazioni di secondo se il tipo di parametro è **data/ora** oppure **smalldatetime**. In caso contrario, viene restituito NULL.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL Riservato per utilizzi futuri.|  
|**INTERVAL_PRECISION**|**smallint**|NULL Riservato per utilizzi futuri.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
|**SCOPE_CATALOG**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
|**SCOPE_SCHEMA**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
|**SCOPE_NAME**|**nvarchar (** 128 **)**|NULL Riservato per utilizzi futuri.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
