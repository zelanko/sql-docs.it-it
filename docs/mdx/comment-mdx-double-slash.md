---
description: Commenta la barra doppia MDX
title: Commento (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17f6a0d4220982007e7f742c11f197cb7b8b4dd6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487614"
---
# <a name="comment-mdx-double-slash"></a>Commenta la barra doppia MDX


  Evidenzia il testo inserito dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
// Comment_Text   
```  
  
#### <a name="parameters"></a>Parametri  
 *Comment_Text*  
 Stringa contenente il testo del commento.  
  
## <a name="remarks"></a>Osservazioni  
 I commenti possono essere inseriti su una riga distinta oppure nidificati alla fine di una riga di script MDX (Multidimensional Expressions) o in un'istruzione MDX. Nel server il commento non viene valutato.  
  
 Per commenti su una sola riga, utilizzare //. I commenti inseriti con // sono delimitati dal carattere di nuova riga.  
  
 I commenti possono essere di qualsiasi lunghezza.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
// This member returns the gross profit margin for product types  
// and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
      [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM // Select from the Adventure Works cube.  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Commento &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
