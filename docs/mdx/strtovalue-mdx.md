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
ms.openlocfilehash: cad8fec605a56a60cfcc7024739225e474fd42f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036696"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Restituisce il valore numerico specificato da una stringa in formato MDX (Multidimensional Expression).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *MDX_Expression*  
 Espressione stringa valida che viene risolta, direttamente o indirettamente, in una singola cella.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **StrToValue** restituisce il valore numerico specificato dall'espressione MDX. La funzione **StrToValue** viene in genere utilizzata con funzioni definite dall'utente per restituire un'espressione MDX da una funzione esterna a un'istruzione MDX che può essere risolta in un'unica cella.  
  
-   Quando viene utilizzato il flag CONSTRAINED, l'espressione MDX deve contenere solo un valore scalare. Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se si specifica un'espressione MDX non direttamente risolvibile in un valore scalare, viene visualizzato l'errore seguente: "Le restrizioni imposte dal flag CONSTRAINED nella funzione STRTOVALUE sono state violate".  
  
-   Quando non viene utilizzato il flag CONSTRAINED, non esistono limiti alla complessità dell'espressione MDX specificata, purché si risolva in un'espressione MDX (Multidimensional Expression) valida che restituisce una singola cella.  
  
> [!NOTE]  
>  La restituzione del risultato di un'espressione MDX come valore numerico è particolarmente utile se tale valore viene archiviato come testo e se si desidera utilizzare i valori restituiti per l'esecuzione di operazioni aritmetiche.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usata la funzione **StrToValue** per restituire il peso di ogni bicicletta come valore.  
  
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
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
