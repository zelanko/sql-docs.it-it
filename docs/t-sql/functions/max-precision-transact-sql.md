---
title: '@@MAX_PRECISION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@MAX_PRECISION_TSQL'
- '@@MAX_PRECISION'
dev_langs:
- TSQL
helpviewer_keywords:
- precision [SQL Server], @@MAX_PRECISION
- numeric data type, precision level
- decimal data type, precision level
- '@@MAX_PRECISION function'
- data types [SQL Server], precision
ms.assetid: 9e7158a1-e503-422a-b326-3c9b06e181b2
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 158ee073a0aed0d069f538732679aabcb1a19da0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832993"
---
# <a name="x40x40max_precision-transact-sql"></a>&#x40;&#x40;MAX_PRECISION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il livello di precisione usato dai tipi di dati **decimal** e **numeric** attualmente impostato nel server.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
@@MAX_PRECISION  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **tinyint**  
  
## <a name="remarks"></a>Osservazioni  
 Per impostazione predefinita, la precisione massima restituisce 38.  
  
## <a name="examples"></a>Esempi  
  
```  
SELECT @@MAX_PRECISION AS 'Max Precision'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di configurazione &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)  
  
  
