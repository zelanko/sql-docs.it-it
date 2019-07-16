---
title: Utilizzando Progettazione Query e assi di sezionamento in un semplice esempio (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fce95d7e51c17f6e8a0fedbec01eccf7bd8ec8c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165831"
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>Query MDX e assi di sezionamento - Uso degli assi in un semplice esempio
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Il semplice esempio presentato in questo argomento illustra le nozioni fondamentali sull'impostazione e l'utilizzo di assi di query e assi di sezionamento.  
  
## <a name="the-cube"></a>Il cubo  
 Viene utilizzato un cubo con il nome TestCube e due semplici dimensioni, Route e Time. Ogni dimensione include un'unica gerarchia utente, Route e Time rispettivamente. Poiché le misure del cubo fanno parte della dimensione Measures, il cubo ha in tutto tre dimensioni.  
  
## <a name="the-query"></a>La query  
 La query deve restituire una matrice in cui è possibile confrontare la misura Packages su vari canali di distribuzione e periodi di tempo.  
  
 Nella seguente query MDX di esempio gli assi della query sono costituiti dalle gerarchie Route e Time, mentre la dimensione Measures costituisce l'asse di sezionamento. La funzione [Members](../../../mdx/members-set-mdx.md) indica che MDX utilizzerà i membri della gerarchia o del livello per costruire un set. Poiché viene utilizzata la funzione **Members** , non è necessario definire esplicitamente ogni membro di una gerarchia o di un livello specifico in una query MDX.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>I risultati  
 Il risultato è costituito da una griglia che identifica il valore della misura Packages per ogni intersezione delle dimensioni degli assi COLUMNS e ROWS. Tale griglia è illustrata nella tabella seguente.  
  
||air|sea|  
|-|---------|---------|  
|1st quarter|60|50|  
|2nd quarter|45|45|  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione del contenuto di un asse della query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Impostazione del contenuto di un asse di sezionamento &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
