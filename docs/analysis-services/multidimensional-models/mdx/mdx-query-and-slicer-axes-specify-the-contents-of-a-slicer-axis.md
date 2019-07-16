---
title: Impostazione del contenuto di un asse di sezionamento (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9c21efd8ac93c6d105d11cc6b006d0cc3b916f81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208743"
---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-slicer-axis"></a>Query MDX e assi di sezionamento - Specificare il contenuto di un asse di sezionamento
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  L'asse di sezionamento filtra i dati restituiti dall'istruzione SELECT di MDX (Multidimensional Expression), limitando la restituzione ai soli dati che si intersecano con i membri specificati. Può essere considerato un asse aggiuntivo invisibile in una query. L'asse di sezionamento è definito nella clausola WHERE dell'istruzione SELECT in MDX.  
  
## <a name="slicer-axis-syntax"></a>Sintassi dell'asse di sezionamento  
 Per specificare in modo esplicito un asse di sezionamento, è necessario utilizzare `<SELECT slicer axis clause>` in MDX, come descritto nella sintassi seguente:  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 Nella sintassi dell'asse di sezionamento riportata sopra `Set_Expression` può accettare un'espressione di tupla, che viene considerata come set per la valutazione della clausola, o un'espressione set. Se viene specificata un'espressione set, viene tentata la valutazione del set mediante l'aggregazione delle celle dei risultati in ogni tupla del set. In altre parole, MDX tenta di utilizzare la funzione [Aggregate](../../../mdx/aggregate-mdx.md) sul set aggregando ogni misura in base alla funzione di aggregazione associata. Inoltre, se non è possibile esprimere l'espressione set come crossjoin di membri della gerarchia dell'attributo, ai fini della valutazione le celle esterne all'espressione set per il sezionamento vengono considerate Null.  
  
> [!IMPORTANT]  
>  A differenza della clausola WHERE in SQL, la clausola WHERE di un'istruzione MDX SELECT non filtra mai direttamente i valori restituiti nell'asse delle righe di una query. Per filtrare quanto visualizzato nell'asse delle righe o delle colonne di una query, è possibile utilizzare un'ampia gamma di funzioni MDX, ad esempio FILTER, NONEMPTY e TOPCOUNT.  
  
### <a name="implicit-slicer-axis"></a>Asse di sezionamento implicito  
 Se un membro di una gerarchia all'interno del cubo non viene incluso in un'asse della query in modo esplicito, il membro predefinito della gerarchia viene incluso nell'asse di sezionamento in modo implicito. Per altre informazioni, vedere [Definire un membro predefinito](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
## <a name="examples"></a>Esempi  
 Nella query seguente non è inclusa una clausola WHERE e viene restituito il valore della misura Internet Sales Amount per tutti gli anni di calendario:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 L'aggiunta di una clausola WHERE, come indicato di seguito:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 non modifica i valori restituiti nelle righe o nelle colonne nella query, ma modifica i valori restituiti per ogni cella. In questo esempio la query viene sezionata in modo da restituire il valore di Internet Sales Amount per tutti gli anni di calendario, ma solo per i clienti che vivono negli Stati Uniti. È possibile aggiungere più membri di gerarchie diverse alla clausola WHERE. Nella query seguente viene illustrato il valore di Internet Sales Amount per tutti gli anni di calendario per i clienti che vivono negli Stati Uniti e che hanno acquistato prodotti nella categoria Bikes:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 Se si desidera utilizzare più membri della stessa gerarchia, è necessario includere un set nella clausola WHERE. Nella query seguente, ad esempio, viene indicato il valore di Internet Sales Amount per tutti gli anni di calendario per i clienti che hanno acquistato prodotti nella categoria Bikes e che vivono negli Stati Uniti o in Regno Unito:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 Come indicato in precedenza, l'utilizzo di un set nella clausola WHERE consente di aggregare in modo implicito valori per tutti i membri del set. In questo caso, la query indica i valori aggregati per gli Stati Uniti e il Regno Unito in ogni cella.  
  
  
