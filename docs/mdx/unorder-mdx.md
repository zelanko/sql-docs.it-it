---
title: Unorder-(MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
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
  
## <a name="remarks"></a>Note  
 Il **Unorder=1=«set»=restituisce** funzione rimuove qualsiasi ordinamento imposto sulle tuple contenute nel set da qualsiasi altra funzione o istruzione, ad esempio le [ordine](../mdx/order-mdx.md) (funzione). L'ordinamento delle tuple nel set restituito per il **Unorder=1=«set»=restituisce** funzione è indeterminato.  
  
 Il **Unorder=1=«set»=restituisce** funzione viene utilizzata come un hint di ottimizzazione delle query per l'elaborazione di set. Se l'ordine delle tuple all'interno di un set non ha importanza per un calcolo o una query, usando il **Unorder=1=«set»=restituisce** funzione può fornire un miglioramento delle prestazioni in questi casi. Ad esempio, il [NonEmpty (MDX)](../mdx/nonempty-mdx.md) funzione siano migliori quando il set specificato per questa funzione è ordinato rispetto ai casi [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] venga mantenuto un ordine, anche se con [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], query processor tenta di eseguire Questa funzione automaticamente per molte funzioni, ad esempio **somma** e **aggregazione**. Il miglioramento delle prestazioni di utilizzo **Unorder=1=«set»=restituisce** solo è apprezzabile in set molto grandi, costituiti da milioni di tuple.  
  
## <a name="example"></a>Esempio  
 Nello pseudocodice seguente viene illustrata la sintassi per questa funzione.  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
