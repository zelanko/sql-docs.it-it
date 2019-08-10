---
title: Istruzione CREATE CELL CALCULATION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7ba563c848179e8cf3dc12f64d2b3c4233955159
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892161"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>Definizione dei dati MDX - CREATE CELL CALCULATION


  Crea una formula di calcolo che valuta un'espressione MDX (Multidimensional Expression) su un set di tuple specificato all'interno di un cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Stringa valida che specifica il nome di un cubo.  
  
 *Calculation_Name*  
 Stringa valida che specifica il nome di una formula per il calcolo di celle.  
  
 *Set_Expression*  
 Espressione MDX valida che restituisce un set.  
  
 *String*  
 Valore stringa valido.  
  
 *MDX_Expression*  
 Espressione MDX valida.  
  
 *Logical_Expression*  
 Espressione logica MDX valida.  
  
 *Integer*  
 Valore integer valido.  
  
 *Calculation_Name*  
 Stringa valida che specifica il nome per la proprietà di calcolo di una cella.  
  
 *Scalar_Expression*  
 Espressione scalare MDX valida.  
  
## <a name="remarks"></a>Note  
 Utilizzando celle calcolate, l'applicazione client può specificare un valore di rollup per un particolare set di celle, anziché per un intero set di celle come avviene nel caso di un membro calcolato o di una formula di rollup personalizzata. È ad esempio possibile specificare che tutte le celle nel set definito da `{[Canada],[Time].[2000]}` possono contenere un valore definito da una formula. Tutte le altre celle non contenute nel set vengono calcolate normalmente.  
  
> [!NOTE]  
>  Per compatibilità con le versioni precedenti, la sintassi BNF di `{*(<comment> | <whitespace> | <newline>)}` verrà analizzata come `{*}`.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di celle calcolate con ambito sessione](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [Creazione di formule per il calcolo di celle con ambito query &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [Compilazione di calcoli di celle &#40;in MDX MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [Utilizzo delle proprietà delle celle &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [Contenuto di FORMAT_STRING &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [Contenuto &#40;di FORE_COLOR e BACK_COLOR MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [MDX-istruzioni &#40;per la definizione dei dati MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
