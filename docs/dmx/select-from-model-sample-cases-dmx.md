---
title: Selezionare da &lt; modello &gt; . SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7eda9b0e13ee5cbf918d80f41b9a517906a56a57
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970508"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>Selezionare da &lt; modello &gt; . SAMPLE_CASES (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce case di esempio rappresentativi dei case utilizzati per il training del modello di data mining.  
  
 Per utilizzare questa istruzione, è necessario attivare il drill-through alla creazione del modello di data mining. Per ulteriori informazioni sull'abilitazione del drill-through, vedere Creazione di un [modello di data mining &#40;dmx&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)e [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativa. Valore intero mediante il quale viene specificato il numero di righe da restituire.  
  
 *elenco di espressioni*  
 Elenco delimitato da virgole contenente identificatori di colonna correlati.  
  
 *model*  
 Identificatore del modello.  
  
 *Elenco condizioni*  
 Facoltativa. Condizioni per limitare i valori restituiti dall'elenco di colonne.  
  
 *expression*  
 Facoltativa. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 I case di esempio potrebbero essere generati e potrebbero non esistere effettivamente nei dati utilizzati per il training. Il case restituito è rappresentativo del nodo di contenuto specificato.  
  
 Sebbene l' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Sequence Clustering sia l'unico [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo che supporta l'utilizzo di Select from \<model> . SAMPLE_CASES, gli algoritmi di terze parti possono anche supportarla.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i case di esempio utilizzati per il training del modello di data mining Target Mail. Utilizzando la funzione [IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md) nella clausola **where** vengono restituiti solo i case associati al nodo ' 000000003'. La stringa del nodo si trova nella colonna NODE_UNIQUE_NAME del set di righe dello schema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SELEZIONARE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
