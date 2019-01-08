---
title: '- (negazione) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 587ac12e6628104613d8b1457b02088e1baf4998
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799843"
---
# <a name="--negate-ssis-expression"></a>- (negazione) (espressione SSIS)
  Viene applicato un segno negativo a un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione valida con qualsiasi tipo di dati numeric. Sono supportati solo i tipi di dati numeric con segno. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipi restituiti  
 Restituisce il tipo di dati di *numeric_expression*.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene applicato un segno negativo al valore della variabile **Counter** e viene aggiunto il valore letterale numerico 50.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
