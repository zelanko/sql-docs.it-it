---
title: Creazione con ambito sessione celle calcolate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- session-scoped calculated members [MDX]
ms.assetid: f2d14a89-6286-4e74-9afb-091076f93f21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4388ef278c0762184859162dc55f656aae1c9a15
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074434"
---
# <a name="creating-session-scoped-calculated-cells"></a>Creazione di celle calcolate con ambito sessione
    
> [!IMPORTANT]  
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
 Per creare celle calcolate disponibili a tutte le query di una stessa sessione, è possibile usare l'istruzione [CREATE CELL CALCULATION](/sql/mdx/mdx-data-definition-create-cell-calculation) oppure l'istruzione [ALTER CUBE](/sql/mdx/mdx-data-definition-alter-cube). Entrambe le istruzioni restituiscono lo stesso risultato.  
  
## <a name="create-cell-calculation-syntax"></a>Sintassi di CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
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
>  Questa sintassi è deprecata e deve essere sostituita da istruzioni MDX di assegnazione. Per altre informazioni sull'assegnazione, vedere [Script MDX di base &#40;MDX&#41;](the-basic-mdx-script-mdx.md).  
  
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
|Set di membri di un livello|Espressione set MDX che restituisce i membri di un singolo livello. Un esempio di questo è il *Level_Expression*.`Members` . Per includere i membri calcolati, usare il *Level_Expression*.`AllMembers` .<br /><br /> Per altre informazioni, vedere [AllMembers &#40;MDX&#41;](/sql/mdx/allmembers-mdx).|  
|Set di discendenti|Espressione set MDX che restituisce i discendenti di un membro specificato. Un esempio di questo è il `Descendants`(*Member_Expression*, *Level_Expression*, *Desc_Flag*) funzione MDX.<br /><br /> Per altre informazioni, vedere [Descendants &#40;MDX&#41;](/sql/mdx/descendants-mdx).|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di formule per il calcolo di celle in MDX &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)  
  
  
