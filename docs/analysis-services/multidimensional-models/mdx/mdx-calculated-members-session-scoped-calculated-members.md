---
title: Creazione con ambito sessione calcolati membri (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 476c62ef2aa4f0aad3d65cd2b78f27fc9ae6fd7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68176587"
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>Membri - membri calcolati con ambito sessione calcolati MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Per creare un membro calcolato disponibile nell'ambito di un'intera sessione MDX (Multidimensional Expressions), è possibile usare l'istruzione [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) . Un membro calcolato creato utilizzando l'istruzione CREATE MEMBER non viene rimosso fino alla chiusura della sessione MDX.  
  
 Come descritto in questo argomento, la sintassi dell'istruzione CREATE MEMBER è intuitiva e facile da utilizzare.  
  
> [!NOTE]  
>  Per altre informazioni sui membri calcolati, vedere [Compilazione di membri calcolati in MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
## <a name="create-member-syntax"></a>Sintassi dell'istruzione CREATE MEMBER  
 Per aggiungere l'istruzione CREATE MEMBER a un'istruzione MDX, utilizzare la sintassi seguente:  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 Nella sintassi dell'istruzione CREATE MEMBER il valore `fully-qualified-member-name` rappresenta il nome completo del membro calcolato. Il nome completo include la dimensione o il livello a cui è associato il membro calcolato. Il valore `expression` restituisce il valore del membro calcolato dopo la valutazione del valore dell'espressione.  
  
## <a name="create-member-example"></a>Esempio sull'istruzione CREATE MEMBER  
 Nell'esempio seguente l'istruzione CREATE MEMBER viene utilizzata per creare il membro calcolato `LastFourStores` , che restituisce la somma delle unità vendute negli ultimi quattro punti vendita e sarà disponibile per l'intera sessione del cubo.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di membri calcolati con ambito query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
