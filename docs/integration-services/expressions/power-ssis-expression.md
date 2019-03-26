---
title: POWER (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f75364a019bbf6f4827d060cfd1daa7076137ea
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58269987"
---
# <a name="power-ssis-expression"></a>POWER (espressione SSIS)
  Restituisce il risultato dell'elevamento a potenza di un'espressione numerica. Il parametro power deve restituire un valore integer.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida.  
  
 *power*  
 Espressione numerica valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 Prima del calcolo della potenza, viene eseguito il cast degli argomenti *numeric_expression* e *power* nel tipo di dati DT_R8. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Se *numeric_expression* restituisce zero e *power* è negativo, l'analizzatore di espressioni restituisce un errore e imposta il risultato restituito su Null.  
  
 Se *numeric_expression* o *power* restituisce risultati indeterminati, viene restituito Null.  
  
 L'argomento *power* può essere una frazione. ad esempio 0,5.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale numerico. La funzione eleva 4 all'esponente 3 e restituisce 64.  
  
```  
POWER(4,3)  
```  
  
 Questo esempio usa la colonna **Length** e la variabile **DimensionCount** . Se **Length** è 8 e **DimensionCount** è 2, il risultato restituito è 64.  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
