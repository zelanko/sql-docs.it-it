---
title: -(Commento) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc8bf49f6d25c4e00c2d5693ff6a9cf48d5450ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208759"
---
# <a name="comment---mdx-operator-reference"></a>Comment - riferimento agli operatori MDX


  Indica un testo di commento specificato dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
-- Comment_Text      
```  
  
#### <a name="parameters"></a>Parametri  
 *Comment_Text*  
 Stringa contenente il testo del commento.  
  
## <a name="remarks"></a>Note  
 I commenti possono essere inseriti su una riga distinta oppure nidificati alla fine di una riga di script MDX (Multidimensional Expressions) o in un'istruzione MDX. Nel server il commento non viene valutato.  
  
 Utilizzare questo operatore per commenti su una sola riga o nidificati. I commenti inseriti con -- sono delimitati dal carattere di nuova riga.  
  
 I commenti possono essere di qualsiasi lunghezza.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
-- This member returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM -- Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Commento &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [&#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
