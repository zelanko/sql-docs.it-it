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
ms.openlocfilehash: 01be0e2d0ead01a3b6c630e0ddd0f53e55620104
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008326"
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
  
 Gli algoritmi di terze parti possono supportare ulteriori flag di modellazione. Per determinare i flag di modellazione un algoritmo, utilizzare il **SUPPORTED_MODELING_FLAGS** set di righe dello schema. È inoltre possibile eseguire una query sui servizi di data mining nel server per determinare i flag di modellazione supportati per un algoritmo specifico. Ad esempio, la query seguente restituisce i flag di modellazione supportati per l'algoritmo Microsoft Linear Regression nel server corrente:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Risultati previsti:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Specifica dei flag di modellazione in un modello di data mining  
 Per esempi di sintassi che [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportati per la specifica un flag in una colonna della struttura di data mining, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Per un esempio della sintassi per la specifica un flag di modellazione in una colonna del modello di data mining, vedere [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Per altre informazioni sull'utilizzo delle colonne del modello di data mining, vedere [colonne del modello di Data Mining](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
