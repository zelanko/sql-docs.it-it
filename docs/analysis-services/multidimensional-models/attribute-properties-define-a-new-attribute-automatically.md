---
title: Definire automaticamente un nuovo attributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5368288930526435682723ba8f50d878ff029ce1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179620"
---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>Proprietà degli attributi - Definire automaticamente un nuovo attributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile creare un nuovo attributo in una dimensione utilizzando la funzionalità di modifica tramite trascinamento in Progettazione dimensioni.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Per creare un nuovo attributo automaticamente  
  
1.  In Progettazione dimensioni aprire la dimensione in cui si desidera creare l'attributo.  
  
2.  Nella scheda **Struttura dimensione** selezionare la colonna di una tabella nel riquadro **Vista origine dati** alla quale si vuole associare l'attributo e quindi trascinare la colonna nel riquadro **Attributi** .  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea il nuovo attributo che ha lo stesso nome della colonna alla quale è associato. Se a una stessa colonna sono associati più attributi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aggiunge un numero al nome dell'attributo.  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni nei modelli multidimensionali](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [Riferimento alle proprietà degli attributi delle dimensioni](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
