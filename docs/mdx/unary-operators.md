---
title: Gli operatori unari | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1bb0dcbd16fc96cb587718504de8fa43babd0db6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097361"
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
  
 Inoltre, MDX utilizzare speciali operatori unari per determinare l'operazione di aggregazione eseguita dal [RollupChildren](../mdx/rollupchildren-mdx.md) (funzione). Per altre informazioni su questi operatori unari speciali, vedere [aggiungere un'aggregazione personalizzata a una dimensione](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gli operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
