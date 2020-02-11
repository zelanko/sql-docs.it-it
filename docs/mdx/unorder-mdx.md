---
title: Unorder (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097262"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  Rimuove l'ordinamento imposto da un set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Unorder** rimuove qualsiasi ordinamento imposto nelle tuple contenute nel set da qualsiasi altra funzione o istruzione, ad esempio la funzione [Order](../mdx/order-mdx.md) . L'ordinamento delle tuple nel set restituito dalla funzione **Unorder** è indeterminato.  
  
 La funzione **Unorder** viene utilizzata come hint per l'ottimizzazione delle query per l'elaborazione dei set. Se l'ordine delle tuple all'interno di un set non è importante per un calcolo o una query, l'utilizzo della funzione **Unorder** può offrire un vantaggio in merito alle prestazioni in tali casi. Ad esempio, la [funzione NonEmpty (MDX)](../mdx/nonempty-mdx.md) può offrire prestazioni migliori quando il set fornito a questa funzione non è ordinato rispetto a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] quando deve mantenere l'ordine, sebbene [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]con, query processor tenti di eseguire automaticamente questa funzione per molte funzioni, ad esempio **Sum** e **Aggregate**. Il vantaggio in merito alle prestazioni derivante dall'utilizzo di **Unorder** è probabilmente visibile solo su set di grandi dimensioni costituiti da milioni di Tuple.  
  
## <a name="example"></a>Esempio  
 Nello pseudocodice seguente viene illustrata la sintassi per questa funzione.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
