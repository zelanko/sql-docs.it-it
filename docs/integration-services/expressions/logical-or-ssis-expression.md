---
title: '|| (OR logico) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4ea60751df8c27ba61c190a3f48d25e4dfce8cb1
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725217"
---
# <a name="-logical-or-ssis-expression"></a>|| (OR logico) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene eseguita un'operazione con OR logico. Viene restituito TRUE dall'espressione se una o entrambe le condizioni sono TRUE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>Argomenti  
 *boolean_expression1, boolean_expression2*  
 Qualsiasi espressione valida che restituisce TRUE, FALSE o NULL.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 Il risultato dell'operatore || è illustrato nella tabella seguente.  
  
|Risultato|Espressione|Espressione|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>Esempi di espressione SSIS  
 In questo esempio vengono utilizzate le colonne **StandardCost** e **ListPrice** . Viene restituito TRUE se il valore della colonna **StandardCost** è minore di 300 o quello della colonna **ListPrice** è maggiore di 500.  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 In questo esempio vengono utilizzate le variabili **SPrice** e **LPrice** anziché valori letterali numerici.  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#124; &#40;OR inclusivo bit per bit&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40;OR esclusivo bit per bit&#41; &#40;Espressione SSIS&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
