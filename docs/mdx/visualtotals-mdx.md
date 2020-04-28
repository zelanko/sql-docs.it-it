---
title: VisualTotals (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a5becd3382f07a9adc89055a253235495a7e50a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68125844"
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)


  Restituisce un set generato calcolando dinamicamente il totale dei membri figlio in un set specificato, utilizzando facoltativamente un modello per il nome del membro padre nel set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Modello*  
 Espressione stringa valida per il membro padre del set, contenente un asterisco (*) come carattere di sostituzione per il nome del padre.  
  
## <a name="remarks"></a>Osservazioni  
 L'espressione set specificata può indicare un set contenente membri a qualsiasi livello in una singola dimensione, in genere membri con una relazione predecessore-discendente. La funzione **VisualTotals** totali i valori dei membri figlio nel set specificato e ignora i membri figlio che non sono nel set nel calcolo dei totali dei risultati. Vengono calcolati i totali visualizzati per i set ordinati nella gerarchia. Se l'ordine dei membri nei set viola la gerarchia, i risultati non costituiscono totali visualizzati. VisualTotals (USA, WA, CA, Seattle), ad esempio, non restituisce WA come Seattle, bensì restituisce i valori di WA, CA e Seattle e quindi calcola il totale di tali valori come totale visualizzato per USA, conteggiando due volte le vendite di Seattle.  
  
> [!NOTE]  
>  L'applicazione della funzione **VisualTotals** ai membri della dimensione che non sono correlati a una misura o che si trovano sotto la granularità del gruppo di misure provocherà la sostituzione dei valori con null.  
  
 *Pattern*, che è facoltativo, specifica il formato per l'etichetta dei totali. Il *modello* richiede un asterisco (*) come carattere di sostituzione per il membro padre e il resto del testo nella stringa viene visualizzato nel risultato concatenato al nome padre. Per visualizzare un asterisco letterale, utilizzare due asterischi (\*\*).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il totale visualizzato per il terzo trimestre dell'anno di calendario 2001 in base all'unico discendente specificato, ovvero il mese di luglio.  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il membro [Totale] della gerarchia dell'attributo Category nella dimensione Product, con due dei quattro elementi figlio. Il totale restituito per il membro [Totale] per la misura Internet Sales Amount corrisponde al totale per i soli membri Accessories e Clothing. Viene inoltre utilizzato l'argomento Pattern per specificare l'etichetta per la colonna [All Products].  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
