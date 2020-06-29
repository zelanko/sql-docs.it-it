---
title: UPPER (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 957b0ce9c43fd986cafc51807f212bd64eb4d9e0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437018"
---
# <a name="upper-ssis-expression"></a>UPPER (espressione SSIS)
  Restituisce un'espressione di caratteri dopo aver convertito i caratteri minuscoli in caratteri maiuscoli.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Espressione di caratteri da convertire in caratteri maiuscoli.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_WSTR  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare UPPER solo con il tipo di dati DT_WSTR. Se l'argomento *character_expression* è un valore letterale stringa o una colonna di dati con tipo di dati DT_STR, prima di eseguire l'operazione prevista da UPPER verrà eseguito il cast implicito al tipo di dati DT_WSTR. Per gli altri tipi di dati è necessario il cast esplicito al tipo di dati DT_WSTR. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md) e [Cast &#40;espressione SSIS&#41;](cast-ssis-expression.md).  
  
 Se l'argomento è Null, UPPER restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio un valore letterale stringa viene convertito in caratteri maiuscoli. Il risultato restituito è "HELLO".  
  
```  
UPPER("hello")  
```  
  
 In questo esempio viene convertito in maiuscolo il primo carattere della colonna **FirstName** . Se **FirstName** contiene anna, il risultato restituito sarà "A". Per altre informazioni, vedere [SUBSTRING &#40;espressione SSIS&#41;](substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 In questo esempio il valore della variabile **PostalCode** viene convertito in caratteri maiuscoli. Se **PostalCode** contiene k4b1s2, il risultato restituito sarà "K4B1S2".  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LOWER &#40;espressione SSIS&#41;](lower-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
