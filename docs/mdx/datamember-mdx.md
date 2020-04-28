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
ms.openlocfilehash: 4395f0ff113c8549ec2250d5fa87d37090627b3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892908"
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
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione opera sui membri non foglia di una gerarchia e può essere utilizzata dal comando [UPDATE CUBE Statement (MDX)](../mdx/mdx-data-manipulation-update-cube.md) per eseguire il writeback diretto dei dati a un membro non foglia, anziché ai discendenti del membro foglia.  
  
> [!NOTE]  
>  Restituisce il membro specificato se tale membro è un membro foglia o se al membro non foglia non è associato alcun membro dei dati.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la funzione **DataMember** in una misura calcolata per mostrare la quota di vendite per ogni singolo dipendente:  
  
```  
WITH MEMBER measures.InvidualQuota AS   
([Employee].[Employees].currentmember.datamember, [Measures].[Sales Amount Quota])  
,FORMAT_STRING='Currency'  
SELECT {[Measures].[Sales Amount Quota],[Measures].InvidualQuota} ON COLUMNS,  
[Employee].[Employees].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [Concetti chiave di MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)  
  
  
