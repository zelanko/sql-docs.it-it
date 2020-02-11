---
title: '&amp;&amp; (AND logico) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f0d51123d4ef5b17ad69dc8623a586058e27e212
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62897538"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (AND logico) (espressione SSIS)
  Viene eseguita un'operazione con AND logico. Viene restituito TRUE dall'espressione se tutte le condizioni sono TRUE.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>Argomenti  
 *boolean _expression1, boolean_expression2*  
 Qualsiasi espressione valida che restituisce TRUE, FALSE o NULL.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_BOOL  
  
## <a name="remarks"></a>Osservazioni  
 Il risultato dell'operatore && è illustrato nella tabella seguente.  
  
|Risultato|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio vengono usate le colonne **StandardCost** e **ListPrice** . Viene restituito TRUE se il valore della colonna **StandardCost** è minore di 300 e quello della colonna **ListPrice** è maggiore di 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 In questo esempio vengono usate le variabili **SPrice** e **LPrice** anziché valori letterali.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&& &#40;AND bit per bit&#41; &#40;espressione SSIS&#41;](bitwise-and-ssis-expression.md)   
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
