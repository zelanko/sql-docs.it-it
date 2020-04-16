---
title: Celle cubo (Analysis Services - Dati multidimensionali) Documenti Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73967427b97a00d88b3d6c372a0228aa28c2024c
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387911"
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Celle del cubo (Analysis Services - Dati multidimensionali)
  Un cubo è composto di celle organizzate per gruppi di misure e dimensioni. Una cella rappresenta l'intersezione logica univoca in un cubo di un membro da ogni dimensione del cubo. Ad esempio, il cubo descritto nella figura seguente contiene un gruppo di due misure organizzato in base a tre dimensioni, denominate Source, Route e Time.  
  
 ![Diagramma del cubo in cui è evidenziata una singola cella](../../analysis-services/dev-guide/media/as-cubeintro5.gif "Diagramma del cubo in cui è evidenziata una singola cella")  
  
 La cella ombreggiata rappresenta l'intersezione dei membri seguenti:  
  
-   Il membro air della dimensione Route.  
  
-   Il membro Africa della dimensione Source.  
  
-   Il membro 4th quarter della dimensione Time.  
  
-   La misura Packages.  
  
## <a name="leaf-and-nonleaf-cells"></a>Celle foglia e non foglia  
 È possibile ottenere il valore della cella in un cubo in uno dei modi seguenti. Nell'esempio precedente, il valore nella cella può essere recuperato direttamente dalla tabella dei fatti del cubo, poiché tutti i membri utilizzati per identificare tale cella sono *membri foglia.* Un membro foglia non ha membri figlio in termini gerarchici e generalmente fa riferimento a un unico record nella tabella della dimensione. Questo tipo di cella viene definita *cella foglia*.  
  
 Tuttavia, una cella può essere identificata anche utilizzando *membri non foglia*. Un membro non foglia è un membro che ha uno o più membri figlio. In questo caso, il valore della cella viene generalmente derivato dall'aggregazione dei membri figlio associati al membro non foglia. Ad esempio, l'intersezione dei membri e delle dimensioni seguenti fa riferimento a una cella il cui valore viene fornito dall'aggregazione:  
  
-   Il membro air della dimensione Route.  
  
-   Il membro Africa della dimensione Source.  
  
-   Il membro 2nd half della dimensione Time.  
  
-   Il membro Packages.  
  
 Il membro 2nd half della dimensione Time è un membro non foglia. È pertanto necessario aggregare tutti i valori associati, come illustrato nella figura seguente.  
  
 ![Celle del 3° e 4° trimestre per il membro del 2° semestre](../../analysis-services/dev-guide/media/as-cubeintro6.gif "Celle del 3° e 4° trimestre per il membro del 2° semestre")  
  
 Supponendo che le aggregazioni dei membri 3rd quarter e 4th quarter siano somme, il valore della cella specificata è 400, che corrisponde al totale di tutte le celle foglia ombreggiate nella figura precedente. Poiché il valore della cella deriva dall'aggregazione di altre celle, la cella specificata viene considerata una *cella non foglia.*  
  
 I valori della cella derivati per i membri che utilizzano rollup personalizzati e gruppi di membri, oltre a membri personalizzati, vengono gestiti in modo simile. I valori della cella derivati per i membri calcolati, tuttavia, vengono basati completamente sull'espressione MDX (Multidimensional Expressions) utilizzata per definire il membro calcolato. In alcuni casi, ciò potrebbe non interessare alcun dato effettivo delle celle. Per ulteriori informazioni, vedere [Operatori di rollup personalizzati nelle dimensioni padre-figlio](../multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [Definizione di formule membro personalizzate](../multidimensional-models/attribute-properties-define-custom-member-formulas.md)e [Calcoli](../multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Celle vuote  
 Non è necessario che tutte le celle di un cubo contengano un valore. In un cubo possono esistere intersezioni prive di dati, che vengono chiamate celle vuote. Questo tipo di celle è frequente nei cubi, dato che non tutte le intersezioni degli attributi delle dimensioni con una misura contengono un record corrispondente nella tabella dei fatti. Il rapporto tra le celle vuote in un cubo e il numero totale di celle in un cubo viene spesso definito *sparsità* di un cubo.  
  
 Ad esempio, la struttura del cubo visualizzata nel diagramma seguente è simile a quella degli altri esempi presentati in questo argomento. Tuttavia, in questo esempio, non vi sono spedizioni aree per l'Africa nel terzo trimestre o per l'Australia nel quarto trimestre. Nella tabella dei fatti non sono presenti dati che supportano le intersezioni di queste dimensioni e misure e pertanto le celle corrispondenti a queste intersezioni sono vuote.  
  
 ![Diagramma del cubo in cui sono evidenziate le celle vuote](../../analysis-services/dev-guide/media/as-cubeintro7.gif "Diagramma del cubo in cui sono evidenziate le celle vuote")  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una cella vuota è una cella che ha qualità speciali. Dato che le celle vuote possono distorcere i risultati di cross join, conteggi e così via, molte funzioni MDX consentono di ignorare le celle vuote a scopo di calcolo. Per altre informazioni, vedere [Espressioni multidimensionali &#40;riferimento a&#41; MDX](/sql/mdx/multidimensional-expressions-mdx-reference)e Concetti chiave in MDX &#40;Analysis Services [&#41;](../multidimensional-models/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Sicurezza  
 L'accesso ai dati delle celle viene gestito in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a livello di ruolo e può essere controllato con efficacia utilizzando espressioni MDX. Per altre informazioni, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis ServicesAnalysis Services&#41;](../multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)e Concedere [l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;. ](../multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Archiviazione cubi &#40;Analysis Services -&#41;dati multidimensionaliCube Storage &#40;Analysis Services - Multidimensional Data&#41;](../multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Aggregations and Aggregation Designs](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
