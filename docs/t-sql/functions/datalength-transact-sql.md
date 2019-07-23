---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a62aa2b5249384405372afe662a84a73055f4a67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026211"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Questa funzione restituisce il numero di byte usati per rappresentare un'espressione.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>Argomenti  
*expression*  
[Espressione](../../t-sql/language-elements/expressions-transact-sql.md) con qualsiasi tipo di dati.
  
## <a name="return-types"></a>Tipi restituiti
**bigint** se *expression* è del tipo di dati **nvarchar(max)** , **varbinary(max)** o **varchar(max)** . In caso contrario, **int**.
  
## <a name="remarks"></a>Remarks  
`DATALENGTH` è molto utile in combinazione con i tipi di dati

- **image**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**
- **varchar**

in quanto tali tipi di dati consentono di archiviare dati a lunghezza variabile.
  
Per un valore NULL, `DATALENGTH` restituisce NULL.
  
> [!NOTE]  
>  I livelli di compatibilità possono influire sui valori restituiti. Vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) per informazioni sui livelli di compatibilità supportati.  
  
## <a name="examples"></a>Esempi  
Questo esempio trova la lunghezza della colonna `Name` nella tabella `Product`:
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche
[LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

