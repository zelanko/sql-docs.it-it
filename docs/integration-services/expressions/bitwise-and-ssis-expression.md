---
title: '&amp; (AND bit per bit) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 295affd0b03368d8156bec8e3b7193f3ce0684ac
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71290308"
---
# <a name="amp-bitwise-and-ssis-expression"></a>&amp; (AND bit per bit) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Esegue un'operazione con AND bit per bit tra due valori integer. Confronta ogni bit del primo operando con il bit corrispondente del secondo operando. Se entrambi i bit hanno valore 1, il bit del risultato verrà impostato su 1, altrimenti verrà impostato su 0.  
  
 Entrambe le condizioni devono essere costituite da un intero con segno o da un intero senza segno.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression1, integer_expression2*  
 Qualsiasi espressione valida con tipo di dati Integer con o senza segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se una delle due condizioni è Null, il risultato dell'espressione sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene effettuata un'operazione con AND bit per bit tra le colonne **NumberA** e **NumberB**. La colonna**NumberA** contiene 3 (0000011) e la colonna **NumberB** contiene 7 (00000111).  
  
```  
NumberA & NumberB  
```  
  
 L'espressione restituisce 3 (00000011).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 In questo esempio viene eseguita un'operazione con AND bit per bit tra le colonne **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 Se **ReorderPoint** ha valore 10 e **SafetyStockLevel** ha valore 8, l'espressione restituirà 8 (00001000).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 In questo esempio viene eseguita un'operazione con AND bit per bit tra due valori integer.  
  
```  
3 & 5   
```  
  
 L'espressione restituisce 1 (00000001).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## <a name="see-also"></a>Vedere anche  
 [&& &#40;AND logico&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
