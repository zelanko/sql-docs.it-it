---
title: CEILING (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5771d0b0eec65bc6d22be86a09b08a4b052de821
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781303"
---
# <a name="ceiling-ssis-expression"></a>CEILING (espressione SSIS)
  Restituisce il più piccolo valore integer maggiore o uguale a un'espressione numerica specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 Tipo di dati dell'espressione numerica inviata alla funzione.  
  
## <a name="remarks"></a>Note  
 Se l'argomento è Null, CEILING restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questi esempi la funzione CEILING viene applicata a valori positivi, negativi e zero.  
  
```  
CEILING(123.74)  
```  
  
 Restituisce 124,00.  
  
```  
CEILING(-124.27)  
```  
  
 Restituisce -124,00.  
  
```  
CEILING(0.00)  
```  
  
 Restituisce 0,00.  
  
## <a name="see-also"></a>Vedere anche  
 [FLOOR &#40;espressione SSIS&#41;](floor-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
