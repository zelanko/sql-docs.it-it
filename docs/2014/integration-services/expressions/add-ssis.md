---
title: + (addizione) (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 995632c691daf8210b7c01a6c132878228968f01
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437288"
---
# <a name="-add-ssis"></a>+ (addizione) (SSIS)
  Vengono aggiunte due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression1, numeric_expression2*  
 Espressione valida con tipo di dati numeric.  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se uno degli operandi è Null, il risultato sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio vengono sommati alcuni valori letterali numerici.  
  
```  
5 + 6.09 + 7.0  
```  
  
 In questo esempio vengono sommati i valori nelle colonne **VacationHours** e **SickLeaveHours** .  
  
```  
VacationHours + SickLeaveHours  
```  
  
 In questo esempio un valore calcolato viene sommato alla colonna **StandardCost** . Poiché il nome include il carattere %, la variabile **Profit%** deve essere racchiusa tra parentesi. Per altre informazioni, vedere [Identificatori &#40;SSIS&#41;](identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
