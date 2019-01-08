---
title: ROUND (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3033398be7625230ac6d9abd7b8b329f312632c1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808013"
---
# <a name="round-ssis-expression"></a>ROUND (espressione SSIS)
  Restituisce un'espressione numerica arrotondata alla lunghezza o alla precisione specificata. Il parametro length deve restituire un valore integer.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione di tipo numeric valido. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
 *lunghezza*  
 Espressione integer. Precisione per l'arrotondamento di *numeric_expression* .  
  
## <a name="result-types"></a>Tipi restituiti  
 Tipo identico a *numeric*_*expression*.  
  
## <a name="remarks"></a>Note  
 Tramite l'argomento *length* deve essere restituito un numero intero positivo oppure zero.  
  
 Se l'argomento è Null, ROUND restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questi esempi alcuni valori letterali numerici vengono arrotondati con lunghezza tre. Il primo risultato restituito è 137,1570, il secondo 137,1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
