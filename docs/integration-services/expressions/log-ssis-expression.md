---
title: LOG (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
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
ms.openlocfilehash: d59d1ecc0f250d19196a356f77ecae00b097fdd9
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282745"
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
  
## <a name="remarks"></a>Remarks  
 Prima del calcolo del logaritmo viene eseguito il cast dell' *espressione numerica* al tipo di dati DT_R8. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
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
 [EXP &#40;espressione SSIS&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN &#40;espressione SSIS&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
