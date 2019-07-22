---
title: '- (negazione) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4224a49bc5464a6f175972db5c93a9f84edbc874
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968087"
---
# <a name="--negate-ssis-expression"></a>- (negazione) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene applicato un segno negativo a un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione valida con qualsiasi tipo di dati numeric. Sono supportati solo i tipi di dati numeric con segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Restituisce il tipo di dati di *numeric_expression*.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene applicato un segno negativo al valore della variabile **Counter** e viene aggiunto il valore letterale numerico 50.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
