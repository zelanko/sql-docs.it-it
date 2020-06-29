---
title: '- (sottrazione) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 26cdffc6862ace3bd0c9049ed24e04fce0b8fca9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428048"
---
# <a name="--subtract-ssis-expression"></a>- (sottrazione) (espressione SSIS)
  Viene sottratta la seconda espressione numerica dalla prima.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression1, numeric_expression2*  
 Espressione valida con tipo di dati numeric. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Osservazioni  
 Racchiudere l'espressione con il meno unario tra parentesi per assicurarsi che l'espressione venga valutata nell'ordine corretto  
  
## <a name="remarks"></a>Osservazioni  
 Se uno degli operandi è Null, il risultato sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene eseguita una sottrazione tra alcuni valori letterali numerici.  
  
```  
5 - 6.09  
```  
  
 In questo esempio il valore nella colonna **StandardCost** viene sottratto dal valore nella colonna **ListPrice** .  
  
```  
ListPrice - StandardCost  
```  
  
 In questo esempio un valore calcolato viene sottratto dalla colonna **ListPrice** . Poiché il nome include il carattere %, la variabile **Discount%** deve essere racchiusa tra parentesi. Per altre informazioni, vedere [Identificatori &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
