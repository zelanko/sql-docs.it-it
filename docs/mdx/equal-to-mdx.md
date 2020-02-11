---
title: = (Uguale a) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 189facb54de244ff220b41ec08c8b02faf5a2c27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139321"
---
# <a name="-equal-to-mdx"></a>= (uguale a) (MDX)


  Esegue un'operazione di confronto che determina se il valore di un'espressione MDX (Multidimensional Expression) è uguale a quello di un'altra espressione MDX.  
  
> [!NOTE]  
>  Per confrontare gli oggetti, utilizzare l'operatore [&#41;&#40;MDX](../mdx/is-mdx.md) . Ad esempio, utilizzare l'operatore IS per controllare se il membro corrente su un asse della query è un membro specifico.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parametri  
 *MDX_Expression*  
 Espressione MDX valida.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano basato sulle condizioni seguenti:  
  
-   **true** se il valore del primo parametro è uguale al valore del secondo parametro.  
  
-   **false** se il valore del primo parametro non è uguale al valore del secondo parametro.  
  
-   **true** se entrambi i parametri sono null o se un parametro è null e l'altro parametro è 0.  
  
## <a name="examples"></a>Esempi  
 Nella query seguente vengono illustrati degli esempi relativi a queste condizioni:  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)  
  
  
