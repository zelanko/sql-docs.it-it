---
title: CODEPOINT (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10d2eeb6991c0c75e8dbe8102f94148f60f0a361
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62769377"
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (espressione SSIS)
  Viene restituito l'elemento di codice Unicode del carattere più a sinistra di un'espressione di caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Espressione di caratteri di cui restituire il primo carattere a sinistra.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_UI2  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo di dati di*character_expression* deve essere DT_WSTR.  
  
 Se il parametro *character_expression* è una stringa vuota o Null, tramite CODEPOINT verrà restituito Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale stringa. Il risultato restituito è 77, l'elemento di codice Unicode corrispondente alla lettera M.  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 In questo esempio viene utilizzata una variabile. Se **Name** contiene la stringa Touring Front Wheel, il risultato restituito sarà 84, l'elemento di codice Unicode corrispondente alla lettera T.  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
