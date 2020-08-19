---
description: ClusterProbability (DMX)
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f27a901bbb45c48996c82bbedbbb3691c1a6cbc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431113"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce la probabilità che il case di input appartenga al cluster specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Si applica a  
 È possibile utilizzare questa funzione solo se il modello di data mining sottostante supporta il clustering.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 La sintassi seguente utilizza il set di righe dello schema relativo al contenuto del modello di data mining per restituire le didascalie dei nodi esistenti nel modello di data mining.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Per ulteriori informazioni sull'utilizzo di questa sintassi, vedere [selezionare da &#60;modello&#62;. CONTENUTO &#40;&#41;DMX ](../dmx/select-from-model-content-dmx.md). Per ulteriori informazioni sul set di righe dello schema del contenuto del modello di data mining, vedere [DMSCHEMA_MINING_MODEL_CONTENT set di righe](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126267(v=sql.110)).  
  
 Se \<node caption> non si specifica alcun valore, la funzione restituisce la probabilità che i case di input appartengano al cluster più probabile. Usare la funzione **cluster** per restituire il cluster più probabile.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la probabilità che il case specificato esista nel cluster con etichetta Cluster 2.  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;&#41;DMX del cluster ](../dmx/cluster-dmx.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
