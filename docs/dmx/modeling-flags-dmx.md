---
title: Flag di modellazione (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a610f3aed7f520163dc4e2b30651d8b0397ef644
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893935"
---
# <a name="modeling-flags-dmx"></a>Flag di modellazione (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è possibile utilizzare flag di modellazione per fornire a un algoritmo di data mining informazioni aggiuntive sui dati definiti in una tabella del case. L'algoritmo può utilizzare tali informazioni per compilare un modello di data mining più accurato. I flag di modellazione possono essere definiti sia sulle colonne della struttura di data mining che su quelle del modello di data mining.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta i flag di modellazione seguenti:  
  
 **NOT NULL**  
 I valori per la colonna attributo non devono mai contenere valori Null. Se durante il processo di training del modello [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] rileva un valore null per la colonna attributo, verrà generato un errore. Questo flag viene definito su una colonna di una struttura di data mining.  
  
 **REGRESSOR**  
 Indica che l'algoritmo può utilizzare la colonna specificata nella formula di regressione degli algoritmi di regressione. Questo flag è supportato dagli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] Linear Regression e [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees ed è definito su una colonna di un modello di data mining.  
  
 **MODEL_EXISTENCE_ONLY**  
 I valori della colonna attributo sono meno importanti rispetto alla presenza dell'attributo. Questo flag viene definito su una colonna di un modello di data mining.  
  
 Gli algoritmi di terze parti possono supportare ulteriori flag di modellazione. Per determinare i flag di modellazione supportati da un algoritmo, utilizzare il set di righe dello schema **SUPPORTED_MODELING_FLAGS** . È inoltre possibile eseguire una query sui servizi di data mining nel server per determinare i flag di modellazione supportati per un algoritmo specifico. Ad esempio, la query seguente restituisce i flag di modellazione supportati per l'algoritmo Microsoft Linear Regression nel server corrente:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Risultati previsti:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Specifica dei flag di modellazione in un modello di data mining  
 Per esempi della sintassi [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportata da per specificare un flag in una colonna della struttura di data mining, vedere creare una struttura [ &#40;di data mining DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Per un esempio della sintassi per specificare un flag di modellazione in una colonna del modello di data mining, vedere [ALTER MINING STRUCTURE &#40;&#41;DMX](../dmx/alter-mining-structure-dmx.md).  
  
 Per ulteriori informazioni sull'utilizzo delle colonne del modello di data mining, vedere [colonne del modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementi di sintassi &#40;DMX&#41; di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento &#40;agli&#41; operatori DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento &#40;alle&#41; istruzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenzioni della &#40;sintassi&#41; DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni &#40;di stima generali DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
