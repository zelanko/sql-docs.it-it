---
title: Creazione di misure in MDX | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2095d3bde254a59c5b2edbe8ebb117854ab7777
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806129"
---
# <a name="mdx-building-measures"></a>Creazione di misure in MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Nelle espressioni MDX una misura è un'espressione DAX denominata che viene risolta tramite il calcolo dell'espressione per la restituzione di un valore in un modello tabulare. Dietro a questa definizione apparentemente semplice si nasconde un'enorme quantità di informazioni. La possibilità di creare e utilizzare misure in una query MDX offre capacità notevoli per la manipolazione dei dati tabulari.  
  
> [!WARNING]  
>  Le misure possono essere definite solo nei modelli tabulari. Se il database viene impostato in modalità multidimensionale, la creazione di una misura genera un errore  
  
 Per creare una misura definita come parte di una query MDX, pertanto con ambito limitato alla query, è necessario utilizzare la parola chiave WITH. È quindi possibile utilizzare tale misura in un'istruzione MDX SELECT. In tal modo, è possibile modificare il membro calcolato creato utilizzando la parola chiave WITH senza alterare l'istruzione SELECT. In MDX, tuttavia, si fa riferimento alla misura in modo diverso rispetto a quanto avviene nelle espressioni DAX. Per fare riferimento alla misura è necessario assegnare a essa un nome come membro della dimensione [Measures], come illustrato nell'esempio MDX seguente:  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 Dall'esecuzione verranno restituiti i dati seguenti:  
  
||Total Sales Amount||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
