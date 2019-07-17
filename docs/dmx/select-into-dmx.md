---
title: SELECT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a34cdf743ff0bcecbb4b3088d99efdf3bbfef744
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938165"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea un nuovo modello di data mining compilato in base alla struttura di data mining di un modello di data mining esistente. Il **SELECT INTO** istruzione crea il nuovo modello di data mining copiando lo schema e altre informazioni che non sono specifiche dell'algoritmo effettivo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>Argomenti  
 *nuovo modello*  
 Nome univoco del nuovo modello da creare.  
  
 *algorithm*  
 Nome definito dal provider di un algoritmo di data mining.  
  
 *elenco di parametri*  
 facoltativo. Elenco delimitato da virgole dei parametri definiti dal provider per l'algoritmo.  
  
 *expression*  
 Espressione che restituisce una condizione di filtro valida sui dati di training. Per altre informazioni sulle espressioni che possono essere utilizzate come filtri, vedere [i filtri per i modelli di Data Mining &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 *modello esistente*  
 Nome del modello esistente da copiare.  
  
## <a name="remarks"></a>Note  
 Se il modello esistente è stato sottoposto a training, il nuovo modello verrà automaticamente elaborato quando viene eseguita l'istruzione. In caso contrario il nuovo modello rimarrà non elaborato.  
  
 Il **SELECT INTO** istruzione funziona solo se la struttura del modello esistente è compatibile con l'algoritmo del nuovo modello. Pertanto, questa istruzione è molto utile per creare e testare rapidamente modelli basati sullo stesso algoritmo. Se si modifica il tipo di algoritmo, il nuovo algoritmo deve supportare il tipo di dati di ogni colonna presente nel modello esistente, altrimenti potrebbe verificarsi un errore quando viene elaborato il modello.  
  
 Il **WITH DRILLTHROUGH** clausola consente il drill-through sul nuovo modello di data mining. È possibile attivare il drill-through solo al momento della creazione del modello.  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>Esempio 1: Modifica dei parametri del modello  
 L'esempio seguente crea un nuovo modello di data mining basato su un modello di data mining esistente, `TM_Clustering`, che si crea nel [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Il parametro CLUSTER_COUNT viene modificato in modo che nel nuovo modello esistano al massimo cinque cluster. Nel modello esistente viene invece utilizzato il valore predefinito 10.  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>Esempio 2: Aggiunta di un filtro al modello  
 Nell'esempio seguente viene creato un nuovo modello di data mining basato su un modello di data mining esistente e viene aggiunto un filtro nel modello. Il filtro limita i dati di training solo ai clienti che vivono in un'area specifica.  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  I filtri applicati alla tabella del case possono essere modificati mediante l'istruzione SELECT INTO come mostrato in questo esempio. Tuttavia, se il modello originale contiene un filtro in una tabella nidificata, il filtro della tabella nidificata non può essere modificato o rimosso mediante questa sintassi, ma viene copiato dal modello originale senza alcuna modifica. Per creare un modello con un filtro diverso in una tabella nidificata, utilizzare la sintassi ALTER STRTUCTURE...ADD MODEL.  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
