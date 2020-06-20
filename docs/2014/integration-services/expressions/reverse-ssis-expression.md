---
title: REVERSE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5b8a65119f52302c12211ea0e33ac18aa1ce9676
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969081"
---
# <a name="reverse-ssis-expression"></a>REVERSE (espressione SSIS)
  Viene restituita un'espressione di caratteri in ordine inverso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Espressione di caratteri da invertire.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_WSTR  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo di dati dell’argomento *character_expression* deve essere DT_WSTR.  
  
 Se *character_expression* è null, REVERSE restituisce un risultato null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale stringa. Il risultato restituito è "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 In questo esempio viene utilizzata una variabile. Se **Name** contiene Touring Bike, il risultato restituito sarà "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
