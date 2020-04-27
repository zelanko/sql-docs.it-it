---
title: IsEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8b31b884e0f86bf2aebe4859cd1c7a441669e813
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905995"
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)


  Indica se l'espressione valutata corrisponde al valore di cella vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Value_Expression*  
 Espressione MDX (Multidimensional Expression) valida che in genere restituisce le coordinate delle celle di un membro o di una tupla.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **IsEmpty** restituisce **true** se l'espressione valutata è un valore di cella vuota. In caso contrario, la funzione restituisce **false**.  
  
> [!NOTE]  
>  La proprietà predefinita di un membro è costituita dal valore del membro.  
  
 La funzione **IsEmpty** è l'unico modo per verificare in modo affidabile una cella vuota, perché il valore di cella vuota ha un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]significato speciale in.  
  
> [!IMPORTANT]  
>  Se la valutazione dell'espressione valore restituisce un errore, la funzione restituirà **false**. Un'espressione valore può restituire un errore, ad esempio, se in un riferimento alle proprietà viene fatto riferimento a una proprietà non valida o inesistente.  
  
 Per ulteriori informazioni sulle celle vuote, vedere la documentazione relativa a OLE DB.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito TRUE se il valore Internet Sales Amount per il membro corrente della gerarchia Fiscal nella dimensione Date restituisce una cella vuota:  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedi anche  
 [Utilizzo di valori vuoti](../mdx/working-with-empty-values.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
