---
title: SIGN (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: b77aaffe4e6f0f0163978ba346abdd31cdc61ce8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897307"
---
# <a name="sign-ssis-expression"></a>SIGN (espressione SSIS)
  Viene restituito il segno positivo (+1), negativo (-1) o zero (0) di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida con segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Note  
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
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
