---
title: STR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c52996b890529504c304aae2bf1dc41c3a3f4b4b
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947570"
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce dati di tipo carattere convertiti da dati di tipo numerico.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *float_expression*  
 Espressione del tipo di dati numerico approssimato (**float**) con un separatore decimale.  
  
 *length*  
 Lunghezza totale, che include il separatore decimale, il segno, le cifre e gli spazi. Il valore predefinito è 10.  
  
 *decimal*  
 Numero di posizioni a destra del separatore decimale. Il valore di *decimal* deve essere minore o uguale a 16. Se *decimal* è maggiore di 16, il risultato viene troncato in modo da includere sedici posizioni a destra del separatore decimale.  
  
## <a name="return-types"></a>Tipi restituiti  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 I valori dei parametri *length* e *decimal* della funzione STR devono essere positivi. Il numero viene arrotondato a un valore intero per impostazione predefinita o se il parametro decimal è 0. La lunghezza specificata deve essere maggiore o uguale alla parte intera del numero (a sinistra del separatore decimale) più il segno del numero, se disponibile. Un argomento di tipo *float_expression* breve viene allineato a destra in base alla lunghezza specificata, mentre un argomento di tipo *float_expression* lungo viene troncato al numero di cifre decimali specificato. Ad esempio, STR(12 **,** 10) restituisce il risultato 12, che viene allineato a destra nel set di risultati. STR(1223 **,** 2) tronca invece il set di risultati a **. Le funzioni stringa possono essere nidificate.  
  
> [!NOTE]  
>  Per eseguire la conversione in dati Unicode, usare STR in una funzione di conversione CONVERT o [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente un'espressione composta da cinque cifre e un separatore decimale viene convertita in una stringa di caratteri con sei posizioni. La parte frazionaria del numero viene arrotondata a una cifra decimale.  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 Quando l'espressione supera la lunghezza specificata, la stringa restituisce `**` per la lunghezza specificata.  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 Quando nella funzione `STR` i dati numerici sono nidificati, il risultato corrisponde comunque a dati di tipo carattere nel formato specificato.  
  
```  
SELECT STR (FLOOR (123.45), 8, 3);
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

