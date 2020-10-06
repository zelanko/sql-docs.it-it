---
description: PredictCaseLikelihood (DMX)
title: PredictCaseLikelihood (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a08ec4809b281205386abad429afe339e0dbb1d1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727708"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Questa funzione restituisce la probabilità che un case di input risulti adatto al modello esistente. Utilizzata solo con i modelli di tipo clustering.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>Argomenti  
 NORMALIZED  
 Il valore restituito contiene la probabilità del case nel modello diviso per la probabilità del case senza il modello.  
  
 NONNORMALIZED  
 Il valore restituito contiene la probabilità non elaborata del case, che rappresenta il prodotto delle probabilità degli attributi del case.  
  
## <a name="applies-to"></a>Si applica a  
 Modelli compilati utilizzando gli [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi clustering e [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
## <a name="return-type"></a>Tipo restituito  
 Numero a virgola mobile a precisione doppia compreso tra 0 e 1. Un numero più vicino a 1 indica che il case ha una maggiore probabilità di essere presente nel modello. Un numero più vicino a 0 indica che il case ha una minore probabilità di essere presente nel modello.  
  
## <a name="remarks"></a>Osservazioni  
 Per impostazione predefinita, il risultato della funzione **PredictCaseLikelihood** è normalizzato. I valori normalizzati sono in genere più utili come numero di attributi in un aumento del case e le differenze tra le probabilità non elaborate di uno dei due case si riducono notevolmente.  
  
 L'equazione seguente viene utilizzata per calcolare i valori normalizzati, dati x e y:  
  
-   x = probabilità del case in base al modello di clustering  
  
-   y = probabilità marginale del case, calcolata come la probabilità in forma logaritmica del case in base al conteggio dei case di training  
  
-   Z = exp (log (x)-log (Y)  
  
 Normalizzato = (z/(1 + z))  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita la probabilità che il case specificato si presenti nel modello di clustering, basato sul database [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Risultati previsti:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6.30672792729321E-08|6.30672792729321E-08|9.5824454056846E-48|  
  
 La differenza tra questi risultati dimostra l'effetto della normalizzazione. Il valore non elaborato per **CaseLikelihood** suggerisce che la probabilità del case è circa il 20%. Tuttavia, quando si normalizzano i risultati, risulta evidente che la probabilità del case è molto bassa.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining ](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
