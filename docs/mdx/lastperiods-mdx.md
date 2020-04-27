---
title: LastPeriods (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905781"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  Restituisce il set dei membri che precedono e includono un membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Indice*  
 Espressione numerica valida che specifica un numero di periodi.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Se il numero di periodi specificato è positivo, la funzione **LastPeriods** restituisce un set di membri che iniziano con il membro che fa ritardare *index* -1 dall'espressione del membro specificata e termina con il membro specificato. Il numero di membri restituiti dalla funzione è uguale a *index*.  
  
 Se il numero di periodi specificato è negativo, la funzione **LastPeriods** restituisce un set di membri che inizia con il membro specificato e termina con il membro che conduce (- *index* -1) dal membro specificato. Il numero di membri restituiti dalla funzione è uguale al valore assoluto di *index*.  
  
 Se il numero di periodi specificato è zero, la funzione **LastPeriods** restituisce il set vuoto. Questo è diverso dalla funzione **lag** , che restituisce il membro specificato se è specificato 0.  
  
 Se un membro non è specificato, la funzione **LastPeriods** utilizza **time. CurrentMember**. Se nessuna dimensione è contrassegnata come temporale, l'analisi e l'esecuzione della funzione verranno completate senza errori, ma si verificherà un errore a livello di cella nell'applicazione client.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il valore predefinito della misura per il secondo, il terzo e il quarto trimestre fiscale dell'anno fiscale 2002.  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  È inoltre possibile scrivere l'esempio utilizzando l'operatore Range (:).  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura per il primo trimestre fiscale dell'anno fiscale 2002. Benché il numero specificato di periodi sia tre, ne verrà restituito solo uno, in quanto non vi sono periodi precedenti nell'anno fiscale.  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
