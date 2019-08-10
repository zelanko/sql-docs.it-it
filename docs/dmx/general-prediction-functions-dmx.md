---
title: Funzioni di stima generali (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 57909c1bb4009ae85b7e1b38b8b3cf3fa0e70ea9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892776"
---
# <a name="general-prediction-functions-dmx"></a>Funzioni di stima correlate (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile utilizzare l'istruzione **Select** in DMX (Data Mining Extensions) per creare diversi tipi di query. Una query può essere utilizzata per restituire informazioni sul modello di data mining stesso, per eseguire nuove stime o per modificare il modello eseguendone il training con i nuovi dati. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]fornisce un'ampia gamma di funzioni specializzate che controllano il tipo di informazioni restituite in una query. Aggiungendo queste funzioni a una query DMX, è possibile recuperare statistiche o colonne di dati aggiuntive. Tuttavia, ogni tipo di query e ogni tipo di modello supportano solo determinate funzioni.  
  
## <a name="common-functions"></a>Funzioni comuni  
 È possibile utilizzare le funzioni per estendere i risultati restituiti da un modello di data mining. Per qualsiasi istruzione **Select** che restituisce un'espressione di tabella, è possibile utilizzare le funzioni seguenti:  
  
|||  
|-|-|  
|[DMX &#40;BottomCount&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[DMX &#40;BottomPercent&#41;](../dmx/bottompercent-dmx.md)|[Conteggio conteggi &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[DMX percentuale &#40;&#41;](../dmx/toppercent-dmx.md)|  
|[DMX &#40;RangeMax&#41;](../dmx/rangemax-dmx.md)|[&#40;DMX Tops&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Inoltre, le funzioni seguenti sono supportate per quasi tutti i tipi di modello:  
  
-   [DMX &#40;esistente&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [DMX &#40;IsTestCase&#41;](../dmx/istestcase-dmx.md)  
  
-   [DMX &#40;IsTrainingCase&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [DMX &#40;RangeMax&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [DMX &#40;StructureColumn&#41;](../dmx/structurecolumn-dmx.md)  
  
 I singoli algoritmi possono supportare funzioni aggiuntive. Per un elenco delle funzioni supportate da ogni tipo di modello, vedere query di [data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).  
  
## <a name="functions-specific-to-select-syntax"></a>Funzioni specifiche per la sintassi SELECT  
 Nella tabella seguente sono elencate le funzioni che è possibile utilizzare per ogni tipo di istruzione **Select** .  
  
 Per informazioni generali sulle funzioni in DMX, vedere Guida di [riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo di query|Funzioni supportate|Note|  
|----------------|-------------------------|-------------|  
|[Selezionare Distinct dal \<modello >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [DMX &#40;RangeMax&#41;](../dmx/rangemax-dmx.md)|Queste funzioni possono essere utilizzate per fornire valori massimi, valori minimi e medie per qualsiasi colonna che contenga un tipo di dati numerico, indipendentemente dal fatto che sia continua o sia stata discretizzata.|  
|[Selezionare da \<Model >. CONTENUTO](../dmx/select-from-model-content-dmx.md)<br /><br /> oppure<br /><br /> [Selezionare da \<Model >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Questa funzione recupera i nodi figlio per il nodo specificato nel modello e può essere utilizzata, ad esempio, per scorrere i nodi nel contenuto del modello di data mining. La disposizione dei nodi nel contenuto del modello di data mining dipende dal tipo di modello. Per informazioni sulla struttura per ogni tipo di modello di data mining, vedere [contenuto &#40;dei modelli di data&#41;mining Analysis Services-Data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).<br /><br /> Se il contenuto del modello di data mining è stato salvato come dimensione, è anche possibile utilizzare altre funzioni MDX (Multidimensional Expression) disponibili per l'esecuzione di query su una gerarchia di attributo.|  
|[Selezionare da \<Model >. CASI](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [Classe ClientSettingsGeneralFlag](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [DMX &#40;IsTrainingCase&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [DMX &#40;IsTestCase&#41;](../dmx/istestcase-dmx.md)|La funzione Lag è supportata solo per i modelli Time Series.<br /><br /> La funzione IsTestCase è supportata nei modelli basati su una struttura creata usando l'opzione di controllo per creare un set di dati di testing. Se il modello non è basato su una struttura con un set di test di controllo, tutti i case vengono considerati case di training.|  
|[Selezionare da \<Model >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|In questo contesto, la funzione IsInNode restituisce un case che appartiene a un set di case di esempio idealizzati.|  
|Selezionare da \<Model >. PMML|Non applicabile. Utilizzare la funzione XML.|Le rappresentazioni PMML sono supportate solo per i tipi di modello seguenti:<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[Select from \<Model > prediction join](../dmx/select-from-model-prediction-join-dmx.md)|Funzioni di stima specifiche dell'algoritmo utilizzato per compilare il modello.|Per un elenco delle funzioni di stima per ogni tipo di modello, vedere [query di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
|[Seleziona da \<modello >](../dmx/select-from-model-dmx.md)|Funzioni di stima specifiche dell'algoritmo utilizzato per compilare il modello.|Per un elenco delle funzioni di stima per ogni tipo di modello, vedere [query di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento &#40;agli&#41; operatori DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento &#40;alle&#41; istruzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenzioni della &#40;sintassi&#41; DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Elementi di sintassi &#40;DMX&#41; di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
