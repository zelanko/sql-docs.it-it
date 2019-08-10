---
title: Operatori unari | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9ec9ac3eef28c4deae08d577487599575852c132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893549"
---
# <a name="unary-operators"></a>Operatori unari


  Nel linguaggio MDX (Multidimensional Expressions) gli operatori unari eseguono un'operazione su un singolo operando, ad esempio la restituzione del valore positivo o negativo di un'espressione numerica.  
  
 MDX supporta gli operatori unari elencati nella tabella seguente.  
  
|Operator|Descrizione|  
|--------------|-----------------|  
|[- (negativo)](../mdx/negative-mdx.md)|Restituisce l'opposto del valore di un'espressione numerica.|  
|[+ (positivo)](../mdx/positive-mdx.md)|Restituisce il valore positivo di un'espressione numerica.|  
  
 Nell'esempio seguente viene illustrato l'utilizzo di un operatore unario per la restituzione dell'opposto del valore di una misura:  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Inoltre, MDX utilizza gli operatori unari speciali per determinare l'operazione di aggregazione eseguita dalla funzione [RollupChildren](../mdx/rollupchildren-mdx.md) . Per ulteriori informazioni su questi operatori unari speciali, vedere [aggiungere un'aggregazione personalizzata a una dimensione](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension).  
  
## <a name="see-also"></a>Vedere anche  
 [Sintassi &#40;MDX degli operatori&#41;](../mdx/operators-mdx-syntax.md)  
  
  
