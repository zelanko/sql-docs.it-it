---
title: Commento (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f0aa1455ffd9f52fd917f68d2bb0bb80e3f25a94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006270"
---
# <a name="comment-mdx"></a>Commento (MDX)


  Indica un testo di commento specificato dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
/* Comment_Text */      
```  
  
#### <a name="parameters"></a>Parametri  
 *Comment_Text*  
 Stringa contenente il testo del commento.  
  
## <a name="remarks"></a>Osservazioni  
 Il server non valuta il testo tra i caratteri di commento,/* e \*/. I commenti possono essere inseriti in una riga distinta o sulla stessa riga di un'istruzione MDX (Multidimensional Expressions). I commenti su più righe devono essere indicati da\* / \*e/.  
  
 I commenti possono essere di qualsiasi lunghezza. e nidificati, ad esempio `/* Test /*Comment*/ Text*/`.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore.  
  
```  
/* This member returns the gross profit margin for product types  
  and reseller types crossjoined by year. */  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM /* Select from the Adventure Works cube. */  
    [Adventure Works]  
WHERE  
    [Measures].[Gross Profit Margin]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;commento&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)   
 [--&#40;commento&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
