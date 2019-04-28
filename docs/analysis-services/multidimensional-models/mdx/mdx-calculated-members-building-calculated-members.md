---
title: Compilazione di membri calcolati in MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9235b9e3531e2ca40cabe211d85c077e629dacee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806135"
---
# <a name="mdx-calculated-members---building-calculated-members"></a>Membri calcolati MDX - Creazione di membri calcolati
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  In MDX (Multidimensional Expressions) un membro calcolato viene definito come membro che è stato risolto tramite il calcolo di un'espressione MDX per la restituzione di un valore. Dietro a questa definizione apparentemente semplice si nasconde un'enorme quantità di informazioni. La capacità di creare e utilizzare membri calcolati in una query MDX offre capacità notevoli per la manipolazione dei dati multidimensionali.  
  
 I membri calcolati possono essere creati in qualsiasi posizione di una gerarchia. È inoltre possibile creare membri calcolati dipendenti non solo dai membri esistenti di un cubo, ma anche da altri membri calcolati definiti nella stessa espressione MDX.  
  
 È possibile definire un membro calcolato in modo da associarvi uno dei contesti seguenti:  
  
-   **Con ambito query** Per creare un membro calcolato definito come parte di una query MDX e il cui ambito è pertanto limitato alla query, è necessario specificare la parola chiave WITH. Il membro calcolato può essere utilizzato quindi in un'istruzione MDX SELECT. In tal modo, è possibile modificare il membro calcolato creato utilizzando la parola chiave WITH senza alterare l'istruzione SELECT.  
  
     Per altre informazioni sulla creazione di membri calcolati mediante la parola chiave WITH, vedere [Creazione di formule per il calcolo di celle con ambito query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Con ambito sessione** Per creare un membro calcolato il cui ambito risulti più ampio del contesto della query, ovvero il cui ambito corrisponde alla durata della sessione MDX, è necessario usare l'istruzione CREATE MEMBER. I membri calcolati definiti tramite questa istruzione sono disponibili in tutte le query MDX della sessione. L'istruzione CREATE MEMBER risulta utile, ad esempio, in un'applicazione client che riutilizza costantemente un set in vari tipi di query.  
  
     Per altre informazioni sulla creazione di membri calcolati in una sessione tramite l'istruzione CREATE MEMBER, vedere [Creazione di membri calcolati con ambito sessione &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
