---
title: Tuple | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33bfe1d6e46a7687736afd837614eec350a941ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165757"
---
# <a name="tuples"></a>Tuple
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Una tupla consente di identificare in modo univoco una sezione di dati di un cubo. La tupla viene creata da una combinazione di membri di dimensione, finché non esistono due o più membri che appartengono alla medesima gerarchia.  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>Membri dell'attributo impliciti o predefiniti in una tupla  
 Quando si definisce una tupla in una query o espressione MDX, non è necessario includere in modo esplicito il membro dell'attributo di ogni gerarchia dell'attributo. Se un membro di una gerarchia dell'attributo non viene incluso in una query o espressione in modo esplicito, il membro predefinito della gerarchia dell'attributo è il membro dell'attributo incluso nella tupla in modo implicito. Se non altrimenti definito in modo esplicito in un cubo, il membro predefinito per ogni gerarchia dell'attributo è il membro (Totale), se esistente. Se non esiste un membro (Totale) all'interno di una gerarchia dell'attributo, il membro predefinito è un membro del livello principale della gerarchia dell'attributo. La misura predefinita è la prima misura specificata nel cubo, a meno che non venga definita in modo esplicito una misura predefinita. Per altre informazioni, vedere [Definire un membro predefinito](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md) e [DefaultMember &#40;MDX&#41;](../../../mdx/defaultmember-mdx.md).  
  
 La tupla seguente identifica ad esempio una singola cella nel database Adventure Works definendo in modo esplicito un solo membro della dimensione Measures.  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 Nell'esempio precedente viene identificata in modo univoco la cella costituita dal membro Reseller Sales Amount della dimensione Measures e dal membro predefinito di ogni gerarchia dell'attributo del cubo. Il membro predefinito è il membro (Totale) per ogni gerarchia dell'attributo diversa dalla gerarchia dell'attributo Destination Currency. Il membro predefinito per la gerarchia Destination Currency, è il membro US Dollar. Questo membro predefinito viene definito nello script MDX del cubo Adventure Works.  
  
> [!IMPORTANT]  
>  Il membro di una gerarchia dell'attributo in una tupla viene influenzato anche dalle relazioni definite tra gli attributi all'interno di una dimensione.  
  
 Nella query seguente viene restituito il valore della cella a cui fa riferimento la tupla specificata nell'esempio precedente, ($80,450.596.98).  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Quando in una query si specifica un asse per un set (in questo caso costituito da una sola tupla), è necessario specificare innanzitutto un set per l'asse delle colonne prima di specificare un set per l'asse delle righe. L'asse delle colonne è inoltre noto come *Axis(0)* o semplicemente *0*. Per altre informazioni, vedere [Query MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md).  
  
### <a name="tuples-as-values-or-member-references"></a>Tuple come riferimenti a valori o al membro  
 È inoltre possibile usare una tupla in una query per restituire il valore della cella a cui fa riferimento la tupla, come nell'esempio precedente, oppure è possibile usarla in un'espressione per fare riferimento in modo esplicito ai membri specificati nella tupla. La query o l'espressione consente di impiegare funzioni che restituiscono o usano le tuple. Una tupla può essere usata per fare riferimento al valore della cella specificata dalla tupla o per specificare una combinazione di membri quando viene usata in una funzione.  
  
### <a name="tuple-dimensionality"></a>Dimensionalità della tupla  
 Per *dimensionalità* di una tupla si intende la sequenza o l'ordine dei membri nella tupla. Dal momento che i membri impliciti ricorrono sempre nello stesso ordine, la dimensionalità viene spesso considerata in relazione ai membri della tupla definiti in modo esplicito. L'ordinamento dei membri della tupla è importante quando si definisce un set di tuple. Nell'esempio seguente vengono inclusi due membri di una tupla nell'asse delle colonne.  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Quando si specifica in modo esplicito un membro in una tupla da più di una dimensione, è necessario includere l'intera tupla tra parentesi. Quando si specifica un solo membro in una tupla, le parentesi sono facoltative.  
  
 La tupla nella query dell'esempio precedente specifica la restituzione della cella del cubo nel punto di intersezione tra la misura Reseller Sales Amount della dimensione Measures e il membro CY 2004 della gerarchia dell'attributo Calendar Year nella dimensione Date.  
  
> [!NOTE]  
>  È possibile fare riferimento a un membro dell'attributo tramite il nome o la chiave del membro. Nell'esempio precedente, è possibile sostituire il riferimento a [CY 2004] con &[2004].  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Spazio del cubo](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Auto Exist](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Utilizzo di membri, tuple e set &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)  
  
  
