---
title: ~ (NOT bit per bit) (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c07444ff1dd425671fbc17176fc3aa94e0705bd
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725602"
---
# <a name="-bitwise-not-ssis-expression"></a>~ (NOT bit per bit) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene eseguita una negazione bit per bit di un valore integer. Questo operatore può essere applicato a tipi di dati integer con e senza segno.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression*  
 Espressione valida con qualsiasi tipo di dati integer. *integer*_*expression* è un numero intero trasformato in un numero binario per l'operazione bit per bit. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Restituisce il tipo di dati di *integer_expression.*  
  
## <a name="remarks"></a>Remarks  
 None  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene applicato l'operatore ~ (NOT) bit per bit al numero 170 (0000 0000 1010 1010). Il numero è un valore integer con segno.  
  
```  
  
~ 170  
```  
  
 L'espressione restituisce -170 (1111111101010101).  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
