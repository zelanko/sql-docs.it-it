---
title: Utilizzo di espressioni membro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d40d6a3b6cacb65cf1463b0eeb8b29e59e079e4
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893508"
---
# <a name="using-member-expressions"></a>Utilizzo delle espressioni di membro


  Un'espressione di membro contiene un identificatore di membro, una funzione per i membri o un'espressione che può essere convertita in un membro.  
  
 Gli identificatori di membro possono avere molti formati diversi. Il formato più semplice di un identificatore di membro è costituito dal nome del membro. Ad esempio:  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 Tuttavia, se vi sono numerosi membri con lo stesso nome su differenti gerarchie, non sarà possibile in alcun modo determinare quale membro sarà restituito dalla query. Ad esempio, nella query seguente vengono richiesti dei dati per un membro con il nome [CY 2004]. La query viene eseguita correttamente, ma vengono individuati almeno sei membri con quel nome nel cubo di Adventure Works:  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 Pertanto, il formato più affidabile per un identificatore di membro è il nome univoco del membro che garantisce l'identificazione di uno specifico membro in un cubo. In Analysis Services è possibile generare nomi univoci in diversi modi, ma un nome univoco è sempre composto da almeno due identificatori: il nome della dimensione e il nome del membro o chiave membro. Un nome univoco ha il seguente formato:  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 Di seguito vengono riportati alcuni esempi di nomi univoci di membro dal cubo di Adventure Works:  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 Sono molte le funzioni MDX che restituiscono membri. Per un elenco completo, vedere [MDX &#40;&#41; per riferimento alle funzioni MDX](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  Per ulteriori informazioni sui nomi dei membri e sulle chiavi dei membri, vedere [utilizzo di membri, Tuple &#40;e&#41;set MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx).  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
