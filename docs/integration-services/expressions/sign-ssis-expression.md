---
title: SIGN (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ba986e4aeacc122e613a804893dbf755a8df481
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724974"
---
# <a name="sign-ssis-expression"></a>SIGN (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene restituito il segno positivo (+1), negativo (-1) o zero (0) di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida con segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 Se l'argomento è Null, SIGN restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito il segno di un valore letterale numerico. Il risultato restituito sarà -1.  
  
```  
SIGN(-123.45)  
```  
  
 In questo esempio viene restituito il segno del risultato della sottrazione della colonna **StandardCost** dalla colonna **DealerPrice** .  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
