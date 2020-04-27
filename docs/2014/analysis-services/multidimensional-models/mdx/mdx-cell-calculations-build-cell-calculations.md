---
title: Compilazione di calcoli di celle in MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b1d0c01be4901e771278c82c4277c280aeb43ad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074522"
---
# <a name="building-cell-calculations-in-mdx-mdx"></a>Compilazione di formule per il calcolo di celle in MDX (MDX)
  Nel linguaggio MDX (Multidimensional Expressions) sono disponibili numerosi strumenti per la generazione di valori calcolati, ad esempio membri calcolati, rollup personalizzati e membri personalizzati. Utilizzando tali caratteristiche è tuttavia difficile agire su un set specifico di celle o su una singola cella.  
  
 Per generare valori calcolati per celle specifiche, è necessario utilizzare la caratteristica MDX per le celle calcolate. Le celle calcolate consentono di definire una specifica sezione di celle, detta *sottocubo di calcolo*, e di applicare una formula a ogni singola cella del sottocubo di calcolo in base a una condizione facoltativa applicabile a ogni cella.  
  
 Le celle calcolate offrono inoltre funzionalità complesse, ad esempio le formule per la ricerca dell'obiettivo utilizzate negli indicatori di prestazioni chiave (KPI) oppure le formule per l'analisi speculativa. Questo livello di funzionalità deriva dalla funzionalità di pass-Order [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in che consente di eseguire passaggi ricorsivi con le celle calcolate, con le formule di calcolo applicate a passate specifiche nell'ordine di superamento. Per altre informazioni sull'ordine di calcolo, vedere [Informazioni sull'ordine di calcolo e di valutazione &#40;MDX&#41;](mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Per quanto concerne l'ambito di creazione, le celle calcolate sono simili sia ai set denominati che ai membri calcolati, poiché possono essere create temporaneamente per la durata di una sessione o di una singola query oppure possono essere rese disponibili a livello globale nell'ambito di un cubo.  
  
-   **Ambito query** Per creare una cella calcolata definita come parte di una query MDX e il cui ambito è pertanto limitato alla query, è necessario specificare la parola chiave WITH. La cella calcolata può essere quindi utilizzata in un'istruzione MDX SELECT. Utilizzando questo approccio è possibile modificare la cella calcolata creata utilizzando la parola chiave `WITH` senza alterare l'istruzione SELECT.  
  
     Per altre informazioni sulla creazione di membri calcolati mediante la parola chiave WITH, vedere [Creazione di formule per il calcolo di celle con ambito query &#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
-   **Ambito sessione** Per creare una cella calcolata il cui ambito risulti più ampio del contesto della query, ovvero il cui ambito corrisponda alla durata della sessione MDX, è necessario usare l'istruzione CREATE CELL CALCULATION o l'istruzione ALTER CUBE.  
  
     Per altre informazioni sulla creazione di celle calcolate in una sessione mediante l'istruzione CREATE CELL CALCULATION o l'istruzione ALTER CUBE, vedere [Creazione di celle calcolate con ambito sessione](mdx-cell-calculations-session-scoped-calculated-cells.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Istruzione ALTER CUBE &#40;&#41;MDX](/sql/mdx/mdx-data-definition-alter-cube)   
 [Istruzione CREATE CELL CALCULATION &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-cell-calculation)   
 [Creazione di calcoli di celle con ambito query &#40;&#41;MDX](../../multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
