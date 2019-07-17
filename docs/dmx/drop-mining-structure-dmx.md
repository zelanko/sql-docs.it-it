---
title: ELIMINA STRUTTURA DI DATA MINING (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d5c94ec01ff5f11d2b7f663f09de0a7c1527f343
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074083"
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Elimina dal database la struttura di data mining specificata. Dal database verranno eliminati anche tutti i modelli di data mining associati alla struttura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura*  
 Identificatore della struttura.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminata la struttura di data mining New Mailing dal database.  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
