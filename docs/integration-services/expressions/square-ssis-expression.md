---
title: SQUARE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0fa4de2afec8893f9101a973f18e5176490d5c32
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277320"
---
# <a name="square-ssis-expression"></a>SQUARE (espressione SSIS)
  Restituisce il quadrato di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida con qualsiasi tipo di dati numeric. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 Se l'argomento è Null, SQUARE restituirà Null.  
  
 Prima del calcolo del quadrato viene eseguito il cast dell'argomento al tipo di dati DT_R8.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito il quadrato di 12. Il risultato restituito è 144.  
  
```  
SQUARE(12)  
```  
  
 In questo esempio viene restituito il quadrato del risultato della sottrazione dei valori di due colonne. Se **Value1** contiene 12 e **Value2** contiene 4, la funzione SQUARE restituirà 64.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 In questo esempio viene restituita la lunghezza del terzo lato di un triangolo rettangolo, ottenuta applicando la funzione SQUARE a due variabili e quindi calcolando la radice quadrata della somma. Se **Side1** contiene 3 e **Side2** contiene 4, la funzione SQRT restituirà 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  Nelle espressioni i nomi delle variabili includono sempre il prefisso \@.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
