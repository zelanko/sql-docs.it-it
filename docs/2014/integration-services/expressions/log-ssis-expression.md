---
title: LOG (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fde9e5cdaea245fd0b99820a89a4466e2d669fdf
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386419"
---
# <a name="log-ssis-expression"></a>LOG (espressione SSIS)
  Viene restituito il logaritmo in base 10 di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida strettamente maggiore di zero.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_R8  
  
## <a name="remarks"></a>Note  
 Prima del calcolo del logaritmo viene eseguito il cast dell' *espressione numerica* al tipo di dati DT_R8. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
 Se tramite il parametro *numeric_expression* viene restituito zero o un valore negativo, il risultato sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale numerico. La funzione restituisce 1,988291341907488.  
  
```  
LOG(97.34)  
```  
  
 In questo esempio viene usata la colonna **Length**. Se il valore della colonna è 101,24, la funzione restituirà 2,005352136486217.  
  
```  
LOG(Length)   
```  
  
 In questo esempio viene usata la variabile **Length**. La variabile deve avere un tipo di dati numeric o l'espressione deve includere un cast esplicito a un tipo di dati numeric di [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Se **Length** ha valore 234,567, la funzione restituirà 2,370266913465859.  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>Vedere anche  
 [EXP &#40;espressione SSIS&#41;](exp-ssis-expression.md)   
 [LN &#40;espressione SSIS&#41;](ln-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
