---
title: Operatori di concatenazione | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8eacfc08fdeb0f92874758d0f95e5cde3e6b295a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181482"
---
# <a name="concatenation-operators"></a>Operatori di concatenazione


  L'operatore di concatenazione è rappresentato dal segno più (+). È possibile combinare, o concatenare, due o più stringhe di caratteri in modo da formare una singola stringa, nonché concatenare stringhe binarie.  
  
 Nell'esempio di codice seguente l'operatore di concatenazione viene utilizzato per combinare il nome di un prodotto con il nome univoco del prodotto:  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>Considerazioni sul linguaggio  
 Se le stringhe utilizzate in un'operazione di concatenazione hanno le stesse regole di confronto, le regole di confronto dell'input verranno utilizzate anche per la stringa risultante dalla concatenazione. Se invece le stringhe utilizzate in un'operazione di concatenazione hanno regole di confronto diverse, le regole di confronto della stringa risultante dalla concatenazione verranno determinate in base alla precedenza delle regole di confronto. Per altre informazioni, vedere [Lingue e regole di confronto &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Gli operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
