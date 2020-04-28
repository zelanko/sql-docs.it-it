---
title: Predecessori (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017065"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  Restituisce il set dei predecessori del membro specificato, incluso il membro stesso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **predecessores** restituisce tutti i predecessori di un membro dal membro stesso fino all'inizio della gerarchia del membro. in particolare, esegue un attraversamento post-ordine della gerarchia per il membro specificato, quindi restituisce tutti i membri predecessori correlati al membro, incluso se stesso, in un set. Si differenzia dalla funzione [predecessore](../mdx/ancestor-mdx.md) , che restituisce un membro predecessore specifico, o predecessore, a un livello specifico.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il numero di ordini rivenditore per il `[Sales Territory].[Northwest]` membro e tutti i predecessori di tale membro dal cubo **Adventure Works** . La funzione **predecessori** costruisce il set che include il `[Sales Territory].[Northwest]` membro e i relativi predecessori per l'asse delle righe.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
