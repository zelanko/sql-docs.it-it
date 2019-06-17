---
title: Se l'istruzione (MDX MultiDimensional Expression) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4975c455b942f053287b344a956a0083c8ca4e1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187509"
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
  
 *assignment*  
 Espressione MDX che assegna un valore a un sottocubo o a una proprietà calcolata.  
  
## <a name="remarks"></a>Note  
 Utilizzare l'istruzione IF per flusso di controllo, diversamente dal [IIf &#40;MDX&#41; ](../mdx/iif-mdx.md) (funzione) e il [istruzione CASE &#40;MDX&#41; ](../mdx/case-statement-mdx.md) che può essere utilizzato solo per restituire oggetti o valori.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'ambito è limitato al livello Country della gerarchia Geography nella dimensione Customers. Se la misura corrente è Internet Sales Amount, Internet Sales Amount viene impostato su 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
