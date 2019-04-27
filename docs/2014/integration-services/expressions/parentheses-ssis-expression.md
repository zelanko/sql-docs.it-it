---
title: () (parentesi) (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3fc1a9beb0468f50291854d8eb5cd0e3bf9ba8d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768807"
---
# <a name="-parentheses-ssis-expression"></a>() (parentesi) (espressione SSIS)
  Viene identificato l'ordine di valutazione delle espressioni. Le espressioni racchiuse tra parentesi hanno la massima precedenza di valutazione. Le espressioni nidificate racchiuse tra parentesi vengono valutate procedendo dall'interno verso l'esterno.  
  
 È possibile utilizzare le parentesi anche per semplificare la comprensione delle espressioni complesse.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *espressione*  
 Qualsiasi espressione valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 Tipo di dati di *espressione*. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene illustrato come l'utilizzo delle parentesi modifichi la precedenza degli operatori. La prima espressione restituisce 100, mentre la seconda restituisce 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
