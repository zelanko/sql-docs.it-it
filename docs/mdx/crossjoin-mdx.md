---
description: Crossjoin (MDX)
title: Crossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 759feb8b64a06e6238d338d4d619dd1433819dda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387537"
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)


  Restituisce il prodotto incrociato di uno o più set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Crossjoin** restituisce il prodotto incrociato di due o più set specificati. L'ordine delle tuple nel set di risultati dipende dall'ordine dei set da unire e dall'ordine dei membri corrispondenti. Ad esempio, quando il primo set è costituito da {x1, X2,..., x*n*} e il secondo set è costituito da {Y1, Y2,..., y*n*}, il prodotto incrociato di questi set è:  
  
 {(x1, Y1), (x1, Y2),..., (x1, y*n*), (X2, Y1), (X2, y2),...,  
  
 (X2, y*n*),..., (x*n*, Y1), (x*n*, Y2),..., (Xn, y*n*)}  
  
> [!IMPORTANT]  
>  Se i set nel cross join sono costituiti da tuple di gerarchie dell'attributo diverse contenute nella stessa dimensione, questa funzione restituirà solo le tuple effettivamente esistenti. Per ulteriori informazioni, vedere [concetti chiave in MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services).  
  
## <a name="examples"></a>Esempi  
 Nella query seguente vengono illustrati esempi semplici dell'utilizzo della funzione Crossjoin sull'asse delle colonne e delle righe di una query:  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 Nell'esempio seguente viene illustrata l'applicazione di filtri automatica che si verifica quando a gerarchie diverse dalla stessa dimensione viene applicato il crossjoin:  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 Nei tre esempi seguenti vengono restituiti gli stessi risultati, ovvero il valore di Internet Sales Amount per i vari stati degli Stati Uniti. Nei primi casi due vengono utilizzate le due sintassi cross join e nel terzo viene dimostrato l'utilizzo della clausola WHERE per restituire le stesse informazioni.  
  
### <a name="example-1"></a>Esempio 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>Esempio 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>Esempio 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
