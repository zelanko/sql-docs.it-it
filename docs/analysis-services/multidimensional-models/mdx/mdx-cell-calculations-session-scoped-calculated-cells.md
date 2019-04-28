---
title: Creazione con ambito sessione celle calcolate | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ca621d103f294a88fec93dbf6f24d7402279efa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62799547"
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>Calcoli di celle MDX - con ambito sessione celle calcolate
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Per creare celle calcolate disponibili a tutte le query di una stessa sessione, è possibile usare l'istruzione [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) oppure l'istruzione [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md). Entrambe le istruzioni restituiscono lo stesso risultato.  
  
## <a name="create-cell-calculation-syntax"></a>Sintassi di CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Per utilizzare l'istruzione CREATE CELL CALCULATION per definire una cella calcolata con ambito sessione, utilizzare la sintassi seguente:  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>Sintassi di ALTER CUBE  
  
> [!IMPORTANT]  
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Per utilizzare l'istruzione ALTER CUBE per definire una cella calcolata con ambito sessione, utilizzare la sintassi seguente:  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 Il valore `String_Expression` contiene un elenco di espressioni set MDX unidimensionali ortogonali, ognuna delle quali deve essere risolta in una delle categorie di set elencate nella tabella seguente.  
  
|Category|Descrizione|  
|--------------|-----------------|  
|Set vuoto|Espressione set MDX che restituisce un set vuoto. In questo caso l'ambito della cella calcolata è costituito dall'intero cubo.|  
|Set con un singolo membro|Espressione set MDX che restituisce un singolo membro.|  
|Set di membri di un livello|Espressione set MDX che restituisce i membri di un singolo livello. Un esempio è la funzione MDX *Level_Expression*.**Members** . Per includere i membri calcolati, usare la funzione MDX *Level_Expression*.**AllMembers** .<br /><br /> Per altre informazioni, vedere [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Set di discendenti|Espressione set MDX che restituisce i discendenti di un membro specificato. Un esempio è la funzione MDX **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*).<br /><br /> Per altre informazioni, vedere [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di formule per il calcolo di celle in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
