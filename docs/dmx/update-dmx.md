---
description: UPDATE (DMX)
title: AGGIORNAMENTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d74a59aaea079a5d3c1945b92813f6d276591b78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394877"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Modifica la colonna **NODE_CAPTION** nel modello di data mining.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>Argomenti  
 *model*  
 Identificatore del modello.  
  
 *nuova didascalia*  
 Stringa che contiene il nuovo nome per la colonna **NODE_CAPTION** .  
  
 *espressione della condizione*  
 Facoltativo. Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente, l'istruzione **Update** modifica il nome predefinito, `Cluster 1` , per il cluster `001` con il nome più descrittivo `Likely Customers` .  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
