---
title: StrToValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c327dc55420cc89f5e76b6fae7822fad3a4e95f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136106"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Restituisce il valore numerico specificato da una stringa di formato Multidimensional.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *MDX_Expression*  
 Espressione stringa valida che viene risolta, direttamente o indirettamente, in una singola cella.  
  
## <a name="remarks"></a>Note  
 Il **StrToValue** funzione restituisce il valore numerico specificato dall'espressione MDX. Il **StrToValue** funzione viene in genere utilizzata con funzioni definite dall'utente per la restituzione di un'espressione MDX da una funzione esterna a un'istruzione MDX che può essere risolta in una singola cella.  
  
-   Quando viene utilizzato il flag CONSTRAINED, l'espressione MDX deve contenere solo un valore scalare. Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se un'espressione MDX non direttamente risolvibile in un valore scalare, viene visualizzato l'errore seguente: "Le restrizioni imposte dal CONSTRAINED flag nella funzione STRTOVALUE sono state violate."  
  
-   Quando non viene utilizzato il flag CONSTRAINED, non esistono limiti alla complessità dell'espressione MDX specificata, purché si risolva in un'espressione MDX (Multidimensional Expression) valida che restituisce una singola cella.  
  
> [!NOTE]  
>  La restituzione del risultato di un'espressione MDX come valore numerico è particolarmente utile se tale valore viene archiviato come testo e se si desidera utilizzare i valori restituiti per l'esecuzione di operazioni aritmetiche.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa il **StrToValue** funzione per restituire il peso di ogni bicicletta come valore.  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
