---
title: ^ (OR esclusivo bit per bit) (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4afd716b1241371525d2a9def89edc61ba8cc1ae
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297709"
---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (OR esclusivo bit per bit) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene eseguita un'operazione con OR esclusivo bit per bit su due valori integer. Confronta ogni bit del primo operando con il bit corrispondente del secondo operando. Se un bit ha valore 0 e l'altro 1, il bit del risultato corrispondente verrà impostato su 1. Se entrambi i bit hanno valore 0 o 1, il bit del risultato corrispondente verrà impostato su 0.  
  
 Entrambe le condizioni devono essere costituite da un valore con tipo di dati Integer con segno o da un valore con tipo di dati Integer senza segno.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression1, integer_expression2*  
 Qualsiasi espressione valida con tipo di dati Integer con o senza segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se una delle due condizioni è Null, il risultato dell'espressione sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene eseguita un'operazione con OR esclusivo bit per bit tra le variabili **NumberA** e **NumberB**. **NumberA** contiene 3 (00000011) e **NumberB** contiene 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 L'espressione restituisce 4 (00000100).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 In questo esempio viene eseguita un'operazione con OR esclusivo bit per bit tra le colonne **ReorderPoint** e **SafetyStockLevel** .  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Se **ReorderPoint** ha valore 10 e **SafetyStockLevel** ha valore 8, l'espressione restituirà 2 (00000010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 In questo esempio viene eseguita un'operazione con OR esclusivo bit per bit tra due valori integer.  
  
```  
3 ^ 5   
```  
  
 L'espressione restituisce 6 (00000110).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>Vedere anche  
 [&#124;&#124; &#40;OR logico&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; &#40;OR inclusivo bit per bit&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
