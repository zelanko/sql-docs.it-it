---
title: '&lt;&gt; (Non uguale a) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088323"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (Non uguale a) (MDX)


  Esegue un'operazione di confronto che determina se il valore di un'espressione MDX (Multidimensional Expression) è diverso da quello di un'altra espressione MDX.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *MDX_Expression*  
 Espressione MDX valida.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano basato sulle condizioni seguenti:  
  
-   **true** se entrambi i parametri sono non null e il primo parametro non è uguale al secondo parametro.  
  
-   **false** se entrambi i parametri sono non null e il primo parametro è uguale al secondo parametro.  
  
-   Null se uno o entrambi i parametri restituiscono un valore Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
