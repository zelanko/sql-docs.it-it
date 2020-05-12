---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 53fd9e194121fae1d38e75e2c96c00b6ecc41404
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828607"
---
# <a name="schema_id-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce l'ID dello schema associato a un nome di schema.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|----------|----------------|  
|*schema_name*|Nome dello schema. *schema_name* è di tipo **sysname**. Se *schema_name* viene omesso, SCHEMA_ID restituirà l'ID dello schema predefinito del chiamante.|  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
 Se *schema_name* non è uno schema valido, verrà restituito un valore NULL.  
  
## <a name="remarks"></a>Osservazioni  
 SCHEMA_ID restituisce gli ID degli schemi di sistema e degli schemi definiti dall'utente. SCHEMA_ID può essere chiamato in un elenco di selezione, in una clausola WHERE e dovunque è consentita un'espressione.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>R. Restituzione dell'ID di schema predefinito di un chiamante  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Restituzione dell'ID di uno schema denominato  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni per i metadati &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

