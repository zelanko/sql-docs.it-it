---
title: '- (Except) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 618beda530627898cdf55f08be5071fd7568688c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690865"
---
# <a name="except-mdx-operator"></a>Ad eccezione di operatore (MDX)


  Esegue un'operazione sui set che restituisce la differenza tra due set, rimuovendo i membri duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="return-value"></a>Valore restituito  
 Set che include i membri non presenti in entrambi i parametri specificati.  
  
## <a name="remarks"></a>Note  
 Il **- (eccezione)** è funzionalmente equivalente all'operatore le [tranne](../mdx/except-mdx-function.md) (funzione).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo di questo operatore:  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
