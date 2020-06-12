---
title: AGGIORNAMENTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9c4f8c1b48ccc6b3f2c2363671f5e3c072f77042
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669168"
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Facoltativa. Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
## <a name="examples"></a>Esempio  
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
  
  
