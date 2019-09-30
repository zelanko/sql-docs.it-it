---
title: () (parentesi) (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 968ab3afbdb5d184364758797180102d65293eb7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288524"
---
# <a name="-parentheses-ssis-expression"></a>() (parentesi) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 Tipo di dati di *espressione*. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene illustrato come l'utilizzo delle parentesi modifichi la precedenza degli operatori. La prima espressione restituisce 100, mentre la seconda restituisce 31.  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
