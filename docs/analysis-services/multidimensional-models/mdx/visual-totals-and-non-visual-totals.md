---
title: Totali visualizzati e totali Non | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90925c99f281d128ff197fb7b0ef3b088faf5b7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62984472"
---
# <a name="visual-totals-and-non-visual-totals"></a>Totali visualizzati e non visualizzati
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  I totali visualizzati sono totali alla fine di una colonna o riga in cui vengono sommati tutti gli elementi visibili della colonna o riga. Questo è il comportamento predefinito per la maggior parte delle tabelle visualizzate. Tuttavia, in alcuni casi per l'utente è utile visualizzare solo alcune colonne di una tabella, conservando però i totali per la riga intera, compresi gli elementi non visualizzati. Questi vengono chiamati **Totali non visualizzati**, perché il totale è il risultato di valori visualizzati e non visualizzati.  
  
 Nello scenario riportato di seguito viene illustrato il comportamento dei totali non visualizzati. Il primo passaggio mostra il comportamento predefinito dei totali visualizzati.  
  
 L'esempio che segue è una query di [Adventure Works] per ottenere le cifre di [Reseller Sales Amount] in una tabella in cui le categorie dei prodotti sono le colonne e i tipi di attività dei rivenditori sono le righe. Vengono forniti i totali relativi sia ai prodotti che ai rivenditori non appena si esegue l'istruzione SELECT seguente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce i risultati seguenti:  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**Clothing**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>Totale non visualizzato su righe e colonne  
 Per produrre una tabella solo con i dati per i prodotti Accessories e Clothing, i rivenditori Value Added Reseller e Warehouse, conservando tuttavia i totali complessivi, si potrebbe scrivere una query come la seguente utilizzando NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce i risultati seguenti:  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>Totale non visualizzato sulle righe  
 Per produrre una tabella che visivamente somma le colonne, ma per i totali delle righe riporta il totale vero di [Category], immettere la query seguente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Notare come NON VISUAL è applicato solo a [Category].  
  
 La query precedente produce i seguenti risultati:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Se si confrontano i risultati precedenti, è possibile osservare che la riga [All Resellers] si aggiunge ai valori visualizzati di [Value Added Reseller] e [Warehouse] ma che la colonna [All Products] mostra il valore totale per tutti i prodotti, compresi quelli non visualizzati.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Utilizzo di membri, tuple e set &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Query MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Restrizione della query con gli assi della query e di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)   
 [Definizione del contesto di cubo in una query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)  
  
  
