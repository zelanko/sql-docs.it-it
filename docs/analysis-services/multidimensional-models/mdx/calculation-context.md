---
title: Contesto di calcolo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 340d03ba8d0c5a66d89937627ab9389fc49abcae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807734"
---
# <a name="calculation-context"></a>Contesto di calcolo
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Il contesto di calcolo è il sottospazio noto del cubo in cui viene valutata un'espressione e in cui tutte le coordinate sono note in modo esplicito o si possono derivare dall'espressione.  
  
## <a name="determining-the-calculation-context"></a>Determinazione del contesto di calcolo  
 Ogni set, membro, tupla o funzione numerica viene eseguita nel contesto dell'intera istruzione o espressione MDX. Quando un argomento, ad esempio una tupla, viene passato a una funzione, vengono specificate in modo esplicito solo alcune delle coordinate dello spazio del cubo. Le altre coordinate vengono ottenute in base al contesto di calcolo corrente.  
  
 Il contesto di calcolo per le coordinate di celle e i membri dell'attributo non specificati viene determinato nell'ordine seguente:  
  
1.  Clausola FROM (se applicabile): questa clausola consente di specificare un intero cubo o un sottocubo sotto forma di istruzione SELECT.  
  
2.  Clausola WHERE (se applicabile): clausola, anche nota come *asse di sezionamento*, in cui si specifica un set, una tupla o un membro che limita i membri restituiti sull'asse delle colonne e delle righe da una query. Concettualmente, il membro predefinito di ogni gerarchia dell'attributo non specificato in modo esplicito sull'asse delle colonne o delle righe fa parte dell'asse di sezionamento.  
  
    > [!NOTE]  
    >  Quando le coordinate di celle per un determinato attributo vengono specificate sia sull'asse di sezionamento che su un altro asse, è possibile che le coordinate specificate nella funzione abbiano la precedenza nel determinare i membri del set sull'asse. [Filter (MDX)](../../../mdx/filter-mdx.md) e [Order (MDX)](../../../mdx/order-mdx.md) sono esempi di tali funzioni. È possibile filtrare o ordinare un risultato in base ai membri dell'attributo esclusi dal contesto di calcolo dalla clausola WHERE o da un'istruzione SELECT nella clausola FROM.  
  
3.  Set denominati e membri calcolati definiti nella query o nell'espressione.  
  
4.  Tuple e set specificati sugli assi delle righe e delle colonne, utilizzando il membro predefinito per gli attributi non inclusi nell'asse delle righe, delle colonne o di sezionamento.  
  
5.  Celle del cubo o del sottocubo su ogni asse, eliminando le tuple vuote sull'asse e applicando la clausola HAVING.  
  
6.  Per altre informazioni, vedere [Definizione del contesto di cubo in una query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md).  
  
 Nella query seguente il contesto di calcolo per l'asse delle righe viene limitato dal membro dell'attributo Country e dal membro dell'attributo Calendar Year specificati nella clausola WHERE.  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 Se, tuttavia, si modifica questa query specificando la funzione **FILTER** sull'asse delle righe e si usa un membro della gerarchia dell'attributo Calendar Year nella funzione **FILTER** , è possibile modificare il membro dell'attributo della gerarchia dell'attributo Calendar Year usato per specificare il contesto di calcolo per i membri del set sull'asse delle righe.  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 Nella query precedente il contesto di calcolo per le celle nelle tuple incluse nell'asse delle colonne viene filtrato dal membro CY 2003 della gerarchia dell'attributo Calendar Year, anche se il contesto di calcolo nominale per la gerarchia dell'attributo Calendar Year è CY 2004. Viene inoltre filtrato in base alla misura Internet Order Quantity. Tuttavia, dopo avere impostato i membri del set sull'asse delle colonne, il contesto di calcolo per i valori dei membri inclusi nell'asse viene nuovamente determinato dalla clausola WHERE.  
  
> [!IMPORTANT]  
>  Per migliorare le prestazioni delle query, è consigliabile eliminare i membri e le tuple quanto prima durante il processo di risoluzione. In questo modo, i calcoli complessi in fase di query nel set finale di membri vengono eseguiti sul minor numero possibile di celle.  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione del contesto di cubo in una query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
