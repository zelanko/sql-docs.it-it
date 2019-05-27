---
title: ~ (NOT bit per bit) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- "~"
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5957410faa3bcc2870712e01857216c2ef526008
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981322"
---
# <a name="-bitwise-not-transact-sql"></a>~ (NOT bit per bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Esegue un'operazione con NOT logico bit per bit su un valore integer.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Qualsiasi [espressione](../../t-sql/language-elements/expressions-transact-sql.md) valida di qualsiasi tipo di dati della categoria Integer o del tipo di dati **bit**, **binary** o **varbinary**. *expression* viene considerato un numero binario per l'operazione bit per bit.  
  
> [!NOTE]  
>  In un'operazione bit per bit un solo valore *expression* può avere il tipo di dati **binary** o **varbinary**.  
  
## <a name="result-types"></a>Tipi restituiti  
 **int** se i valori di input sono **int**.  
  
 **smallint** se i valori di input sono **smallint**.  
  
 **tinyint** se i valori di input sono **tinyint**.  
  
 **bit** se i valori di input sono **bit**.  
  
## <a name="remarks"></a>Remarks  
 L'operatore bit per bit **~** esegue un'operazione con NOT logico bit per bit per *expression*, valutando ogni bit in serie. Se *expression* ha un valore pari a 0, i bit nel set di risultati vengono impostati su 1; in caso contrario, i bit del risultato vengono impostati su 0. In altre parole, i bit a uno vengono cambiati in zero e i bit a zero vengono modificati in uno.  
  
> [!IMPORTANT]  
>  Per l'esecuzione di qualsiasi operazione bit per bit, la lunghezza di archiviazione dell'espressione utilizzata nell'operazione è un fattore importante. È consigliabile utilizzare lo stesso numero di byte per l'archiviazione dei valori. Ad esempio, il numero di byte del valore archiviato corrispondente al valore decimale 5 risulta diverso a seconda che 5 venga archiviato come valore di tipo **tinyint**, **smallint** o **int**. Infatti **tinyint** archivia i dati usando 1 byte, **smallint** archivia i dati usando 2 byte e **int** archivia i dati usando 4 byte. Un'operazione bit per bit su un valore decimale di tipo **int**, pertanto, restituisce risultati diversi rispetto a quelli di una conversione diretta binaria o esadecimale, soprattutto nel caso dell'operatore **~** (NOT bit per bit). L'operazione con NOT bit per bit potrebbe essere eseguita su una variabile di lunghezza inferiore. In questo caso, quando la variabile di lunghezza inferiore viene convertita in una variabile con tipo di dati di lunghezza maggiore, i bit negli 8 bit superiori potrebbero non essere impostati sul valore previsto. È pertanto consigliabile convertire la variabile del tipo di dati di lunghezza minore nel tipo di dati di lunghezza maggiore ed eseguire quindi l'operazione NOT sul valore risultante.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una tabella con il tipo di dati **int** per l'archiviazione dei valori e i due valori vengono inseriti in un'unica riga.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Nella query seguente viene eseguita l'operazione con NOT bit per bit sulle colonne `a_int_value` e `b_int_value`.  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 Set di risultati:  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 La rappresentazione binaria di 170 (`a_int_value` o `A`) è `0000 0000 1010 1010`. L'esecuzione dell'operazione con NOT bit per bit su questo valore genera il risultato binario `1111 1111 0101 0101`, corrispondente al valore decimale 171. La rappresentazione binaria di 75 è `0000 0000 0100 1011`. L'esecuzione dell'operazione con NOT bit per bit genera il risultato `1111 1111 1011 0100`, ovvero il valore decimale -76.  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operatori bit per bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


