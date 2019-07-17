---
title: Istruzione SCOPE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f355842999b505a97c3387ab9e51d3b651c3b7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138276"
---
# <a name="mdx-scripting---scope"></a>Scripting MDX - SCOPE


  Limita l'ambito delle istruzioni MDX (Multidimensional Expression) specificate a un sottocubo specifico.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Subcube_Expression*  
 Espressione di sottocubo MDX valida.  
  
 *MDX_Statement*  
 Istruzione MDX valida.  
  
 *Common_Grain_Members*  
 Istruzione MDX valida che restituisce i membri allo stesso livello di dettaglio.  
  
 *single_tuple*  
 Una tupla singola.  
  
## <a name="remarks"></a>Note  
 L'istruzione SCOPE determina il sottocubo che interessato dall'esecuzione di una o più istruzioni MDX. Se l'istruzione MDX non è racchiusa all'interno di un'istruzione SCOPE, il suo ambito implicito è l'intero cubo.  
  
> [!NOTE]  
>  In una istruzione SCOPE i membri nascosti vengono esposti.  
  
 Istruzioni SCOPE creano sottocubi che espongono "buchi" indipendentemente i **MDX Compatibility** impostazione. L'istruzione `Scope( Customer.State.members )`, ad esempio, può includere gli stati per aree o paesi che non contengono stati ma al posto dei quali sono stati inseriti membri segnaposto altrimenti invisibili.  
  
 L'istruzione SCOPE non ha effetto sui membri calcolati e sui set denominati creati all'interno dell'istruzione SCOPE.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, lo script di calcolo MDX in Adventure Works soluzione di esempio, definisce l'ambito corrente come trimestre fiscale dell'anno fiscale 2005 e la misura di sales amount quota e quindi assegna un valore alle celle nell'ambito corrente usando il  **ParallelPeriod** (funzione). Nell'esempio viene quindi modificato l'ambito utilizzando un'altra istruzione SCOPE e quindi esegue un'altra assegnazione mediante la [This (MDX)](../mdx/this-mdx.md) (funzione).  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di scripting MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
