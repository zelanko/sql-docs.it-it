---
title: Creare gerarchie definite dall'utente | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6ca49e3a7714134d554538ae4f37e267999f2c2
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52983862"
---
# <a name="user-defined-hierarchies---create"></a>Gerarchie definite dall'utente - Creare
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di creare gerarchie definite dall'utente. Una gerarchia è una raccolta di livelli basata su attributi. Ad esempio, la gerarchia temporale potrebbe includere i livelli Anno, Trimestre, Mese, Settimana e Giorno. In alcune gerarchie, ogni attributo del membro comprende in modo univoco l'attributo del membro che si trova ad un livello superiore. A questo talvolta si fa riferimento come gerarchia naturale. Una gerarchia può essere utilizzata dagli utenti finali per esplorare i dati del cubo. Definire gerarchie utilizzando il riquadro Gerarchie di Progettazione Dimensioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Quando si crea una gerarchia definita dall'utente, è possibile che la gerarchia sia *incompleta*. In una gerarchia incompleta, il membro padre logico di almeno un membro non si trova nel livello immediatamente superiore rispetto al membro stesso. Se si ha una gerarchia incompleta, ci sono impostazioni che controllano se i membri mancanti sono visibili e come visualizzare i membri mancanti. Per altre informazioni, vedere [Gerarchie incomplete](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà delle gerarchie definite dall'utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Proprietà livello - Gerarchie utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Dimensioni padre-figlio](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
