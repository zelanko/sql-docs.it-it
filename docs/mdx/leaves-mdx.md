---
description: Leaves (MDX)
title: Foglie (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7beab859a2953b3eba52e74d97bed5718c59ea90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387307"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  Restituisce un set composto da tutti gli attributi (facoltativamente limitato a quelli appartenenti a una dimensione specifica). Per ogni attributo x nel set restituito, se x è l'attributo di granularità o è correlato direttamente o indirettamente all'attributo di granularità, la granularità viene impostata sull'attributo x senza influire sulla sezione. La funzione **leaves** è progettata per essere usata all'interno di un'istruzione Scope o sul lato sinistro di un'assegnazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Dimension_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una dimensione.  
  
## <a name="remarks"></a>Osservazioni  
 I membri foglia sono tuple ottenute eseguendo il cross join del livello più basso di tutte le gerarchie dell'attributo. I membri calcolati vengono esclusi.  
  
-   Se viene specificato un nome di dimensione, la funzione **leaves** restituisce un set che contiene i membri foglia dell'attributo chiave per la dimensione specificata.  
  
-   Se la dimensione è associata a più gruppi di misure, viene utilizzato il gruppo nell'ambito corrente.  
  
-   Se non si specifica un nome di dimensione, la funzione restituirà un set che contiene i membri foglia dell'intero cubo.  
  
    > [!NOTE]  
    >  Se l'espressione di dimensione viene risolta in una gerarchia e il nome univoco della gerarchia è uguale a quello della dimensione (la proprietà HierarchyUniqueNameStyle della dimensione del cubo è ExcludeDimensionName e il nome della gerarchia corrisponde al nome della dimensione), viene utilizzata la dimensione.  
  
    > [!IMPORTANT]  
    >  Se la granularità nei gruppi di misure nell'ambito corrente non è la stessa per tutti gli attributi, viene generato un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
