---
title: ROWCOUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROWCOUNT_BIG
- ROWCOUNT_BIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROWCOUNT_BIG function
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 6e18a0eb-bb36-4348-90d9-8b1ecf095064
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e1ccc5aa9619c96fd75400531041442138e0b4f3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828637"
---
# <a name="rowcount_big-transact-sql"></a>ROWCOUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il numero di righe modificate dall'ultima istruzione eseguita. Questa funzione opera esattamente come [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md), con la sola differenza che il valore restituito da ROWCOUNT_BIG è di tipo **bigint**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ROWCOUNT_BIG ( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **bigint**  
  
## <a name="remarks"></a>Osservazioni  
 Se segue l'istruzione SELECT, questa funzione restituisce il numero di righe restituite dall'istruzione SELECT.  
  
 Se eseguita dopo le istruzioni INSERT, UPDATE o DELETE, questa funzione restituisce il numero di righe modificate dall'istruzione di modifica dei dati.  
  
 Se viene eseguita dopo istruzioni che non restituiscono alcuna riga, ad esempio un'istruzione IF, questa funzione restituisce zero (0).  
  
## <a name="see-also"></a>Vedere anche  
 [COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
