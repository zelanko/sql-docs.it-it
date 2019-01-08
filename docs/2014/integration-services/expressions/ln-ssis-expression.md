---
title: LN (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eea8fed6bb9330bd552aed042d6aac3557274376
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823675"
---
# <a name="ln-ssis-expression"></a>LN (espressione SSIS)
  Restituisce il logaritmo naturale di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida strettamente maggiore di zero.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_R8  
  
## <a name="remarks"></a>Note  
 Prima del calcolo del logaritmo viene eseguito il cast dell'espressione numerica al tipo di dati DT_R8. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
 Se tramite il parametro *numeric_expression* viene restituito zero o un valore negativo, il risultato sarà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale numerico. La funzione restituisce 3,737766961828337.  
  
```  
LN(42)  
```  
  
 In questo esempio viene usata la colonna **Length**. Se il valore della colonna è 53,99, la funzione restituirà 3,9887988442302.  
  
```  
LN(Length)   
```  
  
 In questo esempio viene usata la variabile **Length**. La variabile deve avere un tipo di dati numeric oppure l'espressione deve includere un cast esplicito a un tipo di dati numeric. Se il valore di **Length** è 234,567, la funzione restituisce 5,45774126708797.  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>Vedere anche  
 [LOG &#40;espressione SSIS&#41;](log-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
