---
title: DrillupMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5dfdec16d20173639cc92a80b1ca546f44b70334
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68049195"
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)


  Restituisce i membri di un set specificato che non sono discendenti dei membri di un secondo set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **DrillupMember** restituisce un set di membri in base ai membri specificati nel primo set che sono discendenti di membri nel secondo set. Il primo set può avere qualsiasi dimensionalità, mentre il secondo deve contenere un set unidimensionale. L'ordine tra i membri originali del primo set viene mantenuto. La funzione costruisce il set includendo solo i membri del primo set che sono discendenti immediati dei membri del secondo set. Se il predecessore immediato di un membro del primo set non è presente nel secondo set, il set restituito dalla funzione include il membro del primo set. Vengono inoltre inclusi i discendenti presenti nel primo set che precedono un membro predecessore del secondo set.  
  
 Il primo set può contenere tuple anziché membri. La funzione per il drill-down di tuple è un'estensione di OLE DB e restituisce un set di tuple anziché di membri.  
  
> [!IMPORTANT]  
>  Il drill-up di un membro verrà eseguito solo se il membro è seguito immediatamente da un elemento figlio o un discendente. L'ordine dei membri nel set è importante per le famiglie di\* funzioni drill\* -down e drillup. Prendere in considerazione l'uso della funzione **Hierarchize** per ordinare i membri del primo set in modo appropriato.  
  
## <a name="example"></a>Esempio  
 I tre esempi seguenti sono identici a eccezione del secondo set. Nel primo esempio, il secondo set è Stati Uniti. Di conseguenza, Colorado viene escluso dal set di risultati. È un discendente di Stati Uniti.  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 Il secondo esempio mostra l'importanza dell'ordine dei membri. Poiché **DrillupMember** esegue il drill-up solo dei membri immediatamente seguiti dai discendenti del primo set, non esegue il drill-up sul membro Canada. Canada è separato dal relativi discendenti da Stati Uniti e Colorado. Se si riordinano i membri in modo che Canada sia direttamente sopra Alberta, Alberta e Brunswick verranno esclusi dal set di righe.  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 Nell'esempio tre viene illustrato come l'utilizzo di **Hierarchize** può attenuare gli effetti dell'ordine dei membri e il drill-up del membro Canada.  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
