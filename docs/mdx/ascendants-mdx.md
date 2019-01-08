---
title: I predecessori (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3122b3aa2f53da69f88e6ffad508f12c8e10da1c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404346"
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
  
## <a name="remarks"></a>Note  
 Il **predecessori** funzione restituisce tutti i predecessori di un membro del membro verso l'alto della gerarchia del membro; in particolare, esegue un attraversamento post-ordine della gerarchia per il membro specificato e quindi Restituisce che tutti i predecessori correlati al membro, incluso se stesso, in un set. È in contrasto con la [predecessore](../mdx/ancestor-mdx.md) funzione, che restituisce un membro specifico predecessori o predecessore, a un livello specifico.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce il numero di ordini dei rivenditori per il `[Sales Territory].[Northwest]` membro e tutti i predecessori di tale membro dal **Adventure Works** cubo. Il **predecessori** funzione costruisce il set che include il `[Sales Territory].[Northwest]` membro e i relativi predecessori per l'asse ROWS.  
  
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
  
  
