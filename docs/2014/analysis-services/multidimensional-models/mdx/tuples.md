---
title: Tuple | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e6565d727ad6fd3f11e2332f53e32fb2c942687
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725165"
---
# <a name="tuples"></a>Tuple
  Una tupla consente di identificare in modo univoco una sezione di dati di un cubo. La tupla viene creata da una combinazione di membri di dimensione, finché non esistono due o più membri che appartengono alla medesima gerarchia.  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>Membri dell'attributo impliciti o predefiniti in una tupla  
 Quando si definisce una tupla in una query o espressione MDX, non è necessario includere in modo esplicito il membro dell'attributo di ogni gerarchia dell'attributo. Se un membro di una gerarchia dell'attributo non viene incluso in una query o espressione in modo esplicito, il membro predefinito della gerarchia dell'attributo è il membro dell'attributo incluso nella tupla in modo implicito. Se non altrimenti definito in modo esplicito in un cubo, il membro predefinito per ogni gerarchia dell'attributo è il membro (Totale), se esistente. Se non esiste un membro (Totale) all'interno di una gerarchia dell'attributo, il membro predefinito è un membro del livello principale della gerarchia dell'attributo. La misura predefinita è la prima misura specificata nel cubo, a meno che non venga definita in modo esplicito una misura predefinita. Per altre informazioni, vedere [Definire un membro predefinito](../attribute-properties-define-a-default-member.md) e [DefaultMember &#40;MDX&#41;](/sql/mdx/defaultmember-mdx).  
  
 La tupla seguente identifica ad esempio una singola cella nel database Adventure Works definendo in modo esplicito un solo membro della dimensione Measures.  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 Nell'esempio precedente viene identificata in modo univoco la cella costituita dal membro Reseller Sales Amount della dimensione Measures e dal membro predefinito di ogni gerarchia dell'attributo del cubo. Il membro predefinito è il membro (Totale) per ogni gerarchia dell'attributo diversa dalla gerarchia dell'attributo Destination Currency. Il membro predefinito per la gerarchia Destination Currency, è il membro US Dollar. Questo membro predefinito viene definito nello script MDX del cubo Adventure Works.  
  
 Nella query seguente viene restituito il valore della cella a cui fa riferimento la tupla specificata nell'esempio precedente, ($80,450.596.98).  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Quando in una query si specifica un asse per un set (in questo caso costituito da una sola tupla), è necessario specificare innanzitutto un set per l'asse delle colonne prima di specificare un set per l'asse delle righe. L'asse delle colonne è inoltre noto come *Axis(0)* o semplicemente *0*. Per altre informazioni, vedere [Query MDX di base &#40;MDX&#41;](mdx-query-the-basic-query.md).  
  
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
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Spazio del cubo](cube-space.md)   
 [Auto Exist](autoexists.md)   
 [Utilizzo di membri, tuple e set &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)  
  
  
