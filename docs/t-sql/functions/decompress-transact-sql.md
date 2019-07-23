---
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6d94ffd0182bfad3ed95f52640a2aed01ceeaa54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118965"
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Questa funzione decomprime il valore di un'espressione di input usando l'algoritmo GZIP. `DECOMPRESS` restituisce una matrice di byte (tipo VARBINARY(MAX)).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
Valore **varbinary(** _n_ **)** , **varbinary(max)** o **binary(** _n_ **)** . Per altre informazioni, vedere [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipi restituiti  
Un valore con tipo di dati **varbinary(max)** . Per decomprimere l'argomento di input, `DECOMPRESS` usa l'algoritmo ZIP. Se necessario, l'utente deve eseguire esplicitamente il cast del risultato a un tipo di destinazione.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-decompress-data-at-query-time"></a>A. Decompressione dei dati al momento della query  
Questo esempio viene illustra come restituire i dati di una tabella compressa:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Visualizzare i dati compressi usando una colonna calcolata  
Questo esempio illustra come creare una tabella per l'archiviazione dei dati decompressi:  
  
```  
CREATE TABLE example_table (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
