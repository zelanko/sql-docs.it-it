---
title: Creazione di misure in MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58bfdace704ee1be0c5b902fd24007844fcc4e45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699790"
---
# <a name="building-measures-in-mdx"></a>Compilazione di misure in MDX
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
 [Istruzione CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [Istruzione SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
