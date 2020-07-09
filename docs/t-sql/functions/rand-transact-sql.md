---
title: RAND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 61303b7bffb07b2a42628af54d054250308723f2
ms.sourcegitcommit: 2e6c4104dca8680064eb64a7a79a3e15e1b4365f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2020
ms.locfileid: "85942925"
---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Restituisce un valore **float** pseudocasuale compreso tra 0 e 1 (esclusi).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *seed*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) Integer (**tinyint**, **smallint** o **int**) che specifica il valore di inizializzazione. Se *seed* è omesso, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] assegna un valore di inizializzazione in modo casuale. Per un valore di inizializzazione specificato, il risultato restituito è sempre lo stesso.  
  
## <a name="return-types"></a>Tipi restituiti  
 **float**  
  
## <a name="remarks"></a>Osservazioni  
 Le chiamate ripetute della funzione RAND() con lo stesso valore di inizializzazione restituiscono gli stessi risultati.  
  
 Per una connessione, se si chiama RAND() con un valore di inizializzazione specificato, tutte le chiamate successive di RAND() restituiscono risultati basati sulla chiamata RAND() inizializzata. Ad esempio, la query seguente restituirà sempre la stessa sequenza di numeri.  
  
```sql  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti quattro numeri casuali diversi generati dalla funzione RAND.  
  
```sql  
DECLARE @counter SMALLINT;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni matematiche &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
