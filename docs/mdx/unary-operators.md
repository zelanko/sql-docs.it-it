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
manager: kfile
ms.openlocfilehash: 6704d9a2fad8b1b19d7757c0e6de40bfccdcc1f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287795"
---
# <a name="unary-operators"></a>Operatori unari


  Nel linguaggio MDX (Multidimensional Expressions) gli operatori unari eseguono un'operazione su un singolo operando, ad esempio la restituzione del valore positivo o negativo di un'espressione numerica.  
  
 MDX supporta gli operatori unari elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
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
  
  
