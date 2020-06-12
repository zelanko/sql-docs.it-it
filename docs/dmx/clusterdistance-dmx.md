---
title: ClusterDistance (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 149285ac5888d6b23272b40fbbb1aef9cf55909e
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669817"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La funzione **ClusterDistance** restituisce la distanza del case di input dal cluster specificato o, se non viene specificato alcun cluster, la distanza del case di input dal cluster più probabile.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>Si applica a  
 È possibile utilizzare questa funzione solo se il modello di data mining sottostante supporta il clustering. La funzione può essere utilizzata con qualsiasi tipo di modello di clustering (EM, K-medie, ecc.), ma i risultati variano in base all'algoritmo.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare.  
  
## <a name="remarks"></a>Commenti  
 La funzione **ClusterDistance** restituisce la distanza tra il case di input e il cluster con la probabilità più elevata per tale case di input.  
  
 Poiché con il clustering K-medie un case può appartenere solo a un cluster, la distanza del cluster è sempre 0 con un peso di appartenenza di 1.0. Tuttavia, in K-medie si presuppone che per ogni cluster sia presente un centro. È possibile ottenere il valore del centro esplorando o eseguendo una query sulla tabella nidificata NODE_DISTRIBUTION nel contenuto del modello di data mining. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining).  
  
 Con il metodo di clustering predefinito EM tutti i punti nel cluster presentano la stessa probabilità; pertanto, per motivi strutturali non è previsto un centro per il cluster. Il valore di **ClusterDistance** tra un particolare caso e un particolare cluster *N* viene calcolato come segue:  
  
 ClusterDistance (N) = 1-(membershipWeight (N))  
  
 Oppure:  
  
 ClusterDistance (N) = 1-ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>Funzioni di stima correlate  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sono disponibili le seguenti funzioni aggiuntive per l'esecuzione di query sui modelli di clustering:  
  
-   Utilizzare la funzione [&#41;DMX &#40;](../dmx/cluster-dmx.md) per restituire il cluster più probabile.  
  
-   Usare la funzione [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md) per ottenere la probabilità che un case appartenga a un cluster specifico. Questo valore viene utilizzato come valore inverso della distanza del cluster.  
  
-   Utilizzare la funzione [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) per restituire un istogramma della probabilità del case di input esistente in ogni cluster del modello.  
  
-   Utilizzare la funzione [PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md) per restituire una misura da 0 a 1 che indica la probabilità che un case di input esista considerando il modello appreso dall'algoritmo.  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Esempio 1: Acquisizione della distanza del cluster rispetto al cluster più probabile  
 Nell'esempio seguente viene restituita la distanza dal case specificato al cluster a cui appartiene il case più probabile.  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Espressione|  
|----------------|  
|0.0477390930705145|  
  
 Per individuare il tipo di cluster, è possibile utilizzare `Cluster` al posto di `ClusterDistance` nell'esempio precedente.  
  
 Risultati dell'esempio:  
  
|$CLUSTER|  
|--------------|  
|Cluster 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Esempio 2: Acquisizione della distanza rispetto a un cluster specificato  
 La sintassi seguente utilizza il set di righe dello schema relativo al contenuto del modello di data mining per restituire l'elenco degli ID dei nodi e le didascalie dei nodi per i cluster del modello di data mining. È quindi possibile usare la didascalia del nodo come argomento dell'identificatore del cluster nella funzione **ClusterDistance** .  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 Risultati dell'esempio:  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|Cluster 1|  
|002|Cluster 2|  
  
 Nell'esempio di sintassi seguente viene restituita la distanza del case specificato dal cluster con etichetta Cluster 2.  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Risultati dell'esempio:  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;&#41;DMX del cluster](../dmx/cluster-dmx.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Contenuto dei modelli di data mining per i modelli di clustering &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)  
  
  
