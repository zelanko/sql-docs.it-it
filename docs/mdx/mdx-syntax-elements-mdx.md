---
description: Elementi della sintassi MDX (MDX)
title: Elementi della sintassi MDX (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 10a9aa360a50b43324ae9e41b77dee6ce84baf60
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483894"
---
# <a name="mdx-syntax-elements-mdx"></a>Elementi della sintassi MDX (MDX)


  Il linguaggio MDX (Multidimensional Expressions) include numerosi elementi utilizzati nella maggior parte delle istruzioni o che ne influenzano l'esecuzione:  
  
|Termine|Definizione|  
|----------|----------------|  
|[Identificatori](../mdx/identifiers-mdx.md)|Gli identificatori sono nomi di oggetti quali cubi, dimensioni, membri e misure.|  
|**Tipi di dati**|Definiscono i tipi dei dati contenuti nelle celle, nelle proprietà dei membri e nelle proprietà delle celle. MDX supporta solo il tipo di dati OLE VARIANT. Per ulteriori informazioni sulla coercizione, la conversione e la modifica del tipo di dati VARIANT, vedere l'argomento dedicato a VARIANT e VARIANTARG nella documentazione di Platform SDK.|  
|[Espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)|Le espressioni sono unità di sintassi che Analysis Services possibile risolvere in oggetti o valori singoli (scalari). Le espressioni includono funzioni che restituiscono un singolo valore, un'espressione set e così via.|  
|[Operatori](../mdx/operators-mdx-syntax.md)|Gli operatori sono elementi di sintassi che utilizzano una o più espressioni MDX semplici per formare espressioni MDX più complesse.|  
|[Funzioni](../mdx/functions-mdx-syntax.md)|Le funzioni sono elementi di sintassi che accettano zero, uno o più valori di input e che restituiscono un valore scalare o un oggetto. Gli esempi includono la funzione [Sum](../mdx/sum-mdx.md) per l'aggiunta di diversi valori, la funzione [Members](../mdx/members-set-mdx.md) per la restituzione di un set di membri da una dimensione o un livello e così via.|  
|[Commenti](../mdx/comments-mdx-syntax.md)|I commenti sono parti di testo inserite all'interno di istruzioni MDX o script per spiegarne lo scopo dell'istruzione. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non esegue commenti.|  
|[Parole chiave riservate](../mdx/reserved-keywords-mdx-syntax.md)|Le parole chiave riservate sono parole che vengono utilizzate da MDX e non possono essere utilizzate come nomi per gli oggetti impiegati nelle istruzioni MDX.|  
|[Membri, tuple e set](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)|Prima di creare una query MDX, è necessario comprendere i concetti di membro, tupla e set.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
