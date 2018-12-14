---
title: Operatori (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1cb952d965c2ddb316b0890a03e2d10947c2e61a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766833"
---
# <a name="operators-ssis-expression"></a>Operatori (espressione SSIS)
  In questa sezione vengono descritti gli operatori disponibili nel linguaggio delle espressioni, nonché le regole di associatività e precedenza degli operatori utilizzate dall'analizzatore di espressioni.  
  
 Nella tabella seguente sono elencati gli argomenti dedicati agli operatori disponibili in questa sezione.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[Cast &#40;espressione SSIS&#41;](cast-ssis-expression.md)|Converte un'espressione da un tipo di dati a un altro.|  
|[&#40;&#41; &#40;parentesi&#41; &#40;espressione SSIS&#41;](parentheses-ssis-expression.md)|Viene identificato l'ordine di valutazione delle espressioni.|  
|[+ &#40;addizione&#41; &#40;espressione SSIS&#41;](add-ssis.md)|Vengono aggiunte due espressioni numeriche.|  
|[+ &#40;concatenazione&#41; &#40;espressione SSIS&#41;](concatenate-ssis-expression.md)|Concatena due espressioni.|  
|[- &#40;sottrazione&#41; &#40;espressione SSIS&#41;](subtract-ssis-expression.md)|Viene sottratta la seconda espressione numerica dalla prima.|  
|[- &#40;negazione&#41; &#40;espressione SSIS&#41;](negate-ssis-expression.md)|Viene applicato un segno negativo a un'espressione numerica.|  
|[&#42; &#40;moltiplicazione&#41; &#40;espressione SSIS&#41;](multiply-ssis-expression.md)|Vengono moltiplicate due espressioni numeriche.|  
|[Divisione &#40;espressione SSIS&#41;](divide-ssis-expression.md)|Viene divisa la prima espressione numerica per la seconda.|  
|[&#40;modulo&#41; &#40;espressione SSIS&#41;](modulo-ssis-expression.md)|Viene restituito il resto Integer dopo aver diviso la prima espressione numerica per la seconda.|  
|[&#124;&#124; &#40;OR logico&#41; &#40;espressione SSIS&#41;](logical-or-ssis-expression.md)|Viene eseguita un'operazione con OR logico.|  
|[&& &#40;AND logico&#41; &#40;espressione SSIS&#41;](logical-and-ssis-expression.md)|Viene eseguita un'operazione con AND logico.|  
|[\! &#40;NOT logico&#41; &#40;espressione SSIS&#41;](logical-not-ssis-expression.md)|NOT logico di un operando booleano.|  
|[&#124; &#40;OR inclusivo bit per bit&#41; &#40;espressione SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)|Viene eseguita un'operazione con OR bit per bit su due valori integer.|  
|[^ &#40;OR esclusivo bit per bit&#41; &#40;Espressione SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)|Viene eseguita un'operazione con OR esclusivo bit per bit su due valori integer.|  
|[& &#40;AND bit per bit&#41; &#40;espressione SSIS&#41;](bitwise-and-ssis-expression.md)|Esegue un'operazione con AND bit per bit tra due valori integer.|  
|[~ &#40;NOT bit per bit&#41; &#40;espressione SSIS&#41;](bitwise-not-ssis-expression.md)|Viene eseguita una negazione bit per bit di un valore integer.|  
|[== &#40;uguale&#41; &#40;espressione SSIS&#41;](equal-ssis-expression.md)|Viene eseguito un confronto per determinare se due espressioni sono uguali.|  
|[\!= &#40;diverso da&#41; &#40;espressione SSIS&#41;](unequal-ssis-expression.md)|Esegue un confronto per determinare se due espressioni sono diverse.|  
|[&#62; &#40;maggiore di&#41; &#40;espressione SSIS&#41;](greater-than-ssis-expression.md)|Esegue un confronto per determinare se la prima espressione è maggiore della seconda.|  
|[&#60; &#40;minore di&#41; &#40;espressione SSIS&#41;](less-than-ssis-expression.md)|Viene eseguito un confronto per determinare se la prima espressione è minore della seconda.|  
|[&#62;= &#40;maggiore o uguale a&#41; &#40;espressione SSIS&#41;](greater-than-or-equal-to-ssis-expression.md)|Viene eseguito un confronto per determinare se la prima espressione è maggiore o uguale alla seconda.|  
|[&#60;= &#40;minore o uguale a&#41; &#40;espressione SSIS&#41;](less-than-or-equal-to-ssis-expression.md)|Viene eseguito un confronto per determinare se la prima espressione è minore o uguale alla seconda.|  
|[? : &#40;condizionale&#41; &#40;espressione SSIS&#41;](conditional-ssis-expression.md)|Viene restituita una di due espressioni in base alla valutazione di un'espressione booleana.|  
  
 Per informazioni sulla posizione di ogni operatore nella gerarchia delle precedenze, vedere [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)   
 [Esempi di espressioni avanzate di Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)  
  
  
