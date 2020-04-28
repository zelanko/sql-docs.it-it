---
title: Istruzione IF (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41bd34fbd3d296f4aa38877e6d26e25eba9ae726
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68138686"
---
# <a name="mdx-scripting---if"></a>Scripting MDX - IF


  Esegue una determinata istruzione se la condizione specificata è soddisfatta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Espressione MDX (Multidimensional Expression) che restituisce un valore booleano, true o false.  
  
 *assegnazione*  
 Espressione MDX che assegna un valore a un sottocubo o a una proprietà calcolata.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare l'istruzione IF per il flusso di controllo, diversamente dalla funzione [IIf &#40;mdx&#41;](../mdx/iif-mdx.md) e dall' [istruzione case &#40;&#41;MDX](../mdx/case-statement-mdx.md) che possono essere utilizzati solo per restituire valori o oggetti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'ambito è limitato al livello Country della gerarchia Geography nella dimensione Customers. Se la misura corrente è Internet Sales Amount, Internet Sales Amount viene impostato su 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
