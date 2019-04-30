---
title: DataMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98b10c951043416280c05fd6a0e5eeb5df92c104
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248134"
---
# <a name="datamember-mdx"></a>DataMember (MDX)


  Restituisce il membro dei dati generato dal sistema associato a un membro non foglia di una dimensione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.DataMember  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 Questa funzione opera su membri non foglia in una gerarchia qualsiasi e può essere usata dal [UPDATE CUBE Statement (MDX)](../mdx/mdx-data-manipulation-update-cube.md) comando per i dati writeback per un membro non foglia direttamente, anziché per i discendenti del membro foglia.  
  
> [!NOTE]  
>  Restituisce il membro specificato se tale membro è un membro foglia o se al membro non foglia non è associato alcun membro dei dati.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa il **DataMember** funzione in una misura calcolata per illustrare la quota di vendite per ogni singolo dipendente:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
